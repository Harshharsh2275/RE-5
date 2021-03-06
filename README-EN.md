# Introduction

__Rect Engine 5__ (RE-5) - is the object-oriented engine-framework made by Black Square Studios for 2D games development with JavaScript. Graphic engine in RE-5 is based on [WebGL2](https://webgl2fundamentals.org) (browser adaptation of [OpenGL3.0](https://www.opengl.org)). Engine is suitable for small and big multiplayer games development as well. Engine has a flexible plugin system that expands its functionality. More lessons and guides to RE-5 you can find following [this link](http://bss.epizy.com/page/?f=re5lessons).

# Setting up the project

- Install any local server or just use our small local [server on Node.js](https://github.com/BSS-Lord/local-server)
- Create project directory on the server
- Anpack this repository into that folder
- When you just open it in browser you sould see the tinged square rotating around and the caption "Rect Engine 5"

__WARNING!__ You can use any comfortable to you code editor, cause there's no native IDE for the engine yet.

# Project structure

- __Engine__ (engine files)
	- __Shaders__ (shaders)
		- __fragment-shader.glsl__ (fragment shader)
		- __vertex-shader.glsl__ (vertex shader)
	- __collision.js__ (collision detection)
	- __engine.js__ (engine logic, program interface)
	- __renderer.js__ (graphics engine shall)
	- __renderCore.js__ (graphics engine core)
	- __matrix.js__ (matrix maths)
	- __vert.js__ (object vertices)
- __Plugins__ (plugins)
- __Scene__ (scenes)
	- __new__ (scene files)
		- __end.js__ (runs when the scene ends)
		- __init.js__ (runs after the scene is initialized)
		- __start.js__ (runs every time when the scene starts)
- __Scripts__ (scripts)
	- __assets.js__ (for setting up assets)
	- __config.js__ (for setting up configurations and settings)
	- __families.js__ (for families initializing)
	- __sources.js__ (for source loading)
- __Sources__ (sources)
	- __audio__ (audio files)
	- __images__ (textures, tilemaps)
	- __json__ (JSON files)
	- __glsl__ (shaders)
- __index.html__ (runs engine.js and main.js)
- __main.js__ (engine initialization)

# What's the project consist of?

In the __*main.js*__ file there's the engine initializing, including all scripts from __*Scripts*__ falder, creating scenes, scripts from the __*Scenes/scene name*__ folder attaching to the scenes, switching to the certain scene.

In the __*config.js*__ script there's all project and engine settings.

In the __*families.js*__ script there's all families initializations

In the __*sources.js*__ script there's all needed sources loading (textures, sounds, fonts...)

In the __*assets.js*__ script there's all assets initializations.

You can add your own scripts in __*Scripts*__ folder or in the folders of the scenes and include it wherever and whenever you want.

In the every folder of the scene there's 3 files:
- __*init.js*__ - the script runs only at ones after the scene is initialized, there you have to create cameras, layers, most of the game objects, game loop for the scene and initialize all needed event listeners.
- __*start.js*__ - the script runs every single time when the scene starts, here the game switches to the necessary camera, the engine settings change, the level starts, for example enemy takes their places on the level.
- __*end.js*__ - the script runs every single time when the scene ends, game engine settings turns back to normal, the game progress could be saved.

# Methods and properties
## Content
### [Initialization](#initialization-1)
- [new RectJS()](#new-rectjscallback-sourcehost-enginesource-pluginsource-eventdetector)
- [require()](#requiresrc-type)
- [new RectJS.Scene()](#new-rectjssceneoptions)
- [Scene.set()](#scenesetstartparams-endparams)
- [Scene.update()](#sceneupdate)
### [Special methods](#специальные-функции-1)
- [new RectJS.Vector2()](#new-rectjsvector2x-y)
- [Vector2.toString()](#vector2tostring)
- [Vector2.fromString()](#vector2fromstringv)
- [vec2()](#vec2x-y)
- [rgb()](#rgbr-g-b)
- [rgba()](#rgbar-g-b-a)
- [colorRGB.toString()](#colorrgbtostring)
- [colorRGBA.toString()](#colorrgbatostring)
- [colorRGBA.toStringCSS()](#colorrgbatostringcss)
- [count()](#countobject)
- [copy()](#copyobject)
- [log()](#log)
- [RectJS.isObject()](#rectjsisobjectobject)
- [RectJS.checkSourceLoaded()](#rectjschecksourceloaded)
### [Cameras and layers](#камеры-и-слои-1)
- [new RectJS.Camera()](#new-rectjscameraoptions)
- [Camera.set()](#cameraset)
- [new RectJS.Layer()](#new-rectjslayerscene-parallax-scale-id-options)
### [Game objects](#игровые-объекты-1)
- [new RectJS.Polygon()](#new-rectjspolygonoptions)
- [new RectJS.Sprite()](#new-rectjsspriteoptions)
- [new RectJS.Text()](#new-rectjstextoptions)
- [Object.destroy()](#objectdestroy)
- [Object.setLayer()](#objectsetlayerlayer)
- [Object.getPoint()](#objectgetpointid)
- [Object.update()](#objectupdate)
### [Game loops](#циклы-1)
- [new RectJS.GameLoop()](#new-rectjsgameloopcallback-active-scene-absl)
- [Loop.start()](#loopstart)
- [Loop.stop()](#loopstop)
- [new RectJS.Interval()](#new-rectjsintervalcallback-timeout-active-scene)
- [new RectJS.Wait()](#new-rectjswaitcallback-delay-active-scene-absl)
### [Sources](#ресурсы-1)
- [new RectJS.Texture](#new-rectjstexturesrc-scale-custom_size)
- [new RectJS.Tiled()](#new-rectjstiledorigin-size)
- [new RectJS.Crop()](#new-rectjscroporigin-pos-size)
- [new RectJS.Animation()](#new-rectjsanimationoptions)
- [RectJS.loadFont()](#rectjsloadfontname-src)
- [new RectJS.Sound()](#new-rectjssoundsrc-distance)
- [Sound.play()](#soundplay)
- [Sound.stop()](#soundstop)
- [Sound.reset()](#soundreset)
- [Sound.restart()](#soundrestart)
- [Sound.getDuration()](#soundgetduration)
- [Sound.setTime()](#soundsettimetime)
- [Sound.getTime()](#soundgettime)
- [Sound.setVolume()](#soundsetvolumevolume)
- [Sound.getVolume()](#soundgetvolume)
- [Sound.bindObject](#soundbindobject)
- [Sound.unbindObject()](#soundunbindobject)
### [Shaders](#шейдеры-1)
- [new RectJS.Shader()](#new-rectjsshadertype-src-id)
- [new RectJS.Program()](#new-rectjsprogramoptions)
### [Vertex shader parameters](#параметры-вершинного-шейдера-1)
- [VS attribute vertex](#attribute-vec2-vertex)
- [VS attribute UV](#attribute-vec2-uv)
- [VS attribute matrix](#attribute-mat3-matrix)
- [VS attribute color](#attribute-vec4-color)
- [VS varying vColor](#varying-vec4-vcolor)
- [VS varying vUV](#varying-vec2-vuv)
- [VS uniform colorMode](#uniform-bool-colormode)
- [VS uniform uColor](#uniform-vec4-ucolor)
### [Fragment shader parameters](#параметры-фрагментного-шейдера-1)
- [FS uniform tex](#uniform-sampler2d-tex)
- [FS varying vColor](#varying-vec4-vcolor-1)
- [FS varying vUV](#varying-vec2-vuv-1)
### [Mouse and keyboard](#мышь-и-клавиатура-1)
- [new RectJS.Click()](#new-rectjsclickcallback-active-scene-target)
- [new RectJS.RightClick()](#new-rectjsrightclickcallback-active-scene-target)
- [new RectJS.MouseDown()](#new-rectjsmousedowncallback-active-scene-target)
- [new RectJS.MouseUp()](#new-rectjsmouseupcallback-active-scene-target)
- [new RectJS.MouseRightDown()](#new-rectjsmouserightdowncallback-active-scene-target)
- [new RectJS.MouseRightUp()](#new-rectjsmouserightupcallback-active-scene-target)
- [new RectJS.MouseWheelDown()](#new-rectjsmousewheeldowncallback-active-scene-target)
- [new RectJS.MouseWheelUp()](#new-rectjsmousewheelupcallback-active-scene-target)
- [new RectJS.MouseMove()](#new-rectjsmousemovecallback-active-scene-target)
- [new RectJS.Wheel()](#new-rectjswheelcallback-active-scene-target)
- [new RectJS.WheelUp()](#new-rectjswheelupcallback-active-scene-target)
- [new RectJS.WheelDown()](#new-rectjswheeldowncallback-active-scene-target)
- [new RectJS.MousePress()](#new-rectjsmousepresscallback-active-scene)
- [new RectJS.TouchStart()](#new-rectjstouchstartcallback-id-active-scene-target)
- [new RectJS.TouchEnd()](#new-rectjstouchendcallback-id-active-scene-target)
- [new RectJS.TouchMove()](#new-rectjstouchmovecallback-id-active-scene-target)
- [new RectJS.KeyDown()](#new-rectjskeydowncallback-key-active-scene-target)
- [new RectJS.KeyUp()](#new-rectjskeyupcallback-key-active-scene-target)
- [new RectJS.KeyPress()](#new-rectjskeypresscallback-key-active-scene)
- [Event.start()](#eventstart)
- [Event.stop()](#eventstop)
- [RectJS.KeyPressed()](#rectjskeypressedkey)
- [new RectJS.Mouse()](#new-rectjsmouse)
- [Mouse.get()](#mousegetlayer-scale-parallax)
- [new RectJS.Touch()](#new-rectjstouch)
- [Touch[index].get()](#touchindexgetlayer)
### [Families and assets](#семьи-и-ассеты-1)
- [new RectJS.Family()](#new-rectjsfamily)
- [Family.get()](#familygetid)
- [Family.getByIndex()](#familygetbyindexindex)
- [Family.isset()](#familyisseto)
- [Family.for()](#familyforcallback)
- [Family.forNearTo()](#familyforneartopos-callback-dist-chunk_mode-chunk_dist)
- [Family.count()](#familycount)
- [Family.add()](#familyaddobject)
- [Family.remove()](#familyremoveobject)
- [new RectJS.Asset()](#new-rectjsassetoptions)
- [new Asset()](#new-assetoptions)
### [Collision detection](#обработка-столкновений-1)
- [RectJS.Collision()](#rectjscollisiona-b)
- [RectJS.getBoundingBox()](#rectjsgetboundingboxobject-calc_angle)
- [RectJS.AABB()](#rectjsaabba-b)
- [RectJS.MouseOver()](#rectjsmouseoverobject)
### [Engine properties](#параметры-движка-1)
- [RectJS.sourceHOST](#rectjssourcehost)
- [RectJS.engineSource](#rectjsenginesource)
- [RectJS.pluginSource](#rectjspluginsource)
- [RectJS.container](#rectjscontainer)
- [RectJS.WebGL_Canvas](#rectjswebgl_canvas)
- [RectJS.ctx2D_Canvas](#rectjsctx2d_canvas)
- [RectJS.eventDetector](#rectjseventdetector)
- [RectJS.gl](#rectjsgl)
- [RectJS.ctx](#rectjsctx)
- [RectJS.client.w](#rectjsclientw)
- [RectJS.client.h](#rectjsclienth)
- [RectJS.canvas_width](#rectjscanvas_width)
- [RectJS.canvas_height](#rectjscanvas_height)
- [RectJS.con_width](#rectjscon_width)
- [RectJS.con_height](#rectjscon_height)
- [RectJS.CLEAR_COLOR](#rectjsclear_color)
- [RectJS.BG_COLOR](#rectjsbg_color)
- [RectJS.scenes](#rectjsscenes)
- [RectJS.currentScene](#rectjscurrentscene)
- [RectJS.layers](#rectjslayers)
- [RectJS.sources](#rectjssources)
- [RectJS.images](#rectjsimages)
- [RectJS.textures](#rectjstextures)
- [RectJS.LOADER_MODE](#rectjsloader_mode)
- [RectJS.sourceLoaded](#rectjssourceloaded)
- [RectJS.timeStep](#rectjstimestep)
- [RectJS.animations](#rectjsanimations)
- [RectJS.cameras](#rectjscameras)
- [RectJS.currentCamera](#rectjscurrentcamera)
- [RectJS.waits](#rectjswaits)
- [RectJS.gameLoops](#rectjsgameloops)
- [RectJS.CUT_FPS](#rectjscut_fps)
- [RectJS.MAX_FPS](#rectjsmax_fps)
- [RectJS.SFRM](#rectjssfrm)
- [RectJS.events](#rectjsevents)
- [RectJS.MousePressed](#rectjsmousepressed)
- [RectJS.RightMousePressed](#rectjsrightmousepressed)
- [RectJS.families](#rectjsfamilies)
- [RectJS.FPS](#rectjsfps)
- [RectJS.render](#rectjsrender)
- [RectJS.renderCore](#rectjsrendercore)
- [RectJS.renderer](#rectjsrenderer)
- [RectJS.renderer.ACTIVE](#rectjsrendereractive)
- [RectJS.renderer.DRAWING_MODE](#rectjsrendererdrawing_mode)
- [RectJS.renderer.DCPF](#rectjsrendererdcpf)
- [RectJS.renderer.DEBUG_MODE](#rectjsrendererdebug_mode)
- [RectJS.renderer.DEBUG_CONSOLE_MODE](#rectjsrendererdebug_console_mode)
### [Plugins](#плагины-1)
- [new RectJS.Plugin()](#new-rectjspluginname-params)



## Initialization

### new RectJS(callback[, sourceHOST[, engineSource[, pluginSource[, eventDetector]]]])

- __callback__ `<function>` - this function takes the game engine instance as an argument
- __sourceHOST__ `<string>` __*Default:*__ `""` - the realtive path from the __*index.html*__ to __*main.js*__, engine and project folders.
- __engineSource__ `<string>` __*Default:*__ `"Engine/"` - the path from the folder set up in __sourceHOST__ to the engine folder.
- __pluginSource__ `<string>` __*Default:*__ `"Plugins/"` - the path from the folder set up in __sourceHOST__ to the plugins folder.
- __eventDetector__ `<object>` __*Default:*__ `null` - DOM element on the page to which all mouse event listeners is bound. If equal `null`, it sets by default to __RectJS.eventDetector__.

Engine initialization

### require(src[, type])

- __src__ `<string>` - relative path to the file
- __type__ `<string>` __*Default:*__ `"JS"` - file type
	- __"JS"__ - JavaScript. The method returns an arrow function from the script.
	- __"JSON"__ - JSON file. The method returns JavaScript-object from the JSON file.
	- __"TEXT"__ - Simple text. The method returns a text from the file as a string.

__ВНИМАНИЕ!__ All available scripts actually are the arrow functions:
```javascript
(params) => {
	// code here
}
```
or the function taken in the brackets:
```javascript
(function (params) {
	// code here
})
```

__WARNING!__ If you want variable to be accessible form all of the scripts it need to be global. There's 3 ways to do that:
- declare the variable missing the keyword ('const', 'let' or 'var') (recommended)
`variable = 1;`
- declare the variable as a property of the __window__
`window.variable = 1;`
- declare the variable beyound the "onload" event listener in the __*main.js*__ script
```javascript
var variable = 1;

window.addEventListener('load', e => {
...
```

### new RectJS.Scene(options)

- __options__ `<object>`
	- __id__ `<string>` __*Default:*__ `"scene_{scene number}"` - scene indentifier
	- __init__ `<function>` __*Default:*__ `() => {}` - script runs after the scene is initialized, takes scene instance as an argument
	- __start__ `<function>` __*Default:*__ `() => {}` - script runs when the scene starts, takes scene instance and the start parameters as arguments.
	- __end__ `<function>` __*Default:*__ `() => {}` - script runs when the scene ends, takes scene instance and the end parameters as arguments.
	- __initOnload__ `<boolean>` __*Default:*__ `true`
		- __true__ - initialization script runs emmidiately after the scene is declared
		- __false__ - initialization script runs right before the first scene start
		
Scene initializer. Returns the scene instance.

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

## Специальные функции

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

### rgb(r, g, b)

- __r__ `<number>` - красный канал (0-255)
- __g__ `<number>` - зелёный канал (0-255)
- __b__ `<number>` - синий канал (0-255)

Создание цвета. Возвращает объект цвета.

### rgba(r, g, b[, a])

- __r__ `<number>` - красный канал (0-255)
- __g__ `<number>` - зелёный канал (0-255)
- __b__ `<number>` - синий канал (0-255)
- __a__ `<number>` __*Default:*__ `255` - альфа канал (0-255)

Создание цвета. Возвращает объект цвета.

### colorRGB.toString()
### colorRGBA.toString()

Возвращает цвет в виде строки.

```javascript
var color = rgb(255, 255, 255);
console.log(color.toString());
// получим в консоли "rgb(255, 255, 255)"
```

```javascript
var color = rgba(255, 255, 255, 255);
console.log(color.toString());
// получим в консоли "rgba(255, 255, 255, 255)"
```

### colorRGBA.toStringCSS()

Возвращает цвет в виде строки в формате CSS, где альфа канал в пределах от 0 до 1.

```javascript
var color = rgba(255, 255, 255, 255);
console.log(color.toStringCSS());
// получим в консоли "rgba(255, 255, 255, 1)"
```

### count(object)

- __object__ `<array> | <object>` - массив или объект

Возвращает количество запоненых ячеек в объекте или массиве в виде числа.

### copy(object)

- __object__ `<object>` - JavaScript-объект

Возвращает копию одномерного JavaScript-объекта (ассоциативного массива).

### log()

То же что и __console.log()__.

### RectJS.isObject(object)

- __object__ `<object>` - JavaScript-объект

Возвращает `true` если аргумент является игровым объектом.

### RectJS.checkSourceLoaded()

В режиме ожидания загрузки ресурсов `RectJS.LOADER_MODE` проверяет наличие незагруженых ресурсов. Если таковы имеются `RectJS.sourceLoaded` устанавливается на `false`, если нет - `true`.

## Камеры и слои

### new RectJS.Camera(options)

- __options__ `<object>` - обязательный параметр!!!
	- __pos__ `<object>` (`<RectJS.Vector2` | `<RectJS.vec2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - позиция камеры на сцене
	- __id__ `<string>` __*Default:*__ `"camera_{номер камеры}"` - идентификатор камеры

Создание камеры. Возвращает объект камеры.

### Camera.set()

Переключение на кмеру.

### new RectJS.Layer(scene[, parallax[, scale[, id[, options]]]])

- __scene__ `<object>` (`<RectJS.Scene>`) - сцена слоя
- __paralalx__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(100, 100)` - проценты параллакса слоя по осям виде вектора
- __scale__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(1, 1)` - скейлинг слоя по осям виде вектора
- __id__ `<string>` __*Default:*__ `"layer_{номер слоя}"` - идентификатор слоя
- __options__ `<object>` __*Default:*__ `new Object()`
	- __visible__ `<boolean>` __*Default:*__ `true` - видимость слоя
	
Создание слоя.
__ВНИМАНИЕ!__ Слои отрисовываются в порядке инициализации.

## Игровые объекты

### new RectJS.Polygon(options)

- __options__ `<object>`
	- __pos__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - позиция объекта на сцене в виде вектора
	- __vertices__ `<array>` [`<RectJS.Vector2>`, ...] __*Default:*__ `new Array()` - массив с вершинами многоугольника в виде векторов
	- __scale__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(1, 1)` - скейлинг объекта
	- __angle__ `<number>` __*Default:*__ `0` - поворот объекта в градусах
	- __origin__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - смещение центра обекта
	- __points__ `<array>` [`<RectJS.Vector2>`, ...] __*Default:*__ `new Array()` - точки привязки
	- __texture__ `<object>` (`RectJS.Texture`) __*Default:*__ `null` - текстура объекта
	- __color__ `<arrat>` (`<rgb> | <rgba>`) __*Default:*__ `rgb(255, 255, 255)` - цвет объекта
	- __colors__ `<array>` [`<rgb> | <rgba>`, ...] __*Default:*__ `[...this.color]` - массив с цветами вершин многоугольника в формате `rgb` или `rgba`. Работает только если __colorMode__ = `"VERTEX"`!
	- __colorMode__ `<string>` __*Default:*__ `SINGLE` - режим отрисовки цвета. Есть три режима:
		- `"SINGLE"` - объект полностью залит цветом. При этом наличие разноцветных объектов не влияет на производительность.
		- `"UNIFORM"` - применяется если у большого количества однотипных объектов одинаковый цвет, на больших масштабах повышает производительность.
		- `"VERTEX"` - работает как "SINGLE", но позволяет задать цвет каждой вершине (цвета задаются в свойстве __colors__)
	- __filters__ `<array>` [`<rgb> | <rgba>`, ...] __*Default:*__ `new Array()` - массив с фильтрами цвета объекта в формате `rgb` или `rgba`
	- __opacity__ `<number>` __*Default:*__ `100` - проценты непрозрачности объекта
	- __render__ `<boolean>` __*Default:*__ `true` - видимость объекта
	- __enable_chunks__ `<boolean>` __*Default:*__ `true` - привязка объекта к чанку в чанковом режиме
	- __layer__ `<object>` (`<RectJS.Layer>`) - слой объекта
	- __id__ `<string>` __*Default:*__ `"object_{номер объекта}"` - индентификатор объекта
	- __textOverlap__ `<boolean>` __*Default:*__ `false` - перекрыте текстов объектом
	- __families__ `<array>` [`<RectJS.Family>`, ...] __*Default:*__ `new Array()` - семьи к которым принадлежит объект
	- __program__ `<object>` (`<RectJS.Program>`) __*Default:*__ `rjs.renderer.programs["DEFAULT"]` - шейдерная программа (большое их количество понижает производительность)
	- __private__ `<object>` __*Default:*__ `new Object()` - объект с дополнительными параметрами объекта и методами.
		- __init__ `<function>` __*Default:*__ `undefined` - срабатывает после создания объекта

Создание многоугольника. Возвращает игровой объект.

```javascript
var object = new rjs.Polygon({
	...
	private: {
		test: 123,
		init: function () {
			console.log(this.text);
			// в консоли получим "123"
		}
	}
});

console.log(object.test);
// в консоли получим "123"
```

Ко всем параметрам объекта кроме __private__ можно обратиться как к его свойствам. Те же что были в свойстве __private__ становятся свойствами и методаим самого объекта (как показано выше).

### new RectJS.Sprite(options)

- __options__ `<object>`
	- __pos__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - позиция объекта на сцене в виде вектора
	- __size__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - размеры спрайта
	- __scale__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(1, 1)` - скейлинг объекта
	- __angle__ `<number>` __*Default:*__ `0` - поворот объекта в градусах
	- __origin__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - смещение центра обекта
	- __points__ `<array>` [`<RectJS.Vector2>`, ...] __*Default:*__ `new Array()` - точки привязки
	- __texture__ `<object>` (`RectJS.Texture`) __*Default:*__ `null` - текстура объекта
	- __color__ `<object>` (`<rgb> | <rgba>`) __*Default:*__ `rgb(255, 255, 255)` - цвет объекта
	- __colors__ `<array>` [`<rgb> | <rgba>`, ...] __*Default:*__ `[...this.color]` - массив с цветами вершин многоугольника в формате `rgb` или `rgba`. Работает только если __colorMode__ = `"VERTEX"`!
	- __colorMode__ `<string>` __*Default:*__ `SINGLE` - режим отрисовки цвета. Есть три режима:
		- `"SINGLE"` - объект полностью залит цветом. При этом наличие разноцветных объектов не влияет на производительность.
		- `"UNIFORM"` - применяется если у большого количества однотипных объектов одинаковый цвет, на больших масштабах повышает производительность.
		- `"VERTEX"` - работает как "SINGLE", но позволяет задать цвет каждой вершине (цвета задаются в свойстве __colors__)
	- __filters__ `<array>` [`<rgb> | <rgba>`, ...] __*Default:*__ `new Array()` - массив с фильтрами цвета объекта в формате `rgb`
	- __opacity__ `<number>` __*Default:*__ `100` - проценты непрозрачности объекта
	- __render__ `<boolean>` __*Default:*__ `true` - видимость объекта
	- __enable_chunks__ `<boolean>` __*Default:*__ `true` - привязка объекта к чанку в чанковом режиме
	- __layer__ `<object>` (`<RectJS.Layer>`) - слой объекта
	- __id__ `<string>` __*Default:*__ `"object_{номер объекта}"` - индентификатор объекта
	- __textOverlap__ `<boolean>` __*Default:*__ `false` - перекрыте текстов объектом
	- __families__ `<array>` [`<RectJS.Family>`, ...] __*Default:*__ `new Array()` - семьи к которым принадлежит объект
	- __program__ `<object>` (`<RectJS.Program>`) __*Default:*__ `rjs.renderer.programs["DEFAULT"]` - шейдерная программа (большое их количество понижает производительность)
	- __private__ `<object>` __*Default:*__ `new Object()` - объект с дополнительными параметрами объекта и методами.
		- __init__ `<function>` __*Default:*__ `undefined` - срабатывает после создания объекта
		
Создание прямоугольного объекта. Возвращает игровой объект.

### new RectJS.Text(options)

- __options__ `<object>`
	- __pos__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - позиция объекта на сцене в виде вектора
	- __size__ `<number>` - размер текста
	- __font__ `<string>` - шрифт текста
	- __text__ `<string>` - текст
	- __scale__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(1, 1)` - скейлинг объекта
	- __angle__ `<number>` __*Default:*__ `0` - поворот объекта в градусах
	- __origin__ `<string>` __*Default:*__ `"center-middle"` - выравнивание текста
	- __points__ `<array>` [`<RectJS.Vector2>`, ...] __*Default:*__ `new Array()` - точки привязки
	- __color__ `<object>` (`<rgb> | <rgba>`) __*Default:*__ `rgb(255, 255, 255)` - цвет текста
	- __filters__ `<array>` [`<rgb> | <rgba>`, ...] __*Default:*__ `new Array()` - массив с фильтрами цвета текста в формате `rgb` или `rgba`
	- __opacity__ `<number>` __*Default:*__ `100` - проценты непрозрачности объекта
	- __render__ `<boolean>` __*Default:*__ `true` - видимость объекта
	- __enable_chunks__ `<boolean>` __*Default:*__ `true` - привязка объекта к чанку в чанковом режиме
	- __layer__ `<object>` (`<RectJS.Layer>`) - слой объекта
	- __id__ `<string>` __*Default:*__ `"object_{номер объекта}"` - индентификатор объекта
	- __families__ `<array>` [`<RectJS.Family>`, ...] __*Default:*__ `new Array()` - семьи к которым принадлежит объект
	- __private__ `<object>` __*Default:*__ `new Object()` - объект с дополнительными параметрами объекта и методами.
		- __init__ `<function>` __*Default:*__ `undefined` - срабатывает после создания объекта
		
Создание текста. Возвращает игровой объект.

### Object.destroy()

Удаление объекта.

### Object.setLayer(layer)

- __layer__ `<object>` (`<RectJS.Layer>`) - новый слой объекта

Перенос объекта на другой слой.

### Object.getPoint(id)

- __id__ `<number>` - индекс точки в массиве `Object.points`

Возвращает координаты привязаной к объекту точки в виде вектора (с учётом его смещения, угла наклона и прочего).

### Object.update()

Обновляет объект. Применяется в случае изменения позиций вершин многоугольника, изменения слоя через свойство __layer__ или изменение текстуры.

## Циклы

### new RectJS.GameLoop(callback[, active[, scene[, absl]]])

- __callback__ `<function>` - функция цикла
- __active__ `<boolean>` __*Default:*__ `true` - состояние цикла
- __scene__ `<object>` (`<RectJS.Scene>`) __*Default:*__ `null` - сцена на которой работает цикл. Если = `null` - цикл работает на всех сценах
- __absl__ `<boolean>` __*Default:*__ `false` - работа цикла в режиме ожидания загрузки ресурсов

Создание игрового цикла. Возвращает объект цикла. `Loop.callback` срабатывает перед отрисовкой каждого кадра (если цикл включён)

### Loop.start()

Запуск цикла

### Loop.stop()

Остановка цикла. Выполняется синхронно перед отрисовкой каждого кадра.

### new RectJS.Interval(callback, timeout[, active[, scene]])

- __callback__ `<function>` - функция цикла
- __timeout__ `<number>` - период цикла в милисекундах
- __active__ `<boolean>` __*Default:*__ `true` - состояние цикла
- __scene__ `<object>` (`<RectJS.Scene>`) __*Default:*__ `null` - сцена на которой работает цикл. Если = `null` - цикл работает на всех сценах

Создание цикла с заданной периодичностью. Выполняется асинхронно.

### new RectJS.Wait(callback[, delay[, active[, scene[, absl]]]])

- __callback__ `<function>` - функция что выполнится после окончания задержки
- __delay__ `<number>` __*Default:*__ `0` - количество тиков задержки
- __active__ `<boolean>` __*Default:*__ `true` - маркер активности задержки
- __scene__ `<object>` (`<RectJS.Scene>`) __*Default:*__ `null` - сцена на которой работает задержка. Если = `null` - задержка работает на всех сценах
- __absl__ `<boolean>` __*Default:*__ `false` - работа задержки в режиме ожидания загрузки ресурсов

Создание задержки на определённое количество тиков. Выполняется синхронно после выполнения всех циклов и перед отрисовкой кадра.

## Ресурсы

### new RectJS.Texture(src[, scale[, custom_size]])

- __src__ `<string>` - относительный путь к файлу изображения
- __scale__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(1, 1)` - скейлинг исходной текстуры, влияет на разрешение текстуры
- __custom_size__ `<object>` (`<RectJS.Vector2>`) __*Default:*__ `new RectJS.Vector2(0, 0)` - размер исходной текстуры в пикселях, влияет на разрешение текстуры. Если равен нулю - размер подстроится под размер загруженого изображения

Загрузка текстуры. Возвращает объект текстуры.

### new RectJS.Tiled(origin, size)

- __origin__ `<object>` (`RectJS.Texture`) - исходное изображение
- __size__ `<object>` (`<RectJS.Vector2>`) - размер одного тайла на сцене

Создание зацикленного изображения из тайлов заданных размеров. Возвращает объект текстуры.

### new RectJS.Crop(origin, pos, size)

- __origin__ `<object>` (`RectJS.Texture`) - исходное изображение
- __pos__ `<object>` (`<RectJS.Vector2>`) - начальная позиция обрезания текстуры (левый верхний угол)
- __size__ `<object>` (`<RectJS.Vector2>`) - размер обрезоной текстуры в пикселях

Обрезка текстуры, например тайла из тайлмапа. Возвращает объект текстуры.

### new RectJS.Animation(options)

- __options__ `<object>`
	- __frames__ `<array>` [`<RectJS.Texture>`, ...] __*Default:*__ `new Array()` - массив с текстурами кадров анимации
	- __speed__ `<number>` __*Default:*__ `60` - количество кадров на 60 кадров отрисовки
	- __id__ `<string>` __*Default*__ `"animation_{номер анимации}"` -идентификатор анимации
	
Создание анимации. Возвращает объект анимации.

За текущий кадр конкретной анимации отвечает её свойство `.currentIndex`, изменяя его вы можете устанавливать кадр анимации.
За скорость отрисовкм отвечает свойство `.speed`, изменяя его вы можете останавливать анимацию, менять скорость, запускать её.

__ВНИМАНИЕ!__ Анимации в RE-5 ещё не доработаны. Все объекты с одной анимацией будут анимироваться синхронно.

### RectJS.loadFont(name, src)

- __name__ `<string>` - уникальное имя шрифта
- __src__ `<string>` - путь к фалу шрифта

Загрузка шрифта. Возвращает уникальное имя шрифта в виде строки.

### new RectJS.Sound(src[, distance])

- __src__ `<string>` - путь к аудиофайлу
- __distance__ `<number>` __*Default*__ `100` - коеффициент громкости привязанного к объекту звука

Загрузка музыки. Возвращает объект звука.

### Sound.play()

Проигрывание звука. Если звук был остановлен он продолжит проигрываться с того же места.

### Sound.stop()

Остановка проигрывания звука.

### Sound.reset()

Останавливает проигрывание и сбрасывает время.

### Sound.restart()

Перезапускает звук сначала.

### Sound.getDuration()

Возвращает продолжительность звука в виде числа.

### Sound.setTime(time)

- __time__ `<number>` - время

Устанавливает время проигрывания.

### Sound.getTime()

Возвращает время проигрывания в виде числа.

### Sound.setVolume(volume)

- __volume__ `<number>` - громкость в процентах (0-100)

Устанавливает громкость звука.

### Sound.getVolume()

Возвращает громкость звука в процентах в виде числа.

### Sound.bind(object)

- __object__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект

Привязывает звук к объекту.

### Sound.unbind(object)

- __object__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект

Отвязывает звук от объекта.

## Шейдеры

### new RectJS.Shader(type, src, id)

- __type__ `<string>` - тип шейдера
	`"VERTEX"` - вершинный шейдер
	`"FRAGMENT"` - фрагментный шейдер
- __src__ `<string>` - путь к файлу
- __id__ `<string>` - идентификаторю !!!Нельзя использовать идентификатор `"DEFAULT"`!!!!

Загружает и компилирует шейдер нужного типа.

### new RectJS.Program(options)

- __options__ `<object>` - набор параметров
	- __vertex__ `<object> | <string>` (`<RectJS.Shader> | <RectJS.Shader.id>`) - вершинный шейдер, чтобы добавить в программу стандартный шейдер задайте значение `"DEFAULT"`
	- __fragment__ `<object> | <string>` (`<RectJS.Shader> | <RectJS.Shader.id>`) - фрагментный шейдер, чтобы добавить в программу стандартный шейдер задайте значение `"DEFAULT"`
	- __id__ `<string>` - идентификатор программы. Чтобы сделать программу стандартной при отрисовке всех объектов задайте значение `"DEFAULT"`

Создаёт кастомную шейдерную программу

Шейдеры в RE-5 работают на языке программирования GLSL

## Параметры вершинного шейдера

### attribute vec2 vertex
Принимает координаты вершины
### attribute vec2 UV
Принимает текстурные координаты вершины
### attribute mat3 matrix
Принимает матрицу трансформаций
### attribute vec4 color
Принимает цветовой фильтр если __RectJS.Object.colorMode__ = `"SINGLE" | "VERTEX"`
### uniform bool colorMode
Если __RectJS.Object.colorMode__ = `"UNIFORM"` - принимает `true`, иначе - `false`
### uniform vec4 uColor
Принимает цветовой фильтр если __RectJS.Object.colorMode__ = `"UNIFORM"`
### varying vec4 vColor
Передаёт нужный фильтр цвета в фрагментный шейдер
### varying vec2 vUV
Передаёт текстурные координаты вершины в фрагментный шейдер

## Параметры фрагментного шейдера

### uniform sampler2D tex
Принимает текстуру
### varying vec4 vColor
Принимает цветовой фильтр
### varying vec2 vUV
Принимает текстурные координаты

## Мышь и клавиатура

### new RectJS.Click(callback[, active[, scene[, target]]])
Событие клика левой кнопой мишы
### new RectJS.RightClick(callback[, active[, scene[, target]]])
Событие клика правой кнопкой мишы
### new RectJS.MouseDown(callback[, active[, scene[, target]]])
Событие зажатия левой кнопки мыши
### new RectJS.MouseUp(callback[, active[, scene[, target]]])
Событие отпускания левой кнопки мыши
### new RectJS.MouseRightDown(callback[, active[, scene[, target]]])
Событие зажатия правой кнопки мыши
### new RectJS.MouseRightUp(callback[, active[, scene[, target]]])
Событие отпускания правой кнопки мыши
### new RectJS.MouseWheelDown(callback[, active[, scene[, target]]])
Событие зажатия колёсика мыши
### new RectJS.MouseWheelUp(callback[, active[, scene[, target]]])
Событие отпускания колёсика мыши
### new RectJS.MouseMove(callback[, active[, scene[, target]]])
Событие движения мыши
### new RectJS.Wheel(callback[, active[, scene[, target]]])
Событие прокручивания колёсика мыши
### new RectJS.WheelUp(callback[, active[, scene[, target]]])
Событие прокручивания колёсика мыши вверх
### new RectJS.WheelDown(callback[, active[, scene[, target]]])
Событие прокручивания колёсика мыши вниз

- __callback__ `<function>` - функция обработчик события, принимает  объект __event__ в качестве аргумента
- __active__ `<boolean>` __*Defaut:*__ `true` - состояние оработчика события
- __scene__ `<object>` (`<RectJS.Scene>`) __*Defaut:*__ `null` - сцена на которой обработчик события работает. Если = `null` - обработчик работает на всех сценах.
- __target__ `<DOM>` __*Defaut:*__ `RectJS.eventDetector` - DOM-элеммент, к которому привязан обработчик события

### new RectJS.MousePress(callback[, active[, scene]])
Событие удерживания левой кнопки мыши в зажатом положении.

- __callback__ `<function>` - функция обработчик события, принимает  объект __event__ в качестве аргумента
- __active__ `<boolean>` __*Defaut:*__ `true` - состояние оработчика события
- __scene__ `<object>` (`<RectJS.Scene>`) __*Defaut:*__ `null` - сцена на которой обработчик события работает. Если = `null` - обработчик работает на всех сценах.

### new RectJS.TouchStart(callback[, id[, active[, scene[, target]]]])
Событие начала нажатия
### new RectJS.TouchEnd(callback[, id[, active[, scene[, target]]]])
Событие окончания нажатия
### new RectJS.TouchMove(callback[, id[, active[, scene[, target]]]])
Событие движения нажатия

- __callback__ `<function>` - функция обработчик события, принимает  объект __event__ в качестве аргумента
- __id__ `<number>` __*Defaut:*__ `null` - индекс нажатия. Если = `null` - обработчик реагирует на все нажатия
- __active__ `<boolean>` __*Defaut:*__ `true` - состояние оработчика события
- __scene__ `<object>` (`<RectJS.Scene>`) __*Defaut:*__ `null` - сцена на которой обработчик события работает
- __target__ `<DOM>` __*Defaut:*__ `RectJS.eventDetector` - DOM-элеммент, к которому привязан обработчик события

### new RectJS.KeyDown(callback[, key[, active[, scene[, target]]]])
Событие зажатия клашвиши на клавиатуры
### new RectJS.KeyUp(callback[, key[, active[, scene[, target]]]])
Событие отпускания клашвиши на клавиатуры

- __callback__ `<function>` - функция обработчик события, принимает  объект __event__ в качестве аргумента
- __key__ `<number>` __*Defaut:*__ `null` - `event.keyCode` клавиши. Если = `null` - обработчик реагирует на все клавиши
- __active__ `<boolean>` __*Defaut:*__ `true` - состояние оработчика события
- __scene__ `<object>` (`<RectJS.Scene>`) __*Defaut:*__ `null` - сцена на которой обработчик события работает
- __target__ `<DOM>` __*Defaut:*__ `RectJS.eventDetector` - DOM-элеммент, к которому привязан обработчик события

### new RectJS.KeyPress(callback[, key[, active[, scene]]])
Событие удерживания клавиши на клавиатуре в зажатом положении

- __callback__ `<function>` - функция обработчик события, принимает  объект __event__ в качестве аргумента
- __key__ `<number>` __*Defaut:*__ `null` - `event.keyCode` клавиши. Если = `null` - обработчик реагирует на все клавиши
- __active__ `<boolean>` __*Defaut:*__ `true` - состояние оработчика события
- __scene__ `<object>` (`<RectJS.Scene>`) __*Defaut:*__ `null` - сцена на которой обработчик события работает. Если = `null` - обработчик работает на всех сценах.

__ВНИМАНИЕ!__ Все вышеуказанные события при создании вовзращают объект типа `RectJS.Event`.

Свойства `RectJS.Event`:
- __fnc__ `<function>` - __callback__ обработчика
- __active__ `<boolean>` - состояние оработчика события
- __scene__ `<object>` (`<RectJS.Scene>`) - сцена на которой обработчик события работает. Если = `null` - обработчик работает на всех сценах
- __event__ `<eventListener>` - слушатель события

### Event.start()

Запуск обработчика.

### Event.stop()

Остановка обработчика.

### RectJS.KeyPressed(key)

- __key__ `<number>` __*Defaut:*__ `null` - `event.keyCode` клавиши. Если = `null` - метод реагирует на все клавиши

Возвращает `true` если заданая клавиша на клавиатуре зажата.

### new RectJS.Mouse()

Возвращает объект мыши.

Свойства `RectJS.Mouse`:
- __x__ `<number>` - горизонтальная позиция на экране
- __y__ `<number>` - вертикальная позиция на экране

### Mouse.get(layer[, scale[, parallax]])

- __layer__ `<obejct>` (`<RectJS.Layer>`) - слой
- __scale__ `<object>` (`<RectJS.Vector2>`) __*Defaut:*__ `layer.scale` - скейлинг
- __parallax__ `<object>` (`<RectJS.Vector2>`) __*Defaut:*__ `layer.parallax` - параллакс в процентах (0-100)

Возвращает позицию мыши на сцене в виде вектора (с учётом смещения камеры, скейлинга слоя и параллакса).

### new RectJS.Touch();
Возвращает объект массив с касаниями.

Свойства каждого касания `(RectJS.Touch)[index]`:
- __x__ `<number>` - горизонтальная позиция на экране
- __y__ `<number>` - вертикальная позиция на экране

### Touch[index].get(layer)

- __layer__ `<obejct>` (`<RectJS.Layer>`) - слой

Возвращает точку касания на сцене в виде вектора (с учётом смещения камеры, скейлинга слоя и параллакса).

__ВНИМАНИЕ!__ Система событий в RE-5 немного недоработана, некоторые вещи могут работать некорректно.

## Семьи и ассеты

### new RectJS.Family()

Создание семьи объектов. Возвращает объект семьи.

### Family.get(id)

- __id__ `<string>` - идентификатор объекта

Возвращает объект из семьи.

### Family.getByIndex(index)

- __index__ `<number>` - номер объекта в семье (в порядке добавления объектов)

Возвращает объект из семьи.

### Family.isset(o)

- __o__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект 

Проверяет наличие объекта в семье.

### Family.for(callback)

- __callback__ `<function>` - функция, что принимает объект в качестве аргумента

Выполняет функцию для всех объектов семьи.

### Family.forNearTo(pos, callback[, dist])

- __pos__ `<object>` (`<RectJS.Vector2>`) - координаты точки
- __callback__ `<function>` - функция, что принимает объект в качестве аргумента
- __dist__ `<number>` __*Default:*__ `100` - максимальное расстояние от точки

Выполняет функцию для всех объектов семьи возле заданной точки.

### Family.count()

Возвращает количество объектов в семье.

### Family.add(object)

- __object__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект

Добавляет объект в семью.

### Family.remove(object)

- __object__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект

Удаляет объект из семьи.

### new RectJS.Asset(options)

- __options__ `<obejct>` - набор параметров объекта
	- __type__ `<string>` - тип объекта
		- `"Polyg"` - многоугольник
		- `"Sprite"` - спрайт
		- `"Text"` - текст
	- __остальные параметры как при создании объектов соответствующих типов__

Возвращает конструктор объекта с задаными свойствами:

### new Asset(options)

- __options__ `<object>` - набор свойств как при обычном создании объекта

__ВНИМАНИЕ!__ Свойства указанные при создании экземпляра записываются поверх свойств указаных в ассете.
__ВНИМАНИЕ!__ При указании цветов и векторов в ассете в экземпляр записываются только ссылки на них, так что изменяя цвет одного объекта вы измените цвет всех остальных.

Пример создания ассета

```javascript
// создаём ассет
const BOX = new rjs.Asset({
	type: "Sprite",
	size: vec2(256, 256),
	color: rgb(100, 50, 255),
	private: {
		init: function () {
			// объект наклонится на (0-90) после создания
			this.angle = Math.random()*90;
		},
		name: "John"
	}
});

// создаём первый объект
const box1 = new BOX({
	pos: vec2(0, 0),
	layer: new_main
});

// создаём второй объект
const box2 = new BOX({
	pos: vec2(500, 0),
	layer: new_main,
	private: {
		// указываем другое имя
		name: "Jack"
	}
});

// изменяем ширину второго объекта
box2.size.x = 128;

log(box1.name);
// получим "John" (как указано в ассете)

log(box2.name);
// получим "Jack" (как указано при создании объекта)

log(box1.size.x);
// вместо 256, как было изначально, мы получим 128,
// ведь мы изменили объект вектора на который ссылались оба объекта

log(box2.size.x);
// получим 128

```

## Обработка столкновений

### RectJS.Collision(a, b)

- __a__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект
- __b__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект

Возвращает `false` если объекты не пересекаются и объект с параметрами пересечения если пересекаются.

### RectJS.getBoundingBox(object[, calc_angle])

- __object__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект
- __calc_angle__ `<boolean>` __*Default:*__ `true` - учёт поворота объекта

Возвращает упрощённый bounding box в виде объекта с учётом наклона или без.

### RectJS.AABB(a, b)

- __a__ `<object>` (`RectJS.getBoundingBox`) - первый bounding box
- __b__ `<object>` (`RectJS.getBoundingBox`) - второй bounding box

Возвращает `true` если bounding box'ы пересекаются.

### RectJS.MouseOver(object)

- __object__ `<object>` (`<RectJS.Polygon> | <RectJS.Sprite> | <RectJS.Text>`) - игровой объект

Возвращает `true` если курсор мыши касается объекта.

# Параметры движка

### RectJS.sourceHOST
`<string>` __*Default:*__ `""` - Относительный путь от файла __*index.html*__ к файлу __*main.js*__, папкам движка и проекта

### RectJS.engineSource
`<string>` __*Default:*__ `"Engine/"` - путь из установленной в __RectJS.sourceHOST__ папки к папке движка

### RectJS.pluginSource
`<string>` __*Default:*__ `"Plugins/"` - путь из установленной в __RectJS.sourceHOST__ папки к папке с плагинами

### RectJS.container
`<DOM>` - div, хранящий все елементы для отрисовки и прослушивания событий

### RectJS.WebGL_Canvas
`<DOM>` - canvas где отрисовываются все игровые объекты

### RectJS.ctx2D_Canvas
`<DOM>` - canvas где отрисовываются все тексты

### RectJS.eventDetector
`<DOM>` - div, что находится поверх canvas'ов и прослушивает события мыш

### RectJS.gl
`<object>` - WebGL2RenderingContext

### RectJS.ctx
`<object>` - CanvasRenderingContext2D

### RectJS.client.w
`<number>` __*Default:*__ `1920` - ширина области отрисовки в условных единицах, что используются для позиционирования и указания размеров объектов

### RectJS.client.h
`<number>` __*Default:*__ `1080` - высота области отрисовки в условных единицах, что используются для позиционирования и указания размеров объектов

### RectJS.canvas_width
`<number>` - текущая ширина canvas'а

### RectJS.canvas_height
`<number>` - текущая высота canvas'а

### RectJS.con_width
`<number>` - текущая ширина контейнера

### RectJS.con_height
`<number>` - текущая высота контейнера

### RectJS.CLEAR_COLOR
`<object>` (`<rgba>`) - цвет заднего фона области отрисовки

### RectJS.BG_COLOR
`<object>` (`<rgba>`) - цвет заднего страници

### RectJS.scenes
`<object>` - объект, хранящий все сцены

### RectJS.currentScene
`<object>` (`<RectJS.Scene>`) - текущая сцена

### RectJS.layers
`<object>` - объект, хранящий все слои всех сцен

### RectJS.sources
`<object>` - объект, хранящий все загруженные ресурсы (кроме шрифтов)

### RectJS.images
`<object>` - объект, хранящий все первичные текстуры

### RectJS.textures
`<object>` - объект, хранящий все первичные и вторичные текстуры (созданные путём обрезания или закливания первичных), а также анимации

### RectJS.LOADER_MODE
`<boolean>` __*Default:*__ `false` - режим ожидания загрузки ресурсов

### RectJS.sourceLoaded
`<boolean>` - отсутствие незагружённых ресурсов

### RectJS.timeStep
 `<number>` (`<integer>`) __*Default:*__ `1` - целое число тиков на 1 вызов requestAnimationFrame()
 
### RectJS.animations
`<object>` - объект, хранящий все анимации

### RectJS.cameras
`<object>` - объект, хранящий все камеры

### RectJS.currentCamera
`<object>` (`<RectJS.camera>`) - текущая камера

### RectJS.waits
`<array>` - массив, хранящий все задержки

### RectJS.gameLoops
`<array>` - массив, хранящий все игровые циклы

### RectJS.CUT_FPS
`<boolean>` __*Default:*__ `false` - ограничение FPS (не рекомендуется)

### RectJS.MAX_FPS
`<number>` (`<integer>`) __*Default:*__ `60` - максимальный FPS

### RectJS.SFRM
**S**ingle **F**rame **R**eqest **M**ode
`<boolean>` __*Default:*__ `true` - режим единичного запроса на отрисовку кадра. Если его отключить рендеринг будет вызываться отдельным от перезапуска глобального игрового цикла вызовом requestAnimationFrame(). В редких случаях его отключение повышает оптимизацию, в остальных же - понижает.

### RectJS.events
`<array>` - массив, хранящий все события мыши, клавиатуры и нажатий

### RectJS.MousePressed
`<boolean>` - указатель нажата ли кнопка мыши

### RectJS.RightMousePressed
`<boolean>` - указатель нажата ли правая кнопка мыши

### RectJS.families
`<array>` - массив, хранящий все семьи

### RectJS.sounds
`<array>` - массив, хранящий все звуки

### RectJS.FPS
`<number>` - текущий FPS

### RectJS.render
`<function>` - функция отрисовки

### RectJS.renderCore
`<object>` - объект, хранящий методы и свойства отрисовки графики

Для совместимости с устаревшими плагинами есть альтернативная ссылка: __RectJS.renderTools__

### RectJS.renderer
`<object>` - интерфейс системы рендеринга

### RectJS.renderer.DRAWING_MODE
`<string>` __*Default:*__ `"mipmap"` - режим отрисовки текстур

- `mipmap` - сглаженое отображение (более ресурсозатратно)
- `linear` - билинейная интерполяция (рекомендовано для оптимизации)
- `pixel` - отсутствие интерполяции (для игр с пиксельартом)

### RectJS.renderer.DCPF
**D**raw **C**all **P**er **F**rame
`<number>` - текущее количество вызовов отрисовки на кадр

### RectJS.renderer.DEBUG_MODE
`<boolean>` __*Default:*__ `false` - режим отладки рендеринга. Позволяет увидеть как проходит рендеринг поэтапно, чтобы оптимиировать игру

### RectJS.renderer.DEBUG_CONSOLE_MODE
`<boolean>` __*Default:*__ `"false` - режим переключения кадров через консоль

# Плагины

## Устройство плагина

Для корректной работы плагин должен находиться в папке __*Plugins/*__*назание_плагина*__*.rjs*__. Плагин состоит из 2 файлов:

- __*package.json*__ - JSON-файл с настройками плагина и информацией о нём.
```JSON
{
	"name": "название_плагина",
	"version": "1.0.0",
	"main": "plugin.js",
	"settings": {
		
	}
}
```
- __*plugin.js*__ - код плагина.
```javascript
(plugin) => {

	
	const exports = plugin.exports = {}; // интерфейс плагина
	const rjs = plugin.engine; // ссылка на движок
	const pack = plugin.pack; // объект загруженный из package.json
	const sets = plugin.pack.settings; // настройки плагина
	const params = plugin.params; // параметры подключения плагина
	const global = plugin.global; // свойства этого объекта после инициализации плагина станут глобальными
	const code = plugin.code; // функция из файла plugin.js
	
	// здесь выполняется код плагина

}
```

## Подключение

### new RectJS.Plugin(name[, ...params])

- __name__ `<string>` - название плагина указанное в файле __*package.json*__
- __...params__ - параметры подключения плагина. Описано в документации плагина.

Подключение плагина. Возвращает объект `plugin.exports`.

__ВНИМАНИЕ!__ Если в документации плагина не указано противного плагин подключается в __callback__ функции инициализации движка.

Вы можете самостоятельно создавать плагины или скачать их на [нашем сайте](http://bss.epizy.com/page/?f=re5plugins).
Чтобы поделиться своими наработками или сообщить о проблеме присоединяйтесь к [нашему сообществу в Discord](https://discord.gg/KAEt7uRFVH).

*© Black Square Studios*
