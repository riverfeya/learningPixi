Обучение Pixi
=============

Пошаговое введение в создание игр и интерактивных медиа с
в [движком рендеринга Pixi](https://github.com/pixijs/pixi.js). **[Обновлено для Pixi v4.5.5](https://github.com/pixijs/pixi.js/releases/tag/v4.5.5)**. . Если тебе это нравится
руководство, [вам понравится книга, в которой на 80% больше контента!](http://www.springer.com/us/book/9781484210956).

### Оглавление
- [Обучение Pixi](#обучение-pixi)
    - [Оглавление](#оглавление)
  - [Вступление](#вступление)
  - [Настройка](#настройка)
    - [Установка Pixi](#установка-pixi)
  - [Создание приложения Pixi и `stage`](#создание-приложения-pixi-и-stage)
  - [Pixi спрайты](#pixi-спрайты)
  - [Загрузка изображений в кеш текстур](#загрузка-изображений-в-кеш-текстур)
  - [Отображение спрайтов](#отображение-спрайтов)
    - [Использование псевдонимов](#использование-псевдонимов)
    - [Еще немного о загрузке вещей](#еще-немного-о-загрузке-вещей)
      - [Создайте спрайт из обычного объекта изображения JavaScript или холста](#создайте-спрайт-из-обычного-объекта-изображения-javascript-или-холста)
      - [Присвоение имени загружаемому файлу](#присвоение-имени-загружаемому-файлу)
      - [Мониторинг прогресса загрузки](#мониторинг-прогресса-загрузки)
      - [Подробнее о загрузчике Pixi](#подробнее-о-загрузчике-pixi)
  - [Размещение спрайтов](#размещение-спрайтов)
  - [Размер и масштаб](#размер-и-масштаб)
  - [Rotation](#rotation)
  - [Make a sprite from a tileset sub-image](#make-a-sprite-from-a-tileset-sub-image)
  - [Using a texture atlas](#using-a-texture-atlas)
  - [Loading the texture atlas](#loading-the-texture-atlas)
  - [Creating sprites from a loaded texture atlas](#creating-sprites-from-a-loaded-texture-atlas)
  - [Moving Sprites](#moving-sprites)
  - [Using velocity properties](#using-velocity-properties)
  - [Game states](#game-states)
  - [Keyboard Movement](#keyboard-movement)
  - [Grouping Sprites](#grouping-sprites)
    - [Local and global positions](#local-and-global-positions)
    - [Using a ParticleContainer to group sprites](#using-a-particlecontainer-to-group-sprites)
  - [Pixi's Graphic Primitives](#pixis-graphic-primitives)
    - [Rectangles](#rectangles)
    - [Circles](#circles)
    - [Ellipses](#ellipses)
    - [Rounded rectangles](#rounded-rectangles)
    - [Lines](#lines)
    - [Polygons](#polygons)
  - [Displaying text](#displaying-text)
  - [Collision detection](#collision-detection)
    - [The hitTestRectangle function](#the-hittestrectangle-function)
  - [Case study: Treasure Hunter](#case-study-treasure-hunter)
    - [The code structure](#the-code-structure)
    - [Initialize the game in the setup function](#initialize-the-game-in-the-setup-function)
      - [Creating the game scenes](#creating-the-game-scenes)
      - [Making the dungeon, door, explorer and treasure](#making-the-dungeon-door-explorer-and-treasure)
      - [Making the blob monsters](#making-the-blob-monsters)
      - [Making the health bar](#making-the-health-bar)
      - [Making the message text](#making-the-message-text)
    - [Playing the game](#playing-the-game)
    - [Moving the explorer](#moving-the-explorer)
      - [Containing movement](#containing-movement)
    - [Moving the monsters](#moving-the-monsters)
    - [Checking for collisions](#checking-for-collisions)
    - [Reaching the exit door and ending the game](#reaching-the-exit-door-and-ending-the-game)
  - [More about sprites](#more-about-sprites)
  - [Taking it further](#taking-it-further)
    - [Hexi](#hexi)
    - [BabylonJS](#babylonjs)
  - [Please help to support this project!](#please-help-to-support-this-project)
  i.[Hexi](#hexi)</br>
  ii.[BabylonJS](#babylonjs)</br>
25. [Поддерживая этот проект](#supportingthisproject)

<a id='introduction'></a>
Вступление
------------

Pixi - это чрезвычайно быстрый движок рендеринга 2D-спрайтов. Что это
жадный? Это означает, что он помогает отображать, анимировать и управлять
интерактивная графика, чтобы вам было легко создавать игры и
приложения, использующие
JavaScript и другие технологии HTML5. Имеет разумный,
незагроможденный API и включает множество полезных функций, таких как поддержка
текстурные атласы и обеспечение оптимизированной системы для анимации
спрайты (интерактивные изображения). Он также дает вам полный график сцены, чтобы вы могли
создавать иерархии вложенных спрайтов (спрайты внутри спрайтов), а также
позволяя прикреплять события мыши и касания непосредственно к спрайтам. А также,
большинство
что важно, Pixi старается не мешать вам, чтобы вы могли использовать как можно больше или
как можно меньше, адаптируйте его к своему личному кодированию
style и легко интегрируйте его с другими полезными фреймворками.

API Pixi на самом деле является усовершенствованной версией зашитого и проверенного в боях
API впервые был разработан Macromedia / Adobe Flash. Старые разработчики Flash
будет чувствовать себя как дома. Другие текущие фреймворки рендеринга спрайтов используют
аналогичный API: CreateJS, Starling, Sparrow и SpriteKit от Apple. В
Преимущество API Pixi в том, что он универсален: это не игра
двигатель. Это хорошо, потому что дает вам полную свободу выражения, чтобы создавать все, что вам нравится, и оборачивать это своим собственным игровым движком.

В этом уроке вы узнаете, как комбинировать Pixi
мощные функции рендеринга изображений и граф сцены, чтобы начать создавать
игры. Но Pixi не только для игр - вы можете использовать их
техники для создания любых интерактивных медиа-приложений. Это значит
приложения для телефонов!

Что вам нужно знать, прежде чем приступить к работе с этим руководством?

У вас должно быть разумное понимание HTML и JavaScript. Вам не обязательно быть экспертом, просто амбициозным новичком с желанием учиться. Если вы не знаете HTML и JavaScript,
Лучшее место для начала изучения - это эта книга:

[Foundation Game Design with HTML5 and JavaScript](https://rutracker.org/forum/viewtopic.php?t=4342415)

Я точно знаю, что это лучшая книга, потому что я ее написал!

Есть также несколько хороших интернет-ресурсов, которые помогут вам начать работу:

[Khan Academy: Computer
Programming](http://www.khanacademy.org/computing/cs)

[Code Academy:
JavaScript](http://www.codecademy.com/tracks/javascript)

Выберите то, что лучше всего подходит вашему стилю обучения.

Вы знаете, что такое переменные, функции, массивы и объекты JavaScript и как их
использовать? Знаешь что [JSON data
files](http://www.copterlabs.com/blog/json-what-it-is-how-it-works-how-to-use-it/)
are? Вы использовали [Canvas Drawing API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_graphics_with_canvas)?

Чтобы использовать Pixi, вам также необходимо запустить веб-сервер в корневом проекте.
каталог. Вы знаете, что такое веб-сервер и как запустить один в папке вашего проекта? 
Лучше всего использовать
[node.js](http://nodejs.org) а затем установить чрезвычайно простой в использовании
[http-server](https://github.com/nodeapps/http-server). Тем не менее, если вы хотите это сделать, вам нужно чувствовать себя комфортно при работе с командной строкой Unix. Вы можете узнать, как использовать
Unix [in this video](https://www.youtube.com/watch?feature=player_embedded&v=cX9ASUE3YAQ)
and, when you're finished, follow it with [this
video](https://www.youtube.com/watch?v=INk0ATBbclc). You should learn
how to use Unix - it only takes a couple of hours to learn and is a
really fun and easy way to interact with your computer.

Но если вы пока не хотите возиться с командной строкой, попробуйте Mongoose
webserver:

[Mongoose](http://cesanta.com/mongoose.shtml)

Или просто напишите весь свой код, используя отличный [текстовый редактор 
Brackets](http://brackets.io). Brackets автоматически запускает веб-сервер
и браузер для вас, когда вы нажимаете кнопку с изображением молнии в его
основное рабочее пространство.

Теперь, если вы думаете, что готовы, читайте дальше!

(Просьба к читателям: это * живой документ *. Если у тебя есть
вопросы о конкретных деталях или необходимости разъяснения содержания, пожалуйста
создайте ** проблему ** в этом репозитории GitHub, и я обновлю текст
с дополнительной информацией.)

<a id='settingup'></a>
Настройка
----------

Прежде чем приступить к написанию кода, создайте папку для своего проекта и запустите
веб-сервер в корневом каталоге проекта. Если вы не используете
веб-сервер, Pixi не будет работать.

Далее вам необходимо установить Pixi.

<a id='installingpixi'></a>

### Установка Pixi

Версия, используемая для этого введения: **v4.5.5**
и вы можете найти файл `pixi.min.js` либо в этом репозитории в папке `pixi` либо в [Страница выпуска Pixi для версии 4.5.5](https://github.com/pixijs/pixi.js/releases/tag/v4.5.5).
Или вы можете получить последнюю версию из [Pixi's main release page](https://github.com/pixijs/pixi.js/releases).

Этот файл - все, что вам нужно для использования Pixi. Вы можете игнорировать все
другие файлы в репозитории: **они тебе не нужны.**

Затем создайте базовую HTML-страницу и используйте тэг `<script>` чтобы залинковать
файл `pixi.min.js` который только что скачали. Тэги `<script>` и `src`
должен быть относительно вашего корневого каталога, в котором находится ваш веб-сервер
Бег. Ваш тэг `<script>` может выглядеть примерно так:

```html
<script src="pixi.min.js"></script>
```

Вот базовая HTML-страница, которую вы можете использовать, чтобы связать Pixi и протестировать ее.
это работает. (Предполагается, что `pixi.min.js` находится в подпапке с именем `pixi`.):

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello World</title>
</head>
  <script src="pixi/pixi.min.js"></script>
<body>
  <script type="text/javascript">
    let type = "WebGL"
    if(!PIXI.utils.isWebGLSupported()){
      type = "canvas"
    }

    PIXI.utils.sayHello(type)
  </script>
</body>
</html>
```

Если Pixi подключается правильно,
что-то вроде этого будет отображаться в консоли JavaScript вашего веб-браузера по умолчанию:

```
      PixiJS 4.4.5 - * canvas * http://www.pixijs.com/  ♥♥♥ 
```

<a id='application'></a>
Создание приложения Pixi и `stage`
----------------------------------

Теперь вы можете начать использовать Pixi!

Но как?

Первый шаг - создать прямоугольную
область отображения, в которой можно начать отображение изображений. 
У Pixi есть объект ʻApplication`, который создает это за вас. 
Он автоматически генерирует HTML-элемент <canvas> и определяет, как
отображать ваши изображения на холсте. Затем вам нужно создать
специальный объект Pixi `Container` под названием` stage`. Как вы увидите
далее этот объект `stage` будет использоваться как корневой контейнер
который содержит все, что вы хотите, чтобы Pixi отображала.

Вот код, который вам нужно написать, чтобы создать `app` Pixi Application
и `stage`. Добавьте этот код в свой HTML-документ между тэгами `<script>`:

```js
//Создать приложение Pixi
let app = new PIXI.Application({width: 256, height: 256});

//Добавьте холст, который Pixi автоматически создал для вас, в HTML-документ.
document.body.appendChild(app.view);
```

Это самый простой код, который вам нужно написать, чтобы начать использовать Pixi.
Он создает черный элемент холста размером 256 на 256 пикселей и добавляет его в ваш
HTML-документ. Вот как это выглядит в браузере при запуске этого кода.

![Базовый экран](/examples/images/screenshots/01.png)

Вау [черный квадрат](http://rampantgames.com/blog/?p=7745)!

`PIXI.Application` выясняет, использовать ли Canvas Drawing API или WebGL для рендеринга графики, в зависимости от того, что доступно в используемом вами веб-браузере. Его аргумент - это единственный объект, называемый объектом `options`.
В этом примере его `width` и `height` свойства установлены для определения ширины и высоты холста в пикселях. Вы можете установить еще много дополнительных свойств внутри этого объекта `options`;
вот как вы можете использовать его для настройки сглаживания, прозрачности и разрешения:

```js
let app = new PIXI.Application({ 
    width: 256,         // default: 800
    height: 256,        // default: 600
    antialias: true,    // default: false
    transparent: false, // default: false
    resolution: 1       // default: 1
  }
);
```

Если вас устраивают настройки Pixi по умолчанию, вам не нужно устанавливать какие-либо из этих параметров.
Bно, если вам нужно, см. документацию Pixi на [PIXI.Application](http://pixijs.download/release/docs/PIXI.Application.html).

Что делают эти варианты?
`antialias` сглаживает края шрифтов и графических примитивов. (WebGL
сглаживание доступно не на всех платформах, поэтому вам необходимо протестировать
это на целевой платформе вашей игры.) `transparent` делает холст
фон прозрачный. `resolution` облегчает работу с
дисплеи с различным разрешением и плотностью пикселей.
Настройка разрешений немного выходит за рамки этого руководства,
но проверьте [Объяснение Мэта Гроува](http://www.goodboydigital.com/pixi-js-v2-fastest-2d-webgl-renderer/) о том, как использовать `resolution` для всех деталей.
Но обычно для большинства проектов просто держите значение «разрешение» равным 1, и все будет в порядке.

Объект Pixi `renderer` по умолчанию будет использовать WebGL, что хорошо, потому что WebGL
невероятно быстр и позволяет использовать впечатляющие визуальные эффекты,
вы узнаете все в будущем.
Но если вам нужно заставить Canvas Drawing API rendering поверх WebGL,
вы можете установить опцию `forceCanvas` в `true`, вот так:

```js
forceCanvas: true,
```

Если вам нужно изменить цвет фона холста после того, как вы
создал его, установите свойство `backgroundColor` объекта `app.renderer`
в любое шестнадцатеричное значение цвета:

```js
app.renderer.backgroundColor = 0x061639;
```

Если вы хотите найти ширину или высоту `renderer`, используйте
`app.renderer.view.width` и `app.renderer.view.height`.

Чтобы изменить размер canvas, используйте метод `renderer` `resize`
, и передайте любые новые значения `width` и `height`. Но чтобы сделать
убедитесь, что размер холста изменен в соответствии с разрешением,
установите `autoResize` в `true`.

```js
app.renderer.autoResize = true;
app.renderer.resize(512, 512);
```

Если вы хотите, чтобы холст заполнял все окно, вы можете применить это
Стилизацией CSS и изменением размера рендера до размера окна браузера..

```
app.renderer.view.style.position = "absolute";
app.renderer.view.style.display = "block";
app.renderer.autoResize = true;
app.renderer.resize(window.innerWidth, window.innerHeight);
```

Но, если вы это сделаете, убедитесь, что вы также установили отступы по умолчанию и
поля до 0 для всех ваших HTML-элементов с помощью этого фрагмента кода CSS:

```html
<style>* {padding: 0; margin: 0}</style>
```

(Звездочка, *, в коде выше, в CSS это "универсальный селектор",
который просто означает "все теги в HTML-документе".)

Если вы хотите, чтобы холст масштабировался пропорционально любому окну браузера
размер, вы можете использовать[эту подстройку функции `scaleToWindow`](https://github.com/kittykatattack/scaleToWindow).

<a id='sprites'></a>
Pixi спрайты
------------

Теперь, когда у вас есть средство визуализации, вы можете начать добавлять в него изображения.
Все, что вы хотите сделать видимым в рендерере, необходимо добавить в специальный объект Pixi, называемый `stage` (deprecated, с версии 5 это теперь PIXI.container). Вы можете получить доступ к этому специальному объекту `stage` так:

```js
app.stage
```

`stage` это Pixi объект `Container`. Вы можете думать о контейнере
как своего рода пустую коробку, которая будет группироваться и хранить все, что вы
положить внутрь.
Объект `stage` - это корневой контейнер для всех видимых
вещей в вашей сцене.
Все, что вы поместите в `stage`, будет на холсте. Сейчас `stage` пуста, но скоро мы собираемся
начать класть вещи в нее. (Вы можете узнать больше об объектах Pixi `Container` [здесь](http://pixijs.download/release/docs/PIXI.Container.html)).

(Важно: поскольку `stage` это Pixi `Container` он имеет те же свойства и методы, что и любой другой объект`Container`. Но, хотя `stage` имеет свойства `width` и `height`, *они не относятся к
размеру окна рендеринга*. `width` и `height` сцены это просто площадь, занимаемая предметами, которые вы поместили внутрь - подробнее об этом впереди!)

Так что вы можете поместить на сцену? Специальные объекты изображения, называемые
**sprites**. Спрайты - это просто изображения, которыми вы можете управлять.
в коде. Вы можете контролировать их положение, размер и множество других свойств, 
которые полезны для создания интерактивной и анимированной графики.
Научиться создавать и контролировать спрайты - действительно самая важная вещь 
в обучении использованию Pixi.

В Pixi есть класс `Sprite`, который является универсальным способом создания игры.
Есть три основных способа их создания:

- Из одного файла изображения.
- Из суб-изображений в **tileset**. Набор плиток - это одно большое изображение, которое
включает все изображения, которые вам понадобятся в вашей игре.
- Из **texture atlas** (Файл JSON, определяющий размер и положение изображения на тайлсете.)

Вы собираетесь изучить все три способа, но прежде давайте найдем
что вам нужно знать об изображениях, прежде чем вы сможете их отображать
с Pixi.

<a id='loading'></a>
Загрузка изображений в кеш текстур
-------------------------------------

Поскольку Pixi отображает изображение на GPU с помощью WebGL, изображение требует
быть в формате, который GPU может обрабатывать. Готовое к WebGL изображение
называется **texture**. Прежде чем вы сможете заставить спрайт отображать изображение,
вам нужно преобразовать обычный файл изображения в текстуру WebGL.
Чтобы все работало быстро и эффективно, Pixi использует
**кэш текстур** для хранения и ссылки на все текстуры для ваших спрайтов.
Имена текстур представляют собой строки, соответствующие расположению файлов изображений, к которым они относятся.
Это означает, что если у вас есть текстура, загруженная из «images/cat.png», вы можете найти ее в кеше текстур, так:

```js
PIXI.utils.TextureCache["images/cat.png"];
```

Текстуры хранятся в формате, совместимом с WebGL, что эффективно для работы рендерера Pixi с ним. Затем вы можете использовать класс Pixi `Sprite`, чтобы создать новый спрайт с использованием текстуры.

```js
let texture = PIXI.utils.TextureCache["images/anySpriteImage.png"];
let sprite = new PIXI.Sprite(texture);
```

Но как загрузить файл изображения и преобразовать его в текстуру?
Используйте встроенный в Pixi объект `loader`.

Мощный Pixi объект `loader` это все, что вам нужно для загрузки любого изображения.
Вот как с его помощью загрузить изображение и вызвать функцию с именем `setup` когда изображение закончило загрузку:

```js
PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  //Этот код будет запущен, когда загрузчик закончит загрузку изображения.
}
```

[Команда разработчиков Pixi рекомендует](http://www.html5gamedevs.com/topic/16019-preload-all-textures/?p=90907)
что если вы используете загрузчик, вы должны создать спрайт с помощью
ссылки на текстуру в `resources` объекта `loader` , вот так:

```js
let sprite = new PIXI.Sprite(
  PIXI.loader.resources["images/anyImage.png"].texture
);
```

Вот пример полного кода, который вы можете написать для загрузки изображения,
вызвать функцию `setup` и создать спрайт из загруженного изображения:

```js
PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  let sprite = new PIXI.Sprite(
    PIXI.loader.resources["images/anyImage.png"].texture
  );
}
```

Это общий формат, который мы будем использовать для загрузки изображений и создания
спрайтов в этом уроке.

Вы можете загрузить несколько изображений одновременно, перечислив их с помощью
цепочки методов `add` , вот так:

```js

PIXI.loader
  .add("images/imageOne.png")
  .add("images/imageTwo.png")
  .add("images/imageThree.png")
  .load(setup);
```

А еще лучше просто перечислите все файлы, которые хотите загрузить.
массивом внутри одного `add` метода, вот так:

```js
PIXI.loader
  .add([
    "images/imageOne.png",
    "images/imageTwo.png",
    "images/imageThree.png"
  ])
  .load(setup);
```

`loader` также позволяет загружать файлы JSON, о чем вы узнаете позже.

<a id='displaying'></a>

Отображение спрайтов
--------------------

После того, как вы загрузили изображение и использовали его для создания спрайта, вам нужно добавить спрайт на сцену `stage` Pixi методом `stage.addChild` вот так:

```js
app.stage.addChild(cat);
```

Помните, что `stage` это основной контейнер, в котором хранятся все ваши спрайты.

**Важно: вы не сможете увидеть свои спрайты, если не добавите их в `stage`!**

Прежде чем продолжить, давайте рассмотрим практический пример того, как использовать то, что
вы только что научились отображать одно изображение. В папке `examples/images`
вы найдете изображение кота в формате PNG размером 64 на 64 пискеля.

![Basic display](/examples/images/cat.png)

Вот весь код JavaScript, необходимый для загрузки изображения, создания
спрайта и отображения его на сцене Pixi:

```js
//Создать приложение Pixi
let app = new PIXI.Application({
    width: 256,
    height: 256,
    antialias: true,
    transparent: false,
    resolution: 1
  }
);

//Добавьте холст, который Pixi автоматически создал для вас, в HTML-документ.
document.body.appendChild(app.view);

//загрузите изображение и запустите функцию `setup`, когда это будет сделано
PIXI.loader
  .add("images/cat.png")
  .load(setup);

//Эта функция `setup` запускается, когда изображение загружено.
function setup() {

  //Создайте спрайт кошки
  let cat = new PIXI.Sprite(PIXI.loader.resources["images/cat.png"].texture);
  
  //Добавьте кота на сцену
  app.stage.addChild(cat);
}
```

Когда этот код запустится, вы увидите следующее:

![Cat on the stage](/examples/images/screenshots/02.png)

Теперь мы куда-то идем!

Если вам когда-нибудь понадобится удалить спрайт со сцены, используйте метод `removeChild`:

```js
app.stage.removeChild(anySprite)
```

Но обычно установка свойства спрайта `visible` в `false` будет более простым и эффективным способом заставить спрайты исчезнуть.

```js
anySprite.visible = false;
```

<a id='usingaliases'></a>

### Использование псевдонимов

Вы можете сэкономить немного времени на вводе текста и сделать свой код более читабельным
создавая короткие псевдонимы для объектов и методов Pixi, которые вы часто
используете.
Например, вас утомляет добавление префикса `PIXI` ко всем объектам Pixi? Если вы так думаете, создайте более короткий псевдоним, указывающий на него.
Например, вот как вы можете создать псевдоним для объекта `TextureCache`:

```js
let TextureCache = PIXI.utils.TextureCache
```

Затем используйте этот псевдоним вместо оригинала, например:

```js
let texture = TextureCache["images/cat.png"];
```

Помимо возможности писать более сжатый код, использование псевдонимов имеет
дополнительное преимущество: это помогает защитить вас от частых
изменение API.
Если API Pixi изменится в будущем
версии - что будет! - вам просто нужно обновить эти псевдонимы до
Объекты и методы Pixi в одном месте, в начале
ваша программа, а не каждый экземпляр, где они используются
ваш код. Поэтому, когда команда разработчиков Pixi решает, что они хотят
Немного переставьте мебель, вы будете на шаг впереди них!

Чтобы увидеть, как это сделать, давайте перепишем написанный нами код для загрузки изображения и его отображения.
используя псевдонимы для всех объектов и методов Pixi.

```js
//Псевдонимы
let Application = PIXI.Application,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    Sprite = PIXI.Sprite;

//Создать приложение Pixi
let app = new Application({
    width: 256,
    height: 256,
    antialias: true,
    transparent: false,
    resolution: 1
  }
);

//Добавьте холст, который Pixi автоматически создал для вас, в HTML-документ.
document.body.appendChild(app.view);

//загрузите изображение и запустите функцию `setup`, когда это будет сделано
loader
  .add("images/cat.png")
  .load(setup);

//Эта функция `setup` запускается, когда изображение загружено.
function setup() {

  //Создайте спрайт кошки
  let cat = new Sprite(resources["images/cat.png"].texture);
  
  //Добавьте кота на сцену
  app.stage.addChild(cat);
}

```

В большинстве примеров в этом руководстве будут использоваться псевдонимы для Pixi.
объекты, которые следуют этой же модели. **Если не указано иное, вы можете предположим, что все последующие примеры кода используют псевдонимы, подобные этим**.

Это все, что вам нужно знать, чтобы начать загружать изображения и создавать
спрайты.

<a id='alittlemoreaboutloadingthings'></a>

### Еще немного о загрузке вещей

Формат, который я показал вам выше, я предлагаю вам использовать в качестве
стандартный шаблон для загрузки изображений и отображения спрайтов. Так что вы
можете спокойно игнорировать следующие несколько абзацев и сразу перейти к
следующему разделу «Размещение спрайтов». Но объект загрузчика Pixi
довольно сложный и включает в себя несколько функций, которыми вы должны быть
осведомлены, даже если вы не используете их на регулярной основе. Давайте
посмотрите на некоторые из самых полезных.

<a id='makeaspritefromanordinaryjavascriptimageobject'></a>

#### Создайте спрайт из обычного объекта изображения JavaScript или холста

Для оптимизации и повышения эффективности всегда лучше создавать спрайт из
текстуры, которая была предварительно загружена в кеш текстур Pixi. Но если
почему-то вам нужно сделать текстуру из обычного объекта JavaScript `Image`,
вы можете сделать это используя классы Pixi `BaseTexture` и `Texture`:

```js
let base = new PIXI.BaseTexture(anyImageObject),
    texture = new PIXI.Texture(base),
    sprite = new PIXI.Sprite(texture);
```

Вы можете использовать `BaseTexture.fromCanvas` если вы хотите сделать текстуру
из любого существующего элемента холста:

```js
let base = new PIXI.BaseTexture.fromCanvas(anyCanvasElement),
```

Если вы хотите изменить текстуру, отображаемую спрайтом, используйте
свойство `texture`. Установите его на любой объект `Текстура`, например:

```js
anySprite.texture = PIXI.utils.TextureCache["anyTexture.png"];
```

Вы можете использовать эту технику для интерактивного изменения спрайта
внешний вид, если с ним в игре произойдет что-то существенное.

<a id='assigninganametoaloadingfile'></a>

#### Присвоение имени загружаемому файлу

Каждому ресурсу можно присвоить уникальное имя.
грузить.
Просто укажите имя (строку) в качестве первого аргумента в методе `add`.
Например, вот как назвать изображение кошки как `catImage`.

```js
PIXI.loader
  .add("catImage", "images/cat.png")
  .load(setup);
```

Это создает объект с именем `catImage` в `loader.resources`.
Это означает, что вы можете создать спрайт, обратившись к объект `catImage`, вот так:

```js
let cat = new PIXI.Sprite(PIXI.loader.resources.catImage.texture);
```

Однако я рекомендую вам не использовать эту функцию!
Это потому, что вам нужно запомнить все имена, которые вы дали каждому загруженному файлу,
а также убедитесь, что вы случайно не используете одно и то же имя более одного раза.
Использование имени пути к файлу, как мы делали в предыдущих примерах, проще и менее подвержено ошибкам..

<a id='monitoringloadprogress'></a>

#### Мониторинг прогресса загрузки

В загрузчике Pixi есть специальное событие `progress`, которое вызывает
настраиваемая функция, которая будет запускаться каждый раз при загрузке файла.
События `progress` вызываются методом `on` объекта `loader`, вот так:

```js
PIXI.loader.on("progress", loadProgressHandler);
```

Вот как включить метод `on` в цепочку загрузки и вызвать определяемая
пользователем функция, называемая `loadProgressHandler` каждый раз,
когда файл загружается.

```js
PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler() {
  console.log("loading");
}

function setup() {
  console.log("setup");
}
```

Каждый раз, когда загружается один из файлов, событие progress вызывает
`loadProgressHandler` для отображения "loading" в консоли.
Когда все три файла загружены, функция setup будет запущена.
Вот вывод вышеприведенного кода в консоли:

```js
loading
loading
loading
setup
```

Это здорово, но становится лучше. Вы также можете узнать, какой именно файл
загружен, и какой процент файлов в настоящее время загружен.
Вы можете сделать это, добавив необязательные `loader` и
`resource` параметры к `loadProgressHandler`, вот так:

```js
function loadProgressHandler(loader, resource) { /*...*/ }
```

Затем вы можете использовать `resource.url` чтобы найти текущий файл
загрузки. (Используйте `resource.name` если вы хотите найти необязательное имя
что вы могли назначить файлу, как первый аргумент в методе
`add`.) И вы можете использовать `loader.progress` для поиска
процента от общих ресурсов загрузки.
Вот код, который это делает.

```js
PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler(loader, resource) {

  // Отобразить загружаемый в данный момент файл url
  console.log("loading: " + resource.url);

  // Показать процент загруженных файлов
  console.log("progress: " + loader.progress + "%");

  // Если вы указали имена файлов в качестве первого аргумента метода ʻadd`,
  // вы можете получить к ним доступ следующим образом
  // console.log("loading: " + resource.name);
}

function setup() {
  console.log("All files loaded");
}
```

Вот что этот код будет отображать в консоли при запуске:

```js
loading: images/one.png
progress: 33.333333333333336%
loading: images/two.png
progress: 66.66666666666667%
loading: images/three.png
progress: 100%
All files loaded
```

Это действительно здорово, потому что вы можете использовать это как основу для
создание индикатора выполнения загрузки.

(Note: Есть дополнительные свойства, к которым вы можете получить доступ на
объект `resource`. `resource.error` расскажет вам о любых возможных
ошибках, произошедших во время попытки загрузить файл. `resource.data` открывает вам
доступ к необработанным двоичным данным файла.)

<a id='moreaboutpixisloader'></a>

#### Подробнее о загрузчике Pixi

Загрузчик Pixi невероятно многофункциональный и настраиваемый. Давайте
взгляните на его использование с высоты птичьего полета, чтобы
начать.

Цепной метод ʻadd` загрузчика принимает 4 основных аргумента.:

```js
add(name, url, optionObject, callbackFunction)
```

Вот что говорится в документации по исходному коду загрузчика
эти параметры:

`name` (string): Имя загружаемого ресурса. Если он не передан, используется url.
`url` (string): URL-адрес этого ресурса относительно baseUrl загрузчика.
`options` (object literal): Варианты загрузки.
`options.crossOrigin` (Boolean): Является ли запрос кросс-источником? По умолчанию определяется автоматически.
`options.loadType`: Как следует загружать ресурс? Значение по умолчанию - `Resource.LOAD_TYPE.XHR`.
`options.xhrType`: Как следует интерпретировать загружаемые данные
при использовании XHR? Значение по умолчанию - `Resource.XHR_RESPONSE_TYPE.DEFAULT`
`callbackFunction`: Функция, вызываемая, когда этот конкретный ресурс завершает загрузку.

Единственный из этих обязательных аргументов - `url` (файл, который вы хотите загрузить).

Вот несколько примеров того, как можно использовать метод `add` для загрузки файла. Эти первые - это то, что в документации называется "нормальным синтаксисом" загрузчика.:

```js
.add('key', 'http://...', function () {})
.add('http://...', function () {})
.add('http://...')
```

А это примеры "объектного синтаксиса" загрузчика.:

```js
.add({
  name: 'key2',
  url: 'http://...'
}, function () {})

.add({
  url: 'http://...'
}, function () {})

.add({
  name: 'key3',
  url: 'http://...'
  onComplete: function () {}
})

.add({
  url: 'https://...',
  onComplete: function () {},
  crossOrigin: true
})
```

Вы также можете передать методу `add` массив объектов, или urls, или оба:

```js
.add([
  {name: 'key4', url: 'http://...', onComplete: function () {} },
  {url: 'http://...', onComplete: function () {} },
  'http://...'
]);
```

(Note: Если вам когда-нибудь понадобится перезагрузить загрузчик, чтобы загрузить новый пакет файлов, вызовите метод загрузчика `reset`: `PIXI.loader.reset();`)

Загрузчик Pixi имеет множество дополнительных функций, в том числе
позволяет загружать и анализировать двоичные файлы всех типов. Это не
то, что вам нужно делать изо дня в день, и выходит за рамки этого руководства,
так что [не забудьте проверить репозиторий загрузчика на GitHub
Чтобы получить больше информации](https://github.com/englercj/resource-loader).

<a id='positioning'></a>
Размещение спрайтов
-------------------

Теперь, когда вы знаете, как создавать и отображать спрайты, давайте узнаем
как их расположить и изменить размер.

В предыдущем примере спрайт кошки был добавлен на сцену в
верхний левый угол. У кота есть `x` позложение равное 0 и
`y` положение равное 0.
Вы можете изменить положение кошки, измененяя значения его свойств `x` и` y`.
Вот как можно центрировать кошку на сцене, установите значения свойств `x` и` y` на 96.

```js
cat.x = 96;
cat.y = 96;
```

Добавьте эти две строки кода в любое место внутри функции
`setup`, после того, как вы создали спрайт.

```js
function setup() {

  //Создание спрайта `cat`
  let cat = new Sprite(resources["images/cat.png"].texture);

  //Измените положение спрайта
  cat.x = 96;
  cat.y = 96;

  //Добавьте кота на сцену, чтобы вы его видели
  app.stage.addChild(cat);
}
```

(Note: В этом примере,
`Sprite` это псевдоним для `PIXI.Sprite`, `TextureCache` является
псевдонимом для `PIXI.utils.TextureCache`, а `resources` это псевдоним для
`PIXI.loader.resources` как описано ранее.
Я буду использовать псевдонимы в том же формате для всех объектов Pixi и
методы в примере кода с этого момента.)

Эти две новые строки кода переместят кота на 96 пикселей вправо,
и 96 пикселей вниз. Вот результат:

![Cat центрирован на сцене](/examples/images/screenshots/03.png)

Левый верхний угол кошки (левое ухо) представляет ее `x` и `y`.
точка привязки. Чтобы кошка двигалась вправо, увеличьте
значение его свойства `x`. Чтобы кошка двигалась вниз, увеличьте
значение его свойства `y`. Если у кота значение `x` равно 0, оно будет на
самой левой стороне сцены. Если он имеет значение `y`, равное 0, он будет
на самом верху сцены.

![Cat центрирован на сцене - diagram](/examples/images/screenshots/04.png)

Вместо того, чтобы устанавливать свойства спрайта `x` и` y` независимо друг от друга,
вы можете установить их вместе в одной строке кода, например:

```js
sprite.position.set(x, y)
```

<a id='sizenscale'></a>
Размер и масштаб
----------------

Вы можете изменить размер спрайта, установив его свойства `width` и `height`. Вот как задать кошке `width`  80 пикселей и `height` 20 пикселей.

```js
cat.width = 80;
cat.height = 120;
```

Добавьте эти две строки кода в функцию `setup`, вот так:

```js
function setup() {

  //Создайте спрайт `cat`
  let cat = new Sprite(resources["images/cat.png"].texture);

  //Измените положение спрайта
  cat.x = 96;
  cat.y = 96;

  //Изменить размер спрайта
  cat.width = 80;
  cat.height = 120;

  //Добавьте кота на сцену, чтобы вы его видели
  app.stage.addChild(cat);
}
```

Вот результат:

![Высота и ширина кошки изменены](/examples/images/screenshots/05.png)

Вы можете видеть, что положение кошки (ее левый верхний угол) не изменилось.
меняем только его ширину и высоту.

![Высота и ширина кота изменены - диаграмма](/examples/images/screenshots/06.png)

Спрайты также имеют свойства `scale.x` и `scale.y` которые меняют
ширина и высота спрайта пропорциональны. Вот как настроить кошачий
масштабировать до половины размера:

```js
cat.scale.x = 0.5;
cat.scale.y = 0.5;
```

Scale values are numbers between 0 and 1 that represent a
percentage of the sprite's size. 1 means 100% (full size), while
0.5 means 50% (half size). You can double the sprite's size by setting
its scale values to 2, like this:
```js
cat.scale.x = 2;
cat.scale.y = 2;
```
Pixi has an alternative, concise way for you set sprite's scale in one
line of code using the `scale.set` method.
```js
cat.scale.set(0.5, 0.5);
```
If that appeals to you, use it!

<a id='rotation'></a>
Rotation
--------

You can make a sprite rotate by setting its `rotation` property to a
value in [radians](http://www.mathsisfun.com/geometry/radians.html).
```js
cat.rotation = 0.5;
```
But around which point does that rotation happen?

You've seen that a sprite's top left corner represents its `x` and `y` position. That point is
called the **anchor point**. If you set the sprite’s `rotation`
property to something like `0.5`, the rotation will happen *around the
sprite’s anchor point*.
This diagram shows what effect this will have on our cat sprite.

![Rotation around anchor point - diagram](/examples/images/screenshots/07.png)

You can see that the anchor point, the cat’s left ear, is the center of the imaginary circle around which the cat is rotating.
What if you want the sprite to rotate around its center? Change the
sprite’s `anchor` point so that it’s centered inside the sprite, like
this:
```js
cat.anchor.x = 0.5;
cat.anchor.y = 0.5;
```
The `anchor.x` and `anchor.y` values represent a percentage of the texture’s dimensions, from 0 to 1 (0%
to 100%). Setting it to 0.5 centers the texture over the point. The location of the point
itself won’t change, just the way the texture is positioned over it.

This next diagram shows what happens to the rotated sprite if you center its anchor point.

![Rotation around centered anchor point - diagram](/examples/images/screenshots/08.png)

You can see that the sprite’s texture shifts up and to the left. This
is an important side-effect to remember!

Just like with `position` and `scale`, you can set the anchor’s x and
y values with one line of code like this:
```js
cat.anchor.set(x, y)
```
Sprites also have a `pivot` property which works in a similar way to
`anchor`. `pivot` sets the position
of the sprite's x/y origin point. If you change the pivot point and
then rotate the sprite, it will
rotate around that origin point. For example, the following code will
set the sprite's `pivot.x` point to 32, and its `pivot.y` point to 32
```js
cat.pivot.set(32, 32)
```
Assuming that the sprite is 64x64 pixels, the sprite will now rotate
around its center point. But remember: if you change a sprite's pivot
point, you've also changed its x/y origin point. 

So, what's the difference between `anchor` and `pivot`? They're really
similar! `anchor` shifts the origin point of the sprite's image texture, using a 0 to 1 normalized value.
`pivot` shifts the origin of the sprite's x and y point, using pixel
values. Which should you use? It's up to you. Just play around
with both of them and see which you prefer.

<a id='tileset'></a>
Make a sprite from a tileset sub-image
--------------------------------------

You now know how to make a sprite from a single image file. But, as a
game designer, you’ll usually be making your sprites using
**tilesets** (also known as **spritesheets**.) Pixi has some convenient built-in ways to help you do this.
A tileset is a single image file that contains sub-images. The sub-images
represent all the graphics you want to use in your game. Here's an
example of a tileset image that contains game characters and game
objects as sub-images.

![An example tileset](/examples/images/screenshots/09.png)

The entire tileset is 192 by 192 pixels. Each image is in its own 32 by 32
pixel grid cell. Storing and accessing all your game graphics on a
tileset is a very
processor and memory efficient way to work with graphics, and Pixi is
optimized for this.

You can capture a sub-image from a tileset by defining a rectangular
area
that's the same size and position as the sub-image you want to
extract. Here's an example of the rocket sub-image that’s been extracted from
the tileset.

![Rocket extracted from tileset](/examples/images/screenshots/10.png)

Let's look at the code that does this. First, load the `tileset.png` image
with Pixi’s `loader`, just as you've done in earlier examples.
```js
loader
  .add("images/tileset.png")
  .load(setup);
```
Next, when the image has loaded, use a rectangular sub-section of the tileset to create the
sprite’s image. Here's the code that extracts the sub image, creates
the rocket sprite, and positions and displays it on the canvas.
```js
function setup() {

  //Create the `tileset` sprite from the texture
  let texture = TextureCache["images/tileset.png"];

  //Create a rectangle object that defines the position and
  //size of the sub-image you want to extract from the texture
  //(`Rectangle` is an alias for `PIXI.Rectangle`)
  let rectangle = new Rectangle(192, 128, 64, 64);

  //Tell the texture to use that rectangular section
  texture.frame = rectangle;

  //Create the sprite from the texture
  let rocket = new Sprite(texture);

  //Position the rocket sprite on the canvas
  rocket.x = 32;
  rocket.y = 32;

  //Add the rocket to the stage
  app.stage.addChild(rocket);
  
  //Render the stage   
  app.renderer.render(app.stage);
}
```
How does this work?

Pixi has a built-in `Rectangle` object (`PIXI.Rectangle`) that is a general-purpose
object for defining rectangular shapes. It takes four arguments. The
first two arguments define the rectangle's `x` and `y` position. The
last two define its `width` and `height`. Here's the format
for defining a new `Rectangle` object.
```js
let rectangle = new PIXI.Rectangle(x, y, width, height);
```
The rectangle object is just a *data object*; it's up to you to decide how you want to use it. In
our example we're using it to define the position and area of the
sub-image on the tileset that we want to extract. Pixi textures have a useful
property called `frame` that can be set to any `Rectangle` objects. 
The `frame` crops the texture to the dimensions of the `Rectangle`.
Here's how to use `frame`
to crop the texture to the size and position of the rocket.
```js
let rectangle = new Rectangle(192, 128, 64, 64);
texture.frame = rectangle;
```
You can then use that cropped texture to create the sprite:
```js
let rocket = new Sprite(texture);
```
And that's how it works!

Because making sprite textures from a tileset
is something you’ll do with great frequency, Pixi has a more convenient way
to help you do this - let's find out what that is next.

<a id='textureatlas'></a>
Using a texture atlas
---------------------

If you’re working on a big, complex game, you’ll want a fast and
efficient way to create sprites from tilesets. This is where a
**texture atlas** becomes really useful. A texture atlas is a JSON
data file that contains the positions and sizes of sub-images on a
matching tileset PNG image. If you use a texture atlas, all you need
to know about the sub-image you want to display is its name. You
can arrange your tileset images in any order and the JSON file
will keep track of their sizes and positions for you. This is
really convenient because it means the sizes and positions of
tileset images aren’t hard-coded into your game program. If you
make changes to the tileset, like adding images, resizing them,
or removing them, just re-publish the JSON file and your game will
use that data to display the correct images. You won’t have to
make any changes to your game code.

Pixi is compatible with a standard JSON texture atlas format that is
output by a popular software tool called [Texture
Packer](https://www.codeandweb.com/texturepacker). Texture Packer’s
“Essential” license is free. Let’s find out how to use it to make a
texture atlas, and load the atlas into Pixi. (You don’t have to use
Texture Packer. Similar tools, like [Shoebox](http://renderhjs.net/shoebox/) or [spritesheet.js](https://github.com/krzysztof-o/spritesheet.js/), output PNG and JSON files
in a standard format that is compatible with Pixi.)

First, start with a collection of individual image files that you'd
like to use in your game.

![Image files](/examples/images/screenshots/11.png)

(All the images in this section were created by Lanea Zimmerman. You
can find more of her artwork
[here](http://opengameart.org/users/sharm).
Thanks, Lanea!)

Next, open Texture Packer and choose **JSON Hash** as the framework
type. Drag your images into Texture Packer's workspace. (You can
also point Texture Packer to any folder that contains your images.)
It will automatically arrange the images on a single tileset image, and give them names that match their original image names.

![Image files](/examples/images/screenshots/12.png)

(If you're using the free version of
Texture Packer, set **Algorithm** to `Basic`, set **Trim mode** to
`None`, set **Extrude** to `0`, set **Size constraints** to `Any size` and slide the **PNG Opt
Level** all the way to the left to `0`. These are the basic
settings that will allow the free version of Texture Packer to create
your files without any warnings or errors.)

When you’re done, click the **Publish** button. Choose the file name and
location, and save the published files. You’ll end up with 2 files: a
PNG file and a JSON file. In this example my file names are
`treasureHunter.json` and `treasureHunter.png`. To make your life easier,
just keep both files in your project’s `images` folder. (You can think
of the JSON file as extra metadata for the image file, so it makes
sense to keep both files in the same folder.)
The JSON file describes the name, size and position of each of the
sub-images
in the tileset. Here’s an excerpt that describes the blob monster
sub-image.
```js
"blob.png":
{
	"frame": {"x":55,"y":2,"w":32,"h":24},
	"rotated": false,
	"trimmed": false,
	"spriteSourceSize": {"x":0,"y":0,"w":32,"h":24},
	"sourceSize": {"w":32,"h":24},
	"pivot": {"x":0.5,"y":0.5}
},
```
The `treasureHunter.json` file also contains “dungeon.png”,
“door.png”, "exit.png", and "explorer.png" properties each with
similar data. Each of these sub-images are called **frames**. Having
this data is really helpful because now you don’t need to know the
size and position of each sub-image in the tileset. All you need to
know is the sprite’s **frame id**. The frame id is just the name
of the original image file, like "blob.png" or "explorer.png".

Among the many advantages to using a texture atlas is that you can
easily add 2 pixels of padding around each image (Texture Packer does
this by default.) This is important to prevent the possibility of
**texture bleed**. Texture bleed is an effect that happens when the
edge of an adjacent image on the tileset appears next to a sprite.
This happens because of the way your computer's GPU (Graphics
Processing Unit) decides how to round fractional pixels values. Should
it round them up or down? This will be different for each GPU.
Leaving 1 or 2 pixels spacing around images on a tilseset makes all
images display consistently.

(Note: If you have two pixels of padding around a graphic, and you still notice a strange "off by one pixel" glitch in the
way Pixi is displaying it, try changing the texture's scale mode
algorithm. Here's how: `texture.baseTexture.scaleMode =
PIXI.SCALE_MODES.NEAREST;`. These glitches can sometimes happen
because of GPU floating point rounding errors.)

Now that you know how to create a texture atlas, let's find out how to
load it into your game code.

<a id='loadingatlas'></a>
Loading the texture atlas
-------------------------

To get the texture atlas into Pixi, load it using Pixi’s
`loader`. If the JSON file was made with Texture Packer, the
`loader` will interpret the data and create a texture from each
frame on the tileset automatically.  Here’s how to use the `loader` to load the `treasureHunter.json`
file. When it has loaded, the `setup` function will run.
```js
loader
  .add("images/treasureHunter.json")
  .load(setup);
```
Each image on the tileset is now an individual texture in Pixi’s
cache. You can access each texture in the cache with the same name it
had in Texture Packer (“blob.png”, “dungeon.png”, “explorer.png”,
etc.).

<a id='creatingsprites'></a>
Creating sprites from a loaded texture atlas
--------------------------------------------

Pixi gives you three general ways to create a sprite from a texture atlas:

1.	Using `TextureCache`:
```js
let texture = TextureCache["frameId.png"],
    sprite = new Sprite(texture);
```
2.	If you’ve used Pixi’s `loader` to load the texture atlas, use the 
loader’s `resources`:
```js
let sprite = new Sprite(
  resources["images/treasureHunter.json"].textures["frameId.png"]
);
```
1. That’s way too much typing to do just to create a sprite! 
So I suggest you create an alias called `id` that points to texture’s 
altas’s `textures` object, like this:
```js
let id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
```
Then you can just create each new sprite like this:
```js
let sprite = new Sprite(id["frameId.png"]);
```
Much better!

Here's how you could use these three different sprite creation
techniques in the `setup` function to create and display the
`dungeon`, `explorer`, and `treasure` sprites.
```js

//Define variables that might be used in more 
//than one function
let dungeon, explorer, treasure, id;

function setup() {

  //There are 3 ways to make sprites from textures atlas frames

  //1. Access the `TextureCache` directly
  let dungeonTexture = TextureCache["dungeon.png"];
  dungeon = new Sprite(dungeonTexture);
  app.stage.addChild(dungeon);

  //2. Access the texture using through the loader's `resources`:
  explorer = new Sprite(
    resources["images/treasureHunter.json"].textures["explorer.png"]
  );
  explorer.x = 68;

  //Center the explorer vertically
  explorer.y = app.stage.height / 2 - explorer.height / 2;
  app.stage.addChild(explorer);

  //3. Create an optional alias called `id` for all the texture atlas 
  //frame id textures.
  id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
  
  //Make the treasure box using the alias
  treasure = new Sprite(id["treasure.png"]);
  app.stage.addChild(treasure);

  //Position the treasure next to the right edge of the canvas
  treasure.x = app.stage.width - treasure.width - 48;
  treasure.y = app.stage.height / 2 - treasure.height / 2;
  app.stage.addChild(treasure);
}
```
Here's what this code displays:

![Explorer, dungeon and treasure](/examples/images/screenshots/13.png)

The stage dimensions are 512 by 512 pixels, and you can see in the
code above that the `app.stage.height` and `app.stage.width` properties are used
to align the sprites. Here's how the `explorer`'s `y` position is
vertically centered:
```js
explorer.y = app.stage.height / 2 - explorer.height / 2;
```
Learning to create and display sprites using a texture atlas is an
important benchmark. So before we continue, let's take a look at the
code you
could write to add the remaining
sprites: the `blob`s and `exit` door, so that you can produce a scene
that looks like this:

![All the texture atlas sprites](/examples/images/screenshots/14.png)

Here's the entire code that does all this. I've also included the HTML
code so you can see everything in its proper context.
(You'll find this working code in the
`examples/spriteFromTextureAtlas.html` file in this repository.)
Notice that the `blob` sprites are created and added to the stage in a
loop, and assigned random positions.
```js
<!doctype html>
<meta charset="utf-8">
<title>Make a sprite from a texture atlas</title>
<body>
<script src="../pixi/pixi.min.js"></script>
<script>

//Aliases
let Application = PIXI.Application,
    Container = PIXI.Container,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    TextureCache = PIXI.utils.TextureCache,
    Sprite = PIXI.Sprite,
    Rectangle = PIXI.Rectangle;

//Create a Pixi Application
let app = new Application({ 
    width: 512, 
    height: 512,                       
    antialias: true, 
    transparent: false, 
    resolution: 1
  }
);

//Add the canvas that Pixi automatically created for you to the HTML document
document.body.appendChild(app.view);

//load a JSON file and run the `setup` function when it's done
loader
  .add("images/treasureHunter.json")
  .load(setup);

//Define variables that might be used in more 
//than one function
let dungeon, explorer, treasure, door, id;

function setup() {

  //There are 3 ways to make sprites from textures atlas frames

  //1. Access the `TextureCache` directly
  let dungeonTexture = TextureCache["dungeon.png"];
  dungeon = new Sprite(dungeonTexture);
  app.stage.addChild(dungeon);

  //2. Access the texture using throuhg the loader's `resources`:
  explorer = new Sprite(
    resources["images/treasureHunter.json"].textures["explorer.png"]
  );
  explorer.x = 68;

  //Center the explorer vertically
  explorer.y = app.stage.height / 2 - explorer.height / 2;
  app.stage.addChild(explorer);

  //3. Create an optional alias called `id` for all the texture atlas 
  //frame id textures.
  id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
  
  //Make the treasure box using the alias
  treasure = new Sprite(id["treasure.png"]);
  app.stage.addChild(treasure);

  //Position the treasure next to the right edge of the canvas
  treasure.x = app.stage.width - treasure.width - 48;
  treasure.y = app.stage.height / 2 - treasure.height / 2;
  app.stage.addChild(treasure);

  //Make the exit door
  door = new Sprite(id["door.png"]); 
  door.position.set(32, 0);
  app.stage.addChild(door);

  //Make the blobs
  let numberOfBlobs = 6,
      spacing = 48,
      xOffset = 150;

  //Make as many blobs as there are `numberOfBlobs`
  for (let i = 0; i < numberOfBlobs; i++) {

    //Make a blob
    let blob = new Sprite(id["blob.png"]);

    //Space each blob horizontally according to the `spacing` value.
    //`xOffset` determines the point from the left of the screen
    //at which the first blob should be added.
    let x = spacing * i + xOffset;

    //Give the blob a random y position
    //(`randomInt` is a custom function - see below)
    let y = randomInt(0, app.stage.height - blob.height);

    //Set the blob's position
    blob.x = x;
    blob.y = y;

    //Add the blob sprite to the stage
    app.stage.addChild(blob);
  }
}

//The `randomInt` helper function
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

</script>
</body>
```
You can see in the code above that all the blobs are created using a
`for` loop. Each `blob` is spaced evenly along the `x` axis like this:
```js
let x = spacing * i + xOffset;
blob.x = x;
```
`spacing` has a value 48, and `xOffset` has a value of 150. What this
means is the first `blob` will have an `x` position of 150.
This offsets it from the left side of the stage by 150 pixels. Each
subsequent `blob` will have an `x` value that's 48 pixels greater than
the `blob` created in the previous iteration of the loop. This creates
an evenly spaced line of blob monsters, from left to right, along the dungeon floor.

Each `blob` is also given a random `y` position. Here's the code that
does this:
```js
let y = randomInt(0, stage.height - blob.height);
blob.y = y;
```
The `blob`'s `y` position could be assigned any random number between 0 and
512, which is the value of `stage.height`. This works with the help of
a custom function called `randomInt`. `randomInt` returns a random number
that's within a range between any two numbers you supply.
```js
randomInt(lowestNumber, highestNumber)
```
That means if you want a random number between 1 and 10, you can get
one like this:
```js
let randomNumber = randomInt(1, 10);
```
Here's the `randomInt` function definition that does all this work:
```js
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```
`randomInt` is a great little function to keep in your back pocket for
making games - I use it all the time.

<a id='movingsprites'></a>
Moving Sprites
--------------

You now know how to display sprites, but how do you make them move?
That's easy: create a looping function using Pixi's `ticker` 
This is called a **game loop**.
Any code you put inside the game loop will update 60 times per
second. Here's some code you could write to make the `cat` sprite move
to the right at a rate of 1 pixel per frame.
```js

function setup() {

  //Start the game loop by adding the `gameLoop` function to
  //Pixi's `ticker` and providing it with a `delta` argument.
  app.ticker.add(delta => gameLoop(delta));
}

function gameLoop(delta){

  //Move the cat 1 pixel 
  cat.x += 1;
}
```
If you run this bit of code, you'll see the sprite gradually move to
the right side of the stage. 

![Moving sprites](/examples/images/screenshots/15.png)

That's because each time the `gameLoop` runs, it adds 1 to the cat's x position.
```
cat.x += 1;
```

Any function you add to Pixi's `ticker` will be called 60 times per second. You can see that the function is provided a `delta` argument - what's that?

The `delta` value represents the amount of fractional lag between frames. You can optionally add it to the cat's position, to make the cat's animation independent of the frame rate. Here's how:
```js
cat.x += 1 + delta;
```
Whether or not you choose to add this `delta` value is largely an aestheic choice. And the effect will only really be noticeable if your animation is struggling to keep up with a consistent 60 frames per second display rate (which might happen, for example, if it's running on a slow device). The rest of the examples in this tutorial won't use this `delta` value, but feel free to use it in your own work if you wish.

You don't have to use Pixi's ticker to create a game loop. If you prefer, just use `requestAnimationFrame`, like this:

```js
function gameLoop() {

  //Call this `gameLoop` function on the next screen refresh
  //(which happens 60 times per second)
  requestAnimationFrame(gameLoop);

  //Move the cat
  cat.x += 1;
}

//Start the loop
gameLoop();

```

It entirely up to you which style you prefer.

And that's really all there is to it! Just change any sprite property by small
increments inside the loop, and they'll animate over time. If you want
the sprite to animate in the opposite direction (to the left), just give it a
negative value, like `-1`.

You'll find this code in the `movingSprites.html` file - here's the
complete code:
```js
//Aliases
let Application = PIXI.Application,
    Container = PIXI.Container,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    TextureCache = PIXI.utils.TextureCache,
    Sprite = PIXI.Sprite,
    Rectangle = PIXI.Rectangle;

//Create a Pixi Application
let app = new Application({ 
    width: 256, 
    height: 256,                       
    antialias: true, 
    transparent: false, 
    resolution: 1
  }
);

//Add the canvas that Pixi automatically created for you to the HTML document
document.body.appendChild(app.view);

loader
  .add("images/cat.png")
  .load(setup);

//Define any variables that are used in more than one function
let cat;

function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  app.stage.addChild(cat);
 
  //Start the game loop 
  app.ticker.add(delta => gameLoop(delta));
}

function gameLoop(delta){

  //Move the cat 1 pixel 
  cat.x += 1;
  
  //Optionally use the `delta` value
  //cat.x += 1 + delta;
}
```
(Notice that the `cat` variable needs to be defined outside the
`setup` and
`gameLoop` functions so that you can access it inside both of them.)

You can animate a sprite's scale, rotation, or size - whatever! You'll see
many more examples of how to animate sprites ahead.

<a id='velocity'></a>
Using velocity properties
-------------------------

To give you more flexibility, it's a good idea to control a sprite's
movement speed using two **velocity properties**: `vx` and `vy`. `vx`
is used to set the sprite's speed and direction on the x axis
(horizontally). `vy` is
used to set the sprite's speed and direction on the y axis (vertically). Instead of
changing a sprite's `x` and `y` values directly, first update the velocity
variables, and then assign those velocity values to the sprite. This is an
extra bit of modularity that you'll need for interactive game animation.

The first step is to create `vx` and `vy` properties on your sprite,
and give them an initial value.
```js
cat.vx = 0;
cat.vy = 0;
```
Setting `vx` and `vy` to 0 means that the sprite isn't moving.

Next, in the game loop, update `vx` and `vy` with the velocity at which you
want the sprite to move. Then assign those values to the
sprite's `x` and `y` properties. Here's how you could use this
technique to make the cat sprite move down and to right at one pixel each
frame:
```js
function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  cat.vx = 0;
  cat.vy = 0;
  app.stage.addChild(cat);
 
  //Start the game loop
  app.ticker.add(delta => gameLoop(delta));
}

function gameLoop(delta){

  //Update the cat's velocity
  cat.vx = 1;
  cat.vy = 1;

  //Apply the velocity values to the cat's 
  //position to make it move
  cat.x += cat.vx;
  cat.y += cat.vy;
}


```
When you run this code, the cat will move down and to the right at one
pixel per frame:

![Moving sprites](/examples/images/screenshots/16.png)

What if you want to make the cat move in a different direction? To
make the cat move to the left, give it a `vx` value of `-1`. To make
it move up, give the cat a `vy` value of `-1`. To make the cat move
faster, give it larger `vx` and `vy` values, like `3`, `5`, `-2`, or
`-4`.

You'll see ahead how modularizing a sprite's velocity with `vx` and
`vy` velocity properties helps with keyboard and mouse pointer
control systems for games, as well as making it easier to implement physics.

<a id='gamestates'></a>
Game states
-----------

As a matter of style, and to help modularize your code, I
recommend structuring your game loop like this:
```js
//Set the game state
state = play;
 
//Start the game loop 
app.ticker.add(delta => gameLoop(delta));

function gameLoop(delta){

  //Update the current game state:
  state(delta);
}

function play(delta) {

  //Move the cat 1 pixel to the right each frame
  cat.vx = 1
  cat.x += cat.vx;
}
```
You can see that the `gameLoop` is calling a function called `state` 60 times
per second. What is the `state` function? It's been assigned to
`play`. That means all the code in the `play` function will also run at 60
times per second.

Here's how the code from the previous example can be re-factored to
this new model:
```js
//Define any variables that are used in more than one function
let cat, state;

function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  cat.vx = 0;
  cat.vy = 0;
  app.stage.addChild(cat);

  //Set the game state
  state = play;
 
  //Start the game loop 
  app.ticker.add(delta => gameLoop(delta));
}

function gameLoop(delta){

  //Update the current game state:
  state(delta);
}

function play(delta) {

  //Move the cat 1 pixel to the right each frame
  cat.vx = 1
  cat.x += cat.vx;
}
```
Yes, I know, this is a bit of [head-swirler](http://www.amazon.com/Electric-Psychedelic-Sitar-Headswirlers-1-5/dp/B004HZ14VS)! But, don't let it scare
you and spend a minute or two walking through in your mind how those
functions are connected. As you'll see ahead, structuring your game
loop like this will make it much, much easier to do things like switching
game scenes and levels.

<a id='keyboard'></a>
Keyboard Movement
-----------------

With just a little more work you can build a simple system to control
a sprite using the keyboard. To simplify your code, I suggest you use
this custom function called `keyboard` that listens for and captures
keyboard events.
```js
function keyboard(value) {
  let key = {};
  key.value = value;
  key.isDown = false;
  key.isUp = true;
  key.press = undefined;
  key.release = undefined;
  //The `downHandler`
  key.downHandler = event => {
    if (event.key === key.value) {
      if (key.isUp && key.press) key.press();
      key.isDown = true;
      key.isUp = false;
      event.preventDefault();
    }
  };

  //The `upHandler`
  key.upHandler = event => {
    if (event.key === key.value) {
      if (key.isDown && key.release) key.release();
      key.isDown = false;
      key.isUp = true;
      event.preventDefault();
    }
  };

  //Attach event listeners
  const downListener = key.downHandler.bind(key);
  const upListener = key.upHandler.bind(key);
  
  window.addEventListener(
    "keydown", downListener, false
  );
  window.addEventListener(
    "keyup", upListener, false
  );
  
  // Detach event listeners
  key.unsubscribe = () => {
    window.removeEventListener("keydown", downListener);
    window.removeEventListener("keyup", upListener);
  };
  
  return key;
}
```
The `keyboard` function is easy to use. Create a new keyboard object like this:
```js
let keyObject = keyboard(keyValue);
```
Its one argument is the key value that you want to listen for.
[Here's a list of keys](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values).

Then assign `press` and `release` methods to the keyboard object like this:
```js
keyObject.press = () => {
  //key object pressed
};
keyObject.release = () => {
  //key object released
};
```
Keyboard objects also have `isDown` and `isUp` Boolean properties that
you can use to check the state of each key.

Don't forget to remove event listeners by using the `unsubscribe` method :
```js
keyObject.unsubscribe();
```

Take a look at the
`keyboardMovement.html` file in the `examples` folder to see how you
can use this `keyboard` function to control a sprite using your
keyboard's arrow keys. Run it and use the left, up, down, and right
arrow keys to move the cat around the stage.

![Keyboard movement](/examples/images/screenshots/17.png)

Here's the code that does all this:
```js
//Define any variables that are used in more than one function
let cat, state;

function setup() {

  //Create the `cat` sprite 
  cat = new Sprite(resources["images/cat.png"].texture);
  cat.y = 96; 
  cat.vx = 0;
  cat.vy = 0;
  app.stage.addChild(cat);

  //Capture the keyboard arrow keys
  let left = keyboard("ArrowLeft"),
      up = keyboard("ArrowUp"),
      right = keyboard("ArrowRight"),
      down = keyboard("ArrowDown");

  //Left arrow key `press` method
  left.press = () => {
    //Change the cat's velocity when the key is pressed
    cat.vx = -5;
    cat.vy = 0;
  };
  
  //Left arrow key `release` method
  left.release = () => {
    //If the left arrow has been released, and the right arrow isn't down,
    //and the cat isn't moving vertically:
    //Stop the cat
    if (!right.isDown && cat.vy === 0) {
      cat.vx = 0;
    }
  };

  //Up
  up.press = () => {
    cat.vy = -5;
    cat.vx = 0;
  };
  up.release = () => {
    if (!down.isDown && cat.vx === 0) {
      cat.vy = 0;
    }
  };

  //Right
  right.press = () => {
    cat.vx = 5;
    cat.vy = 0;
  };
  right.release = () => {
    if (!left.isDown && cat.vy === 0) {
      cat.vx = 0;
    }
  };

  //Down
  down.press = () => {
    cat.vy = 5;
    cat.vx = 0;
  };
  down.release = () => {
    if (!up.isDown && cat.vx === 0) {
      cat.vy = 0;
    }
  };

  //Set the game state
  state = play;
 
  //Start the game loop 
  app.ticker.add(delta => gameLoop(delta));
}

function gameLoop(delta){

  //Update the current game state:
  state(delta);
}

function play(delta) {

  //Use the cat's velocity to make it move
  cat.x += cat.vx;
  cat.y += cat.vy
}
```

<a id='grouping'></a>
Grouping Sprites
----------------

Groups let you create game scenes, and manage similar sprites together
as single units. Pixi has an object called a `Container`
that lets you do this. Let's find out how it works.

Imagine that you want to display three sprites: a cat, hedgehog and
tiger. Create them, and set their positions - *but don't add them to the
stage*.
```js
//The cat
let cat = new Sprite(id["cat.png"]);
cat.position.set(16, 16);

//The hedgehog
let hedgehog = new Sprite(id["hedgehog.png"]);
hedgehog.position.set(32, 32);

//The tiger
let tiger = new Sprite(id["tiger.png"]);
tiger.position.set(64, 64);
```

Next, create an `animals` container to group them all together like
this:
```js
let animals = new PIXI.Container();
```
Then use `addChild` to *add the sprites to the group*.
```js
animals.addChild(cat);
animals.addChild(hedgehog);
animals.addChild(tiger);
```
Finally add the group to the stage.
```js
app.stage.addChild(animals);
```
(As you know, the `stage` object is also a `Container`. It’s the root
container for all Pixi sprites.)

Here's what this code produces:

![Grouping sprites](/examples/images/screenshots/18.png)

What you can't see in that image is the invisible `animals` group
that's containing the sprites.

![Grouping sprites](/examples/images/screenshots/19.png)

You can now treat the `animals` group as a single unit. You can think
of a `Container` as a special kind of sprite that doesn’t
have a texture.

If you need a list of all the child sprites that `animals` contains,
use its `children` array to find out.
```
console.log(animals.children)
//Displays: Array [Object, Object, Object]
```
This tells you that `animals` has three sprites as children.

Because the `animals` group is just like any other sprite, you can
change its `x` and `y` values, `alpha`, `scale` and
all the other sprite properties. Any property value you change on the
parent container will affect the child sprites in a relative way. So if you
set the group's `x` and `y` position, all the child sprites will
be repositioned relative to the group's top left corner. What would
happen if you set the `animals`'s `x` and `y` position to 64?
```
animals.position.set(64, 64);
```
The whole group of sprites will move 64 pixels right and 64 pixels to
the down.

![Grouping sprites](/examples/images/screenshots/20.png)

The `animals` group also has its own dimensions, which is based on the area
occupied by the containing sprites. You can find its `width` and
`height` values like this:
```js
console.log(animals.width);
//Displays: 112

console.log(animals.height);
//Displays: 112

```
![Group width and height](/examples/images/screenshots/21.png)

What happens if you change a group's width or height?
```js
animals.width = 200;
animals.height = 200;
```
All the child sprites will scale to match that change.

![Group width and height](/examples/images/screenshots/22.png)

You can nest as many `Container`s inside other
`Container`s as you like, to create deep hierarchies if
you need to. However, a `DisplayObject` (like a `Sprite` or another
`Container`) can only belong to one parent at a time. If
you use `addChild` to make a sprite the child of another object, Pixi
will automatically remove it from its current parent. That’s a useful
bit of management that you don’t have to worry about.

<a id='localnglobal'></a>
### Local and global positions

When you add a sprite to a `Container`, its `x` and `y`
position is *relative to the group’s top left corner*. That's the
sprite's **local position** For example, what do you think the cat's
position is in this image?

![Grouping sprites](/examples/images/screenshots/20.png)

Let's find out:
```
console.log(cat.x);
//Displays: 16
```
16? Yes! That's because the cat is offset by only 16 pixel's from the
group's top left corner. 16 is the cat's local position.

Sprites also have a **global position**. The global position is the
distance from the top left corner of the stage, to the sprite's anchor
point (usually the sprite's top left corner.) You can find a sprite's global
position with the help of the `toGlobal` method.  Here's how:
```
parentSprite.toGlobal(childSprite.position)
```
That means you can find the cat's global position inside the `animals`
group like this:
```
console.log(animals.toGlobal(cat.position));
//Displays: Object {x: 80, y: 80...};
```
That gives you an `x` and `y` position of 80. That's exactly the cat's
global position relative to the top left corner of the stage. 

What if you want to find the global position of a sprite, but don't
know what the sprite's parent container
is? Every sprite has a property called `parent` that will tell you what the
sprite's parent is. If you add a sprite directly to the `stage`, then
`stage` will be the sprite's parent. In the example above, the `cat`'s
parent is `animals`. That means you can alternatively get the cat's global position
by writing code like this:
```
cat.parent.toGlobal(cat.position);
```
And it will work even if you don't know what the cat's parent
container currently is.

There's one more way to calculate the global position! And, it's
actually the best way, so listen up! If you want to know the distance
from the top left corner of the canvas to the sprite, and don't know
or care what the sprite's parent containers are, use the
`getGlobalPosition` method. Here's how to use it to find the tiger's global position:
```js
tiger.getGlobalPosition().x
tiger.getGlobalPosition().y
```
This will give you `x` and `y` values of 128 in the example that we've
been using.
The special thing about `getGlobalPosition` is that it's highly
precise: it will give you the sprite's accurate global position as
soon as its local position changes. I asked the Pixi development team
to add this feature specifically for accurate collision detection for
games. (Thanks, Matt and the rest of the team for adding it!)

What if you want to convert a global position to a local position? you
can use the `toLocal` method. It works in a similar way, but uses this
general format:
```js
sprite.toLocal(sprite.position, anyOtherSprite)
```
Use `toLocal` to find the distance between a sprite and any other
sprite. Here's how you could find out the tiger's local
position, relative to the hedgehog.
```js
tiger.toLocal(tiger.position, hedgehog).x
tiger.toLocal(tiger.position, hedgehog).y
```
This gives you an `x` value of 32 and a `y` value of 32. You can see
in the example images that the tiger's top left corner is 32 pixels
down and to the left of the hedgehog's top left corner.

<a id='spritebatch'></a>
### Using a ParticleContainer to group sprites

Pixi has an alternative, high-performance way to group sprites called
a `ParticleContainer` (`PIXI.particles.ParticleContainer`). Any sprites inside a `ParticleContainer` will render 2 to 5
times faster than they would if they were in a regular
`Container`. It’s a great performance boost for games.

Create a `ParticleContainer` like this:
```js
let superFastSprites = new PIXI.particles.ParticleContainer();
```
Then use `addChild` to add sprites to it, just like you would with any
ordinary `Container`.

You have to make some compromises if you decide to use a
`ParticleContainer`. Sprites inside a `ParticleContainer` only have a few  basic properties:
`x`, `y`, `width`, `height`, `scale`, `pivot`, `alpha`, `visible` – and that’s
about it. Also, the sprites that it contains can’t have nested
children of their own. A `ParticleContainer` also can’t use Pixi’s advanced
visual effects like filters and blend modes. Each `ParticleContainer` can use only one texture (so you'll have to use a spritesheet if you want Sprites with different appearances). But for the huge performance boost that you get, those
compromises are usually worth it. And you can use
`Container`s and `ParticleContainer`s simultaneously in the same project, so you can fine-tune your optimization.

Why are sprites in a `Particle Container` so fast? Because the positions of
the sprites are being calculated directly on the GPU. The Pixi
development team is working to offload as much sprite processing as
possible on the GPU, so it’s likely that the latest version of Pixi
that you’re using will have much more feature-rich `ParticleContainer` than
what I've described here. Check the current [`ParticleContainer`
documentation](http://pixijs.download/release/docs/PIXI.particles.ParticleContainer.html) for details.

Where you create a `ParticleContainer`, there are four optional
arguments you can provide: `size`, `properties`, `batchSize` and `autoResize`.
```js
let superFastSprites = new ParticleContainer(maxSize, properties, batchSize, autoResize);
```
The default value for `maxSize` is 1500. So, if you need to contain more
sprites, set it to a higher number. The `properties` argument is an object
with 5 Boolean values you can set: `scale`, `position`, `rotation`, `uvs` and
`alphaAndTint`. The default value of `position` is `true`, but all the others
are set to `false`. That means that if you want change the `rotation`,
`scale`, `tint`, or `uvs` of sprite in the `ParticleContainer`, you
have to set those properties to `true`, like this:
```js
let superFastSprites = new ParticleContainer(
  size, 
  {
    rotation: true,
    alphaAndtint: true,
    scale: true,
    uvs: true
  }
);
```
But, if you don't think you'll need to use these properties, keep them
set to `false` to squeeze out the maximum amount of performance.

What's the `uvs` property? Only set it to `true` if you have particles
which change their textures while they're being animated. (All the
sprite's textures will also need to be on the same tileset image for
this to work.) 

(Note: **UV mapping** is a 3D graphics display term that refers to
the `x` and `y` coordinates of the texture (the image) that is being
mapped onto a 3D surface. `U` is the `x` axis and `V` is the `y` axis.
WebGL already uses `x`, `y` and `z` for 3D spatial positioning, so `U`
and `V` were chosen to represent `x` and `y` for 2D image textures.)

(I'm not sure what exactly what those last two optional arguments, `batchSize` and `autoResize`, so if anyone knows, please us know in the Issues!)

<a id='graphic'></a>
Pixi's Graphic Primitives
-------------------------

Using image textures is one of the most useful ways of making sprites,
but Pixi also has its own low-level drawing tools. You can use them to
make rectangles, shapes, lines, complex polygons and text. And,
fortunately, it uses almost the same API as the [Canvas Drawing API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_graphics_with_canvas) so,
if you're already familiar with canvas, there’s nothing really new to
  learn. But the big advantage is that, unlike the Canvas Drawing API,
  the shapes you draw with Pixi are rendered by WebGL on the GPU. Pixi
  lets you access all that untapped performance power.
Let’s take a quick tour of how to make some basic shapes. Here are all
the shapes we'll make in the code ahead.

![Graphic primitives](/examples/images/screenshots/23.png)

<a id='rectangles'></a>
### Rectangles

All shapes are made by first creating a new instance of Pixi's
`Graphics` class (`PIXI.Graphics`).
```js
let rectangle = new Graphics();
```
Use `beginFill` with a hexadecimal color code value to set the
rectangle’ s fill color. Here’ how to set to it to light blue.
```js
rectangle.beginFill(0x66CCFF);
```
If you want to give the shape an outline, use the `lineStyle` method. Here's
how to give the rectangle a 4 pixel wide red outline, with an `alpha`
value of 1.
```js
rectangle.lineStyle(4, 0xFF3300, 1);
```
Use the `drawRect` method to draw the rectangle. Its four arguments
are `x`, `y`, `width` and `height`.
```js
rectangle.drawRect(x, y, width, height);
```
Use `endFill` when you’re done.
```js
rectangle.endFill();
```
It’s just like the Canvas Drawing API! Here’s all the code you need to
draw a rectangle, change its position, and add it to the stage.
```js
let rectangle = new Graphics();
rectangle.lineStyle(4, 0xFF3300, 1);
rectangle.beginFill(0x66CCFF);
rectangle.drawRect(0, 0, 64, 64);
rectangle.endFill();
rectangle.x = 170;
rectangle.y = 170;
app.stage.addChild(rectangle);

```
This code makes a 64 by 64 blue rectangle with a red border at an x and y position of 170.

<a id='circles'></a>
### Circles

Make a circle with the `drawCircle` method. Its three arguments are
`x`, `y` and `radius`
```js
drawCircle(x, y, radius)
```
Unlike rectangles and sprites, a circle’s x and y position is also its
center point. Here’s how to make a violet colored circle with a radius of 32 pixels.
```js
let circle = new Graphics();
circle.beginFill(0x9966FF);
circle.drawCircle(0, 0, 32);
circle.endFill();
circle.x = 64;
circle.y = 130;
app.stage.addChild(circle);
```
<a id='ellipses'></a>
### Ellipses
As a one-up on the Canvas Drawing API, Pixi lets you draw an ellipse
with the `drawEllipse` method.
```js
drawEllipse(x, y, width, height);
```
The x/y position defines the ellipse’s top left corner (imagine that
the ellipse is surrounded by an invisible rectangular bounding box -
the top left corner of that box will represent the ellipse's x/y
anchor position). Here’s a yellow ellipse that’s 50 pixels wide and 20 pixels high.
```js
let ellipse = new Graphics();
ellipse.beginFill(0xFFFF00);
ellipse.drawEllipse(0, 0, 50, 20);
ellipse.endFill();
ellipse.x = 180;
ellipse.y = 130;
app.stage.addChild(ellipse);
```
<a id='roundedrect'></a>
### Rounded rectangles

Pixi also lets you make rounded rectangles with the `drawRoundedRect`
method. The last argument, `cornerRadius` is a number in pixels that
determines by how much the corners should be rounded.
```js
drawRoundedRect(x, y, width, height, cornerRadius)
```
Here's how to make a rounded rectangle with a corner radius of 10
pixels.
```js
let roundBox = new Graphics();
roundBox.lineStyle(4, 0x99CCFF, 1);
roundBox.beginFill(0xFF9933);
roundBox.drawRoundedRect(0, 0, 84, 36, 10)
roundBox.endFill();
roundBox.x = 48;
roundBox.y = 190;
app.stage.addChild(roundBox);
```
<a id='lines'></a>
### Lines

You've seen in the examples above that the `lineStyle` method lets you
define a line.  You can use the `moveTo` and `lineTo` methods to draw the
start and end points of the line, in just the same way you can with the Canvas
Drawing API. Here’s how to draw a 4 pixel wide, white diagonal line.
```js
let line = new Graphics();
line.lineStyle(4, 0xFFFFFF, 1);
line.moveTo(0, 0);
line.lineTo(80, 50);
line.x = 32;
line.y = 32;
app.stage.addChild(line);
```
`PIXI.Graphics` objects, like lines, have `x` and `y` values, just
like sprites, so you can position them anywhere on the stage after
you've drawn them.

<a id='polygons'></a>
### Polygons

You can join lines together and fill them with colors to make complex
shapes using the `drawPolygon` method. `drawPolygon`'s argument is a
path array of x/y points that define the positions of each point on the
shape.
```js
let path = [
  point1X, point1Y,
  point2X, point2Y,
  point3X, point3Y
];

graphicsObject.drawPolygon(path);
```
`drawPolygon` will join those three points together to make the shape.
Here’s how to use `drawPolygon` to connect three lines together to
make a red triangle with a blue border. The triangle is drawn at
position 0,0 and then moved to its position on the stage using its
`x` and `y` properties.
```js
let triangle = new Graphics();
triangle.beginFill(0x66FF33);

//Use `drawPolygon` to define the triangle as
//a path array of x/y positions

triangle.drawPolygon([
    -32, 64,             //First point
    32, 64,              //Second point
    0, 0                 //Third point
]);

//Fill shape's color
triangle.endFill();

//Position the triangle after you've drawn it.
//The triangle's x/y position is anchored to its first point in the path
triangle.x = 180;
triangle.y = 22;

app.stage.addChild(triangle);
```
<a id='text'></a>

Displaying text
---------------

Use a `Text` object (`PIXI.Text`) to display text on the stage. In its simplest form, you can do it like this:
```js
let message = new Text("Hello Pixi!");
app.stage.addChild(message);
```

This will display the words, "Hello, Pixi" on the canvas. Pixi’s Text objects inherit from the `Sprite` class, so they
contain all the same properties like `x`, `y`, `width`, `height`,
`alpha`, and `rotation`. Position and resize text on the stage just like you would any other sprite. For example, you could use `position.set` to set the `message`'s `x` and `y` position like this:
```js
message.position.set(54, 96);
```

![Displaying text](/examples/images/screenshots/24.png)

That will give you basic, unstyled text. But if you want to get fancier, use Pixi's `TextStyle` function to define custom text styling. Here's how:

```js
let style = new TextStyle({
  fontFamily: "Arial",
  fontSize: 36,
  fill: "white",
  stroke: '#ff3300',
  strokeThickness: 4,
  dropShadow: true,
  dropShadowColor: "#000000",
  dropShadowBlur: 4,
  dropShadowAngle: Math.PI / 6,
  dropShadowDistance: 6,
});
``` 
That creates a new `style` object containing all the text styling that you'd like to use. For a complete list of all the style properties you can use, [see here](http://pixijs.download/release/docs/PIXI.TextStyle.html).

To apply the style to the text, add the `style` object as the `Text` function's second argument, like this:
```js
let message = new Text("Hello Pixi!", style);
``` 
![Displaying text](/examples/images/screenshots/24.5.png)

If you want to change the content of a text object after you've
created it, use the `text` property.
```js
message.text = "Text changed!";
```
Use the `style` property if you want to redefine the style properties.
```js
message.style = {fill: "black", font: "16px PetMe64"};
```

Pixi makes text objects by using the Canvas Drawing API to
render the text to an invisible and temporary canvas
element. It then turns the canvas into a WebGL texture so that it
can be mapped onto a sprite. That’s why the text’s color needs to be
wrapped in a string: it’s a Canvas Drawing API color value. As with
any canvas color values, you can use words for common colors like
“red” or “green”, or use rgba, hsla or hex values.

Pixi can also wrap long lines of text. Set the text’s `wordWrap` style
property to `true`, and then set `wordWrapWidth` to the maximum length
in pixels, that the line of text should be. Use the `align` property
to set the alignment for multi-line text.
```js
message.style = {wordWrap: true, wordWrapWidth: 100, align: center};
```
(Note: `align` doesn't affect single line text.)

If you want to use a custom font file, use the CSS `@font-face` rule
to link the font file to the HTML page where your Pixi application is
running.
```js
@font-face {
  font-family: "fontFamilyName";
  src: url("fonts/fontFile.ttf");
}
```
Add this `@font-face` rule to your HTML page's CSS style sheet.

[Pixi also has support for bitmap
fonts](http://pixijs.download/release/docs/PIXI.extras.BitmapText.html). You
can use Pixi's loader to load Bitmap font XML files, the same way you
load JSON or image files.

<a id='collision'></a>
Collision detection
--------------------------

You now know how to make a huge variety of graphics objects, but what
can you do with them? A fun thing to do is to build a simple **collision
detection** system. You can use a custom function called
`hitTestRectangle` that checks whether any two rectangular Pixi sprites are
touching.
```js
hitTestRectangle(spriteOne, spriteTwo)
```
if they overlap, `hitTestRectangle` will return `true`. You can use `hitTestRectangle` with an `if` statement to check for a collision between two sprites like this:
```js
if (hitTestRectangle(cat, box)) {
  //There's a collision
} else {
  //There's no collision
}
```
As you'll see, `hitTestRectangle` is the front door into the vast universe of game design.

Run the `collisionDetection.html` file in the `examples` folder for a
working example of how to use `hitTestRectangle`. Use the arrow keys
to move the cat. If the cat hits the box, the box becomes red
and "Hit!" is displayed by the text object.

![Displaying text](/examples/images/screenshots/25.png)

You've already seen all the code that creates all these elements, as
well as the
keyboard control system that makes the cat move. The only new thing is the
way `hitTestRectangle` is used inside the `play` function to check for a
collision.
```js
function play(delta) {

  //use the cat's velocity to make it move
  cat.x += cat.vx;
  cat.y += cat.vy;

  //check for a collision between the cat and the box
  if (hitTestRectangle(cat, box)) {

    //if there's a collision, change the message text
    //and tint the box red
    message.text = "hit!";
    box.tint = 0xff3300;

  } else {

    //if there's no collision, reset the message
    //text and the box's color
    message.text = "No collision...";
    box.tint = 0xccff99;
  }
}
```
Because the `play` function is being called by the game loop 60 times
per second, this `if` statement is constantly checking for a collision
between the cat and the box. If `hitTestRectangle` is `true`, the
text `message` object uses `text` to display "Hit":
```js
message.text = "Hit!";
```
The color of the box is then changed from green to red by setting the
box's `tint` property to the hexadecimal red value.
```js
box.tint = 0xff3300;
```
If there's no collision, the message and box are maintained in their
original states:
```js
message.text = "No collision...";
box.tint = 0xccff99;
```
This code is pretty simple, but suddenly you've created an interactive
world that seems to be completely alive. It's almost like magic! And, perhaps
surprisingly, you now have all the skills you need to start making
games with Pixi!

<a id='hittest'></a>
### The hitTestRectangle function

But what about the `hitTestRectangle` function? What does it do, and
how does it work? The details of how collision detection algorithms
like this work is a little bit outside the scope of this tutorial. (If you really want to know, you can find out how [this book](https://www.apress.com/us/book/9781430258001).)
The most important thing is that you know how to use it. But, just for
your reference, and in case you're curious, here's the complete
`hitTestRectangle` function definition. Can you figure out from the
comments what it's doing?
```js
function hitTestRectangle(r1, r2) {

  //Define the variables we'll need to calculate
  let hit, combinedHalfWidths, combinedHalfHeights, vx, vy;

  //hit will determine whether there's a collision
  hit = false;

  //Find the center points of each sprite
  r1.centerX = r1.x + r1.width / 2;
  r1.centerY = r1.y + r1.height / 2;
  r2.centerX = r2.x + r2.width / 2;
  r2.centerY = r2.y + r2.height / 2;

  //Find the half-widths and half-heights of each sprite
  r1.halfWidth = r1.width / 2;
  r1.halfHeight = r1.height / 2;
  r2.halfWidth = r2.width / 2;
  r2.halfHeight = r2.height / 2;

  //Calculate the distance vector between the sprites
  vx = r1.centerX - r2.centerX;
  vy = r1.centerY - r2.centerY;

  //Figure out the combined half-widths and half-heights
  combinedHalfWidths = r1.halfWidth + r2.halfWidth;
  combinedHalfHeights = r1.halfHeight + r2.halfHeight;

  //Check for a collision on the x axis
  if (Math.abs(vx) < combinedHalfWidths) {

    //A collision might be occurring. Check for a collision on the y axis
    if (Math.abs(vy) < combinedHalfHeights) {

      //There's definitely a collision happening
      hit = true;
    } else {

      //There's no collision on the y axis
      hit = false;
    }
  } else {

    //There's no collision on the x axis
    hit = false;
  }

  //`hit` will be either `true` or `false`
  return hit;
};

```
<a id='casestudy'></a>
Case study: Treasure Hunter
---------------

I've told you that you now have all the skills you need to start
making games. What? You don't believe me? Let me prove it to you! Let’s take a
close at how to make a simple object collection and enemy
avoidance game called **Treasure Hunter**. (You'll find it in the `examples`
folder.)

![Treasure Hunter](/examples/images/screenshots/26.png)

Treasure Hunter is a good example of one of the simplest complete
games you can make using the tools you've learnt so far. Use the
keyboard arrow
keys to help the explorer find the treasure and carry it to the exit.
Six blob monsters move up and down between the dungeon walls, and if
they hit the explorer he becomes semi-transparent and the health meter
at the top right corner shrinks. If all the health is used up, “You
Lost!” is displayed on the stage; if the explorer reaches the exit with
the treasure, “You Won!” is displayed. Although it’s a basic
prototype, Treasure Hunter contains most of the elements you’ll find
in much bigger games: texture atlas graphics, interactivity,
collision, and multiple game scenes. Let’s go on a tour of how the
game was put together so that you can use it as a starting point for one of your own games.

### The code structure

Open the `treasureHunter.html` file and you'll see that all the game
code is in one big file. Here's a birds-eye view of how all the code is
organized.

```js
//Setup Pixi and load the texture atlas files - call the `setup`
//function when they've loaded

function setup() {
  //Initialize the game sprites, set the game `state` to `play`
  //and start the 'gameLoop'
}

function gameLoop(delta) {
  //Runs the current game `state` in a loop and renders the sprites
}

function play(delta) {
  //All the game logic goes here
}

function end() {
  //All the code that should run at the end of the game
}

//The game's helper functions:
//`keyboard`, `hitTestRectangle`, `contain` and `randomInt`
```
Use this as your world map to the game as we look at how each
section works.

<a id='initialize'></a>
### Initialize the game in the setup function

As soon as the texture atlas images have loaded, the `setup` function
runs. It only runs once, and lets you perform
one-time setup tasks for your game. It's a great place to create and initialize
objects, sprites, game scenes, populate data arrays or parse
loaded JSON game data.

Here's an abridged view of the `setup` function in Treasure Hunter,
and the tasks that it performs.

```js
function setup() {
  //Create the `gameScene` group
  //Create the `door` sprite
  //Create the `player` sprite
  //Create the `treasure` sprite
  //Make the enemies
  //Create the health bar
  //Add some text for the game over message
  //Create a `gameOverScene` group
  //Assign the player's keyboard controllers

  //set the game state to `play`
  state = play;

  //Start the game loop 
  app.ticker.add(delta => gameLoop(delta));
}

```
The last two lines of code, `state = play;` and `gameLoop()` are perhaps
the most important. Adding the `gameLoop` to Pixi's ticker switches on the game's engine,
and causes the `play` function to be called in a continuous loop. But before we look at how that works, let's see what the
specific code inside the `setup` function does.

<a id='gamescene'></a>
#### Creating the game scenes

The `setup` function creates two `Container` groups called
`gameScene` and `gameOverScene`. Each of these are added to the stage.
```js
gameScene = new Container();
app.stage.addChild(gameScene);

gameOverScene = new Container();
app.stage.addChild(gameOverScene);

```
All of the sprites that are part of the main game are added to the
`gameScene` group. The game over text that should be displayed at the
end of the game is added to the `gameOverScene` group.

![Displaying text](/examples/images/screenshots/27.png)

Although it's created in the `setup` function, the `gameOverScene`
shouldn't be visible when the game first starts, so its `visible`
property is initialized to `false`.
```js
gameOverScene.visible = false;
```
You'll see ahead that, when the game ends, the `gameOverScene`'s `visible`
property will be set to `true` to display the text that appears at the
end of the game.

<a id='makingdungon'></a>
#### Making the dungeon, door, explorer and treasure

The player, exit door, treasure chest and the dungeon background image
are all sprites made from texture atlas frames. Very importantly,
they're all added as children of the `gameScene`.
```js
//Create an alias for the texture atlas frame ids
id = resources["images/treasureHunter.json"].textures;

//Dungeon
dungeon = new Sprite(id["dungeon.png"]);
gameScene.addChild(dungeon);

//Door
door = new Sprite(id["door.png"]);
door.position.set(32, 0);
gameScene.addChild(door);

//Explorer
explorer = new Sprite(id["explorer.png"]);
explorer.x = 68;
explorer.y = gameScene.height / 2 - explorer.height / 2;
explorer.vx = 0;
explorer.vy = 0;
gameScene.addChild(explorer);

//Treasure
treasure = new Sprite(id["treasure.png"]);
treasure.x = gameScene.width - treasure.width - 48;
treasure.y = gameScene.height / 2 - treasure.height / 2;
gameScene.addChild(treasure);
```
Keeping them together in the `gameScene` group will make it easy for
us to hide the `gameScene` and display the `gameOverScene` when the game is finished.

<a id='makingblob'></a>
#### Making the blob monsters

The six blob monsters are created in a loop. Each blob is given a
random initial position and velocity. The vertical velocity is
alternately multiplied by `1` or `-1` for each blob, and that’s what
causes each blob to move in the opposite direction to the one next to
it. Each blob monster that's created is pushed into an array called
`blobs`.
```js
let numberOfBlobs = 6,
    spacing = 48,
    xOffset = 150,
    speed = 2,
    direction = 1;

//An array to store all the blob monsters
blobs = [];

//Make as many blobs as there are `numberOfBlobs`
for (let i = 0; i < numberOfBlobs; i++) {

  //Make a blob
  let blob = new Sprite(id["blob.png"]);

  //Space each blob horizontally according to the `spacing` value.
  //`xOffset` determines the point from the left of the screen
  //at which the first blob should be added
  let x = spacing * i + xOffset;

  //Give the blob a random `y` position
  let y = randomInt(0, stage.height - blob.height);

  //Set the blob's position
  blob.x = x;
  blob.y = y;

  //Set the blob's vertical velocity. `direction` will be either `1` or
  //`-1`. `1` means the enemy will move down and `-1` means the blob will
  //move up. Multiplying `direction` by `speed` determines the blob's
  //vertical direction
  blob.vy = speed * direction;

  //Reverse the direction for the next blob
  direction *= -1;

  //Push the blob into the `blobs` array
  blobs.push(blob);

  //Add the blob to the `gameScene`
  gameScene.addChild(blob);
}

```
<a id='healthbar'></a>
#### Making the health bar

When you play Treasure Hunter you'll notice that when the explorer touches
one of the enemies, the width of the health bar at the top right
corner of the screen decreases. How was this health bar made? It's
just two overlapping rectangles at exactly the same position: a black rectangle behind, and
a red rectangle in front. They're grouped together into a single `healthBar`
group. The `healthBar` is then added to the `gameScene` and positioned
on the stage.
```js
//Create the health bar
healthBar = new PIXI.Container();
healthBar.position.set(stage.width - 170, 4)
gameScene.addChild(healthBar);

//Create the black background rectangle
let innerBar = new PIXI.Graphics();
innerBar.beginFill(0x000000);
innerBar.drawRect(0, 0, 128, 8);
innerBar.endFill();
healthBar.addChild(innerBar);

//Create the front red rectangle
let outerBar = new PIXI.Graphics();
outerBar.beginFill(0xFF3300);
outerBar.drawRect(0, 0, 128, 8);
outerBar.endFill();
healthBar.addChild(outerBar);

healthBar.outer = outerBar;
```
You can see that a property called `outer` has been added to the
`healthBar`. It just references the `outerBar` (the red rectangle) so that it will be convenient to access later.
```js
healthBar.outer = outerBar;
```
You don't have to do this; but, hey why not! It means that if you want
to control the width of the red `outerBar`, you can write some smooth code that looks like this:
```js
healthBar.outer.width = 30;
```
That's pretty neat and readable, so we'll keep it!

<a id='message'></a>
#### Making the message text

When the game is finished, some text displays “You won!” or “You
lost!”, depending on the outcome of the game. This is made using a
text sprite and adding it to the `gameOverScene`. Because the
`gameOverScene`‘s `visible` property is set to `false` when the game
starts, you can’t see this text. Here’s the code from the `setup`
function that creates the message text and adds it to the
`gameOverScene`.
```js
let style = new TextStyle({
    fontFamily: "Futura",
    fontSize: 64,
    fill: "white"
  });
message = new Text("The End!", style);
message.x = 120;
message.y = app.stage.height / 2 - 32;
gameOverScene.addChild(message);
```
<a id='playing'></a>
### Playing the game

All the game logic and the code that makes the sprites move happens
inside the `play` function, which runs in a continuous loop. Here's an
overview of what the `play` function does
```js
function play(delta) {
  //Move the explorer and contain it inside the dungeon
  //Move the blob monsters
  //Check for a collision between the blobs and the explorer
  //Check for a collision between the explorer and the treasure
  //Check for a collision between the treasure and the door
  //Decide whether the game has been won or lost
  //Change the game `state` to `end` when the game is finished
}
```
Let's find out how all these features work.

<a id='movingexplorer'></a>
### Moving the explorer

The explorer is controlled using the keyboard, and the code that does
that is very similar to the keyboard control code you learnt earlier.
The `keyboard` objects modify the explorer’s velocity, and that
velocity is added to the explorer’s position inside the `play`
function.
```js
explorer.x += explorer.vx;
explorer.y += explorer.vy;
```
<a id='containingmovement'></a>
#### Containing movement

But what's new is that the explorer's movement is contained inside the walls of the
dungeon. The green outline shows the limits of the explorer's
movement.

![Displaying text](/examples/images/screenshots/28.png)

That's done with the help of a custom function called
`contain`.
```js
contain(explorer, {x: 28, y: 10, width: 488, height: 480});
```
`contain` takes two arguments. The first is the sprite you want to keep
contained. The second is any object with `x`, `y`, `width` and
`height` properties that define a rectangular area. In this example,
the containing object defines an area that's just slightly offset
from, and smaller than, the stage. It matches the dimensions of the dungeon
walls.

Here's the `contain` function that does all this work. The function checks
to see if the sprite has crossed the boundaries of the containing
object. If it has, the code moves the sprite back into that boundary.
The `contain` function also returns a `collision` variable with the
value "top", "right", "bottom" or "left", depending on which side of
the boundary the sprite hit. (`collision` will be `undefined` if the
sprite didn't hit any of the boundaries.)
```js
function contain(sprite, container) {

  let collision = undefined;

  //Left
  if (sprite.x < container.x) {
    sprite.x = container.x;
    collision = "left";
  }

  //Top
  if (sprite.y < container.y) {
    sprite.y = container.y;
    collision = "top";
  }

  //Right
  if (sprite.x + sprite.width > container.width) {
    sprite.x = container.width - sprite.width;
    collision = "right";
  }

  //Bottom
  if (sprite.y + sprite.height > container.height) {
    sprite.y = container.height - sprite.height;
    collision = "bottom";
  }

  //Return the `collision` value
  return collision;
}
```
You'll see how the `collision` return value will be used in the code
ahead to make the blob monsters bounce back and forth between the top
and bottom dungeon walls.

<a id='movingmonsters'></a>
### Moving the monsters

The `play` function also moves the blob monsters, keeps them contained
inside the dungeon walls, and checks each one for a collision with the
player. If a blob bumps into the dungeon’s top or bottom walls, its
direction is reversed. All this is done with the help of a `forEach` loop
which iterates through each of `blob` sprites in the `blobs` array on
every frame.
```js
blobs.forEach(function(blob) {

  //Move the blob
  blob.y += blob.vy;

  //Check the blob's screen boundaries
  let blobHitsWall = contain(blob, {x: 28, y: 10, width: 488, height: 480});

  //If the blob hits the top or bottom of the stage, reverse
  //its direction
  if (blobHitsWall === "top" || blobHitsWall === "bottom") {
    blob.vy *= -1;
  }

  //Test for a collision. If any of the enemies are touching
  //the explorer, set `explorerHit` to `true`
  if(hitTestRectangle(explorer, blob)) {
    explorerHit = true;
  }
});

```
You can see in this code above how the return value of the `contain`
function is used to make the blobs bounce off the walls. A variable
called `blobHitsWall` is used to capture the return value:
```js
let blobHitsWall = contain(blob, {x: 28, y: 10, width: 488, height: 480});
```
`blobHitsWall` will usually be `undefined`. But if the blob hits the
top wall, `blobHitsWall` will have the value "top". If the blob hits
the bottom wall, `blobHitsWall` will have the value "bottom". If
either of these cases are `true`, you can reverse the blob's direction
by reversing its velocity. Here's the code that does this:
```js
if (blobHitsWall === "top" || blobHitsWall === "bottom") {
  blob.vy *= -1;
}
```
Multiplying the blob's `vy` (vertical velocity) value by `-1` will flip
the direction of its movement.

<a id='checkingcollisions'></a>
### Checking for collisions

The code in the loop above uses `hitTestRectangle` to figure
out if any of the enemies have touched the explorer.
```js
if(hitTestRectangle(explorer, blob)) {
  explorerHit = true;
}
```
If `hitTestRectangle` returns `true`, it means there’s been a collision
and a variable called `explorerHit` is set to `true`. If `explorerHit`
is `true`, the `play` function makes the explorer semi-transparent
and reduces the width of the `health` bar by 1 pixel.
```js
if(explorerHit) {

  //Make the explorer semi-transparent
  explorer.alpha = 0.5;

  //Reduce the width of the health bar's inner rectangle by 1 pixel
  healthBar.outer.width -= 1;

} else {

  //Make the explorer fully opaque (non-transparent) if it hasn't been hit
  explorer.alpha = 1;
}

```
If  `explorerHit` is `false`, the explorer's `alpha` property is
maintained at 1, which makes it fully opaque.

The `play` function also checks for a collision between the treasure
chest and the explorer. If there’s a hit, the `treasure` is set to the
explorer’s position, with a slight offset. This makes it look like the
explorer is carrying the treasure.

![Displaying text](/examples/images/screenshots/29.png)

Here's the code that does this:

```js
if (hitTestRectangle(explorer, treasure)) {
  treasure.x = explorer.x + 8;
  treasure.y = explorer.y + 8;
}
```
<a id='reachingexit'></a>
### Reaching the exit door and ending the game

There are two ways the game can end: You can win if you carry the
treasure to the exit, or you can lose if you run out of health.

To win the game, the treasure chest just needs to touch the exit door. If
that happens, the game `state` is set to `end`, and the `message` text
displays "You won".
```js
if (hitTestRectangle(treasure, door)) {
  state = end;
  message.text = "You won!";
}
```
If you run out of health, you lose the game. The game `state` is also
set to `end` and the `message` text displays "You Lost!"
```js
if (healthBar.outer.width < 0) {
  state = end;
  message.text = "You lost!";
}
```
But what does this mean?
```js
state = end;
```
You'll remember from earlier examples that the `gameLoop` is constantly updating a function called
`state` at 60 times per second. Here's the `gameLoop`that does this:
```js
function gameLoop(delta){

  //Update the current game state:
  state(delta);
}
```
You'll also remember that we initially set the value of
`state` to `play`, which is why the `play` function runs in a loop.
By setting `state` to `end` we're telling the code that we want
another function, called `end` to run in a loop. In a bigger game you
could have a `tileScene` state, and states for each game level, like
`leveOne`, `levelTwo` and `levelThree`.

So what is that `end` function? Here it is!
```js
function end() {
  gameScene.visible = false;
  gameOverScene.visible = true;
}
```
It just flips the visibility of the game scenes. This is what hides
the `gameScene` and displays the `gameOverScene` when the game ends.

This is a really simple example of how to switch a game's state, but
you can have as many game states as you like in your games, and fill them
with as much code as you need. Just change the value of `state` to
whatever function you want to run in a loop.

And that’s really all there is to Treasure Hunter! With a little more work you could turn this simple prototype into a full game – try it!

<a id='spriteproperties'></a>
More about sprites
-----------------------------

You've learnt how to use quite a few useful sprite properties so far, like `x`, `y`,
`visible`, and `rotation` that give you a lot of control over a
sprite's position and appearance. But Pixi Sprites also have many more
useful properties that are fun to play with. [Here's the full list.](http://pixijs.download/release/docs/PIXI.Sprite.html)

How does Pixi’s class inheritance system work? ([What is a **class**
and what is **inheritance**? Click this link to find out.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)) Pixi’s sprites are
built on an inheritance model that follows this chain:
```
DisplayObject > Container > Sprite
```
Inheritance just means that the classes later in the chain use
properties and methods from classes earlier in the chain. That means that even though `Sprite` is the last class in the chain, has all the same properties as `DisplayObject` and `Container`, in addition to its own unique properties.
The most basic class is `DisplayObject`. Anything that’s a
`DisplayObject` can be rendered on the stage. `Container`
is the next class in the inheritance chain. It allows `DisplayObject`s
to act as containers for other `DisplayObject`s. Third up the chain is
the `Sprite` class. Sprites can both be displayed on the stage and be containers for other sprites.

<a id='takingitfurther'></a>
Taking it further
-----------------

Pixi can do a lot, but it can't do everything! If you want to start
making games or complex interactive applications with Pixi, you'll need
to use some helper libraries:

- [Bump](https://github.com/kittykatattack/bump): A complete suite of 2D collision functions for games.
- [Tink](https://github.com/kittykatattack/tink): Drag-and-drop, buttons, a universal pointer and other
  helpful interactivity tools.
- [Charm](https://github.com/kittykatattack/charm): Easy-to-use tweening animation effects for Pixi sprites.
- [Dust](https://github.com/kittykatattack/dust): Particle effects for creating things like explosions, fire
  and magic.
- [Sprite Utilities](https://github.com/kittykatattack/spriteUtilities): Easier and more intuitive ways to
  create and use Pixi sprites, as well adding a state machine and
  animation player. Makes working with Pixi a lot more fun.
- [Sound.js](https://github.com/kittykatattack/sound.js): A micro-library for loading, controlling and generating
  sound and music effects. Everything you need to add sound to games.
- [Smoothie](https://github.com/kittykatattack/smoothie): Ultra-smooth sprite animation using true delta-time interpolation. It also lets you specify the fps (frames-per-second) at which your game or application runs, and completely separates your sprite rendering loop from your application logic loop.

You can find out how to use all these libraries with Pixi in the book 
[Learn PixiJS](http://www.springer.com/us/book/9781484210956).

<a id='hexi'></a>
### Hexi

Do you want to use all the functionality of those libraries, but don't
want the hassle of integrating them yourself? Use **Hexi**: a complete
development environment for building games and interactive
applications:

https://github.com/kittykatattack/hexi

It bundles the best version of Pixi (the latest **stable** one) with all these 
libraries (and more!) for a simple and fun way to make games. Hexi also
lets you access the global `PIXI` object directly, so you can write
low-level Pixi code directly in a Hexi application, and optionally choose to use as many or
as few of Hexi's extra conveniences as you need.

<a id='babylonjs'></a>
### BabylonJS

Pixi is great for 2D, but it can't do 3D. When you're ready to step into the third dimension, the most feature rich, easy-to-use 3D game development platform for the web is [BabylonJS](https://www.babylonjs.com). It's a great next step for taking your skills further.

<a id='supportingthisproject'></a>
Please help to support this project!
-------------------

Buy the book! Incredibly, someone actually paid me to finish writing this tutorial
and turn it into a book! 

[Learn PixiJS](http://www.springer.com/us/book/9781484210956)

(And it's not just some junky "e-book", but a real, heavy, paper book, published by Springer,
the world's largest publisher! That means you can invite your friends
over, set it on fire, and roast marshmallows!!) There's 80% more
content than what's in this tutorial, and it's
packed full of all the essential techniques you need to know to use
Pixi to make all kinds of interactive applications and games.

Find out how to:

- Make animated game characters.
- Create a full-featured animation state player.
- Dynamically animate lines and shapes.
- Use tiling sprites for infinite parallax scrolling.
- Use blend modes, filters, tinting, masks, video, and render textures.
- Produce content for multiple resolutions.
- Create interactive buttons.
- Create a flexible drag and drop interface for Pixi.
- Create particle effects.
- Build a stable software architectural model that will scale to any size.
- Make complete games.

And, as a bonus, all the code is written entirely in the latest version of
JavaScript: ES6/2015. And, although the book's code is based on Pixi v3.x, it all works just fine with the latest version of Pixi 4.x!

If you want to support this project, please buy a copy of this book,
and buy another copy for your mom!

Or, make a generous donation to: http://www.msf.org

