# Введение

__Rect Engine 5__ (RE-5) - это объектно-ориентированый движок-фреймворк для разработки 2D игр на JavaScript. Графика в RE-5 работает основе WebGL2(ссылка) (браузерная адаптация OpenGL3.0(ссылка)). Движок подходит как для создания небольших игр так и для сложных многопользовательских проектов. В движке присутствует гибкая система плагинов, что может существенно расширить функционал движка. Больше проектов на RE-5 вы можете найти здесь: (ссылка).

# Создание проекта

- Установите любой локальный сервер или же воспользуйтесь небольшим сервером на Node.js (ссылка).
- Скачайте и установите движок на свой ПК (ссылка).
- Создайте папку для роекта и откройте её в командной строке.
- Введите команду:
```
rjs
```
- Дождитесь окончания загрузки
- Когда вы откроете проект в браузере должен появиться пурпурный вращающийся прямоугольник на сером фоне.

# Структура проекта

- __Engine__ (файлы движка)
	- __Shaders__ (шейдеры)
		- __fragment-shader.glsl__ (фрагментный шейдер)
		- __vertex-shader.glsl__ (вершинный шейдер)
	- __collision.js__ (обработка столкновений)
	- __engine.js__ (логика движка, интерфейс)
	- __renderer.js__ (отрисовка графики)
- __Plugins__ (плагины)
- __Scene__ (сцены)
	- __new__ (файлы сцены)
		- __end.js__ (срабатывает при каждом переходе с этой сцены на другую)
		- __init.js__ (срабатывает единажды при инициализации сцены)
		- __start.js__ (срабатывает при каждом старте сцены)
- __Scripts__ (скрипты)
	- __assets.js__ (скрыпт для создания и настройки ассетов)
	- __config.js__ (скрипт для настроек движка и проекта)
	- __families.js__ (скрипт для создания семей объектов)
	- __sources.js__ (скрипт для загрузки ресурсов)
- __Sources__ (ресурсы)
	- __audio__ (аудиофайлы)
	- __images__ (текстуры)
	- __json__ (JSON файлы)
- __index.html__ (запускает main.js)
- __main.js__ (инициализация движка, запуск всех скриптов)

# Архитектура

