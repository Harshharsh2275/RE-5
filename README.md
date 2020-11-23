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

`#### new RectJS(callback);`

- __callback__ `<function>` - принимает объект экземпляра движка перед его инициализацией.

Инициализация движка