![alt text](https://github.com/BSS-Lord/RE-5/blob/master/re5architecture.png "Архитектура")

# Инициализация и игровой цикл

![alt text](https://github.com/BSS-Lord/RE-5/blob/master/re5logic.png "Инициализация и игровой цикл")

# Как устроен проект

В файле __*main.js*__ инициализируется движок, загружаются все скрипты из папки __*Scripts*__, создаются сцены, к сценам подключаются скрипты из папки __*Scenes/название сцены*__, осуществляется переход на нужную сцену.

В скрипте __*config.js*__ устанавливаются настройки движка и проекта в целом.

В скрипте __*families.js*__ создаются семьи объектов.

В скрипте __*sources.js*__ загружаются все нужные ресурсы (текстуры, звуки, шрифты...)

В скрипте __*assets.js*__ создаются/загружаются ассеты объектов.

Вы можете создавать свои скрипты в папке __*Scripts*__ или папках сцен и подключать их самостоятельно откуда вам угодно.

В папке каждой сцены лежит 3 файла:
- __*init.js*__ - скрипт выполняется единажды при инициализации сцены, здесь создается камера для сцены, слои и большинство объектов, создаётся игровой цикл сцены, нужные слушатели событий.
- __*start.js*__ - скрит выполняется при каждом запуске сцены, здесь игра переключается на нужную камеру, изменяются нужные параметры движка, происходит запуск уровня, расстановка врагов и т.д.
- __*end.js*__ - скрит выполняется при каждом переходе с этой сцены на другую, выключаются разные специальные параметры движка (как особый тип рендеринга или режим оптимизации), которые больше не нужны на других уровнях, может сохраняться игровой прогресс

# Основные методы

### new RectJS(callback)

- __callback__ `<function>` - принимает объект экземпляра движка перед его инициализацие

Инициализация движка

### require(src[, type])

- __src__ `<string>` - относительный путь к файлу
- __type__ `<string>` __*Default:*__ `"JS"` - тип файла
	- __"JS"__ - JavaScript. Метод возвращает функцию из скрипта.
	- __"JSON"__ - JSON файл. Метод возвращает JavaScript-объект из JSON файла.
	- __"TEXT"__ - Текстовый файл. Метод возвращает текст файла в виде строки.

__ВНИМАНИЕ!__ Каждый скрипт являет собою либо стрелочную функцию:
```javascript
(params) => {
	// код скрипта
}
```
либо функцию взятую в скобки:
```javascript
(function (params) {
	// код скрипта
})
```

__ВНИМАНИЕ!__ Чтобы переменная была доступна во всех скриптах она должна быть глобальной. Есть 3 способа сделать переменную глобальной:
- создать переменную без использования ключевого слова в любом скрипте (рекомендовано)
`variable = 1;`
- задать переменную как свойство объекта __window__
`window.variable = 1`
- создать переменную за пределами слушателя события "onload" в файле __*main.js*__
```javascript
var variable = 1;

window.addEventListener('load', e => {
...
```

### new RectJS.Scene(options)

- __options__ `<object>`
	- __id__ `<string>` __*Default:*__ `"scene_{номер сцены}"` - идентификатор сцены
	- __init__ `<function>` __*Default:*__ `() => {}` - скрипт, что выполнится при инициализации сцены, принимает объект сцены
	- __start__ `<function>` __*Default:*__ `() => {}` - скрипт, что выполнится при переходе на сцену, принимает объект сцены и объект с параметрами зауска сцены.
	- __end__ `<function>` __*Default:*__ `() => {}` - скрипт, что выполнится при переходе с этой сцены на другую, принимает объект сцены и объект с параметрами зауска окончания сцены.
	- __initOnload__ `<boolean>` __*Default:*__ `true`
		- __true__ - скрипт инициализации сцены запускается сразу после её создания
		- __false__ - скрипт инициализации сцены запускается перед сразу перед её первым запуском
		
Создание сцены. Возвращает объект сцены.

Пример скрипта инициализации сцены:
```javascript
(scene) => {
	
	// создание камеры
	
	// создание слоёв
	
	// создание объектов и циклов, игровая логика
	
}
```
Пример скрипта запуска и окончания сцены:
```javascript
(scene, params) => {
	
	// код
	
}
```

### Scene.set([startParams[ ,endParams]])

- __startParams__ `<object>` - параметры, что передаются в скрипт запуска сцены
- __endParams__ `<object>` - параметры, что передаются в скрипт окончания сцены

Переход на сцену

### Scene.update()

Обновление объектов на сцене. Выполняется автоматически при переходе на сцену.

### new RectJS.Vector2([x, y])

- __x__ `<number>` | `<string>` __*Default:*__ `0` - горизонтальная координата вектора
- __y__ `<number>` | `<string>` __*Default:*__ `0` - вертикальная координата вектора

Создание двухмерного вектора. Возвращает вектор в виде объекта.

### Vector2.toString()

Перевод вектора в формат строки. Возвращает вектор в виде строки. `"v{координата X};{координата Y}"`
```javascript
new rjs.Vector2(1, 3).toString() = "v1;3";
```

### Vector2.fromString(v)

- __v__ `<string>` - вектор в виде строки

Перевод вектора из строки в объект. Возвращает вектор в виде объекта.
```javascript
Vector2.fromString("v1;3") = new rjs.Vector2(1; 3);
```

### vec2([x, y])

Создание двухмерного вектора. Возвращает __new RectJS.Vector2(x, y)__.

### new RectJS.Camera(options)

- __options__ `<object>` - обязательный параметр!!!
	- __pos__ `<object>` (`<RectJS.Vector2` | `<RectJS.vec2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - позиция камеры на сцене
	- __id__ `<string>` __*Default:*__ `"camera_{номер камеры}"` - идентификатор камеры

Создание камеры. Возвращает объект камеры.

### Camera.set()

Переключение на кмеру.

### new RectJS.Layer(scene[ ,parallax[ ,scale[ ,id[ ,options]]]])

- __scene__ `<object>` (`RectJS.Scene`) - сцена слоя
- __paralalx__ `<object>` (`RectJS.Vector2`) __*Default:*__ `new RectJS.Vector2(100, 100)` - проценты параллакса слоя по осям виде вектора
- __scale__ `<object>` (`RectJS.Vector2`) __*Default:*__ `new RectJS.Vector2(1, 1)` - скейлинг слоя по осям виде вектора
- __id__ `<string>` __*Default:*__ `"layer_{номер слоя}"` - идентификатор слоя
- __options__ `<object>` __*Default:*__ `new Object()`
	- __visible__ `<boolean>` __*Default:*__ `true` - видимость слоя
