# Graphics

### Reference Resources (參考資源)

* https://developer.mozilla.org/en-US/docs/Web/SVG
* https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API
* https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API

***

### Table of Contents (目錄)

* [Flat Display (平面圖形)](#flat-display-平面圖形)
  * [Shapes (形狀)](#shapes-形狀)
    * [Line (線)](#line-線)
    * [Polyline (折線)](#polyline-折線)
    * [Circle (圓形)](#circle-圓形)
    * [Ellipse (橢圓形)](#ellipse-橢圓形)
    * [Rectangle (矩形)](#rectangle-矩形)
    * [Polygon (多邊形)](#polygon-多邊形)
    * [Path (路徑)](#path-路徑)
    * [Layer (圖層)](#layer-圖層)
  * Filters (濾鏡)
    * [Blur (模糊)](#blur-模糊)
    * [Shadow (陰影)](#shadow-陰影)
    * Ripple (漣漪)
  * Gradients (漸層)
    * [Linear Gradient (線性漸層)](#linear-gradient-線性漸層)
    * [Radial Gradient (放射性漸層)](#radial-gradient-放射性漸層)
  * Transformations (變形)
    * Rotate (旋轉)
  * Animations (動畫)
  * Clip (裁切)
  * Mask (遮色片)
  * [Text (文字)](#text-文字)
  * Image (圖像)
  * Pattern (圖案)
  * Responsive (響應式)
* [Three-dimensional (立體圖形)](#three-dimensional-立體圖形)
  * Textures (材質)
  * Lighting (光源)

***

# Flat Display (平面圖形)

## Shapes (形狀)

1. Create a line (畫出一條線):

  SVG: `<line>` <br>
  Canvas: `moveTo()`, `lineTo()`

2. Create any shape that consists of only straight lines (畫出以直線為底的任何形狀):

  SVG: `<polyline>` <br>
  Canvas: `moveTo()`, `lineTo()`

3. Create a circle (畫出一個圓形):

  SVG: `<circle>` <br>
  Canvas: `arc()`

4. Create an ellipse (畫出一個橢圓形):

  SVG: `<ellipse>` <br>
  Canvas: `ellipse()`

5. Create a rectangle and variations of a rectangle shape (畫出一個多變化的矩形形狀)：

  SVG: `<rect>` <br>
  Canvas: `rect()`

6. Create a graphic that contains at least three sides (畫出一個至少包含三個面的圖形):

  SVG: `<polygon>` <br>
  Canvas: `moveTo()`, `lineTo()`

7. Define a path (定義一個路徑):

8. Define a grouping of elements (定義一個群組元素):

### Line (線)

#### SVG

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <line
    x1="30" y1="50"
    x2="120" y2="100"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/line

Round line (圓線)

```html
  <line
    [...]
    stroke-linecap="round"
  />
```

#### Canvas

```html
<canvas id="line" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#line');
const ctx = canvas.getContext('2d');

const [x1, y1] = [30, 50];
const [x2, y2] = [120, 100];

ctx.beginPath();

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.moveTo(x1, y1);
ctx.lineTo(x2, y2);

ctx.stroke();
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/moveTo <br>
https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineTo

Round line (圓線)

```js
ctx.lineCap = 'round';
```

### Polyline (折線)

#### SVG

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <polyline
    points="
      25,50
      50,50
      50,25
      75,25
      75,50
      100,50
      100,25
      125,25
      125,50
      150,50
    "
    fill-opacity="0"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/polyline

#### Canvas

```html
<canvas id="polyline" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#polyline');
const ctx = canvas.getContext('2d');

const [x1, y1] = [25, 50];
const [x2, y2] = [50, 50];
const [x3, y3] = [50, 25];
const [x4, y4] = [75, 25];
const [x5, y5] = [75, 50];
const [x6, y6] = [100, 50];
const [x7, y7] = [100, 25];
const [x8, y8] = [125, 25];
const [x9, y9] = [125, 50];
const [x10, y10] = [150, 50];

ctx.beginPath();

ctx.moveTo(x1, y1);
ctx.lineTo(x2, y2);
ctx.lineTo(x2, y2);
ctx.lineTo(x3, y3);
ctx.lineTo(x4, y4);
ctx.lineTo(x5, y5);
ctx.lineTo(x6, y6);
ctx.lineTo(x7, y7);
ctx.lineTo(x8, y8);
ctx.lineTo(x9, y9);
ctx.lineTo(x10, y10);

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/moveTo <br>
https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineTo

### Circle (圓形)

#### SVG

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <circle
    cx="50" cy="50" r="40"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

`cx` and `cy` define the x and y coordinates of the center of the circle <br>
`r` defines the radius of the circle

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/circle

#### Canvas

```html
<canvas id="circle" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#circle');
const ctx = canvas.getContext('2d');

const [cx, cy, r] = [50, 50, 40];

ctx.beginPath();

ctx.arc(cx, cy, r, 0, 2 * Math.PI);

ctx.fillStyle = '#F8BBD0';
ctx.fill();

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/arc

### Ellipse (橢圓形)

#### SVG

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <ellipse
    cx="150" cy="100" rx="100" ry="50"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/ellipse

#### Canvas

```html
<canvas id="ellipse" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#ellipse');
const ctx = canvas.getContext('2d');

const [cx, cy, rx, ry] = [150, 100, 100, 50];

ctx.beginPath();

ctx.ellipse(cx, cy, rx, ry, 0, 0, 2 * Math.PI);

ctx.fillStyle = '#F8BBD0';
ctx.fill();

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/ellipse

### Rectangle (矩形)

#### SVG

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <rect
    x="30" y="10"
    width="150" height="100"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

`x` defines the left position of the rectangle (like `margin-left`) <br>
`y` defines the top position of the rectangle (like `margin-top`) <br>
`fill` defines the background color of the rectangle (like `background-color`) <br>
`stroke-width` defines the border width of the rectangle (like `border-width`) <br>
`stroke ` defines the border color of the rectangle (like `border-color`)

Add rounded corners (加個圓角)

```html
<svg width="300" height="300">
  <rect
    x="30" y="10"
    rx="12" ry="12"
    width="150" height="100"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

`rx` and `ry` rounds the corners of the rectangle (like `border-radius`)

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/rect

#### Canvas

```html
<canvas id="rect" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#rect');
const ctx = canvas.getContext('2d');

const [x, y] = [30, 10];
const [rx, ry] = [12, 12];
const [width, height] = [150, 100];

// Create a rectangle directly (直接建立一個矩形)

ctx.beginPath();

ctx.rect(x, y, width, height);

ctx.fillStyle = '#F8BBD0';
ctx.fill();

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();

// With the way of drawing lines (用畫線的方式)

ctx.beginPath();

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.moveTo(x, y);  // Starting point (起始點)
ctx.lineTo(width + x, y);
ctx.lineTo(width + x, height + y);
ctx.lineTo(x, height + y);
ctx.lineTo(x, y);  // Back to the starting point (回到起始點)

ctx.fillStyle = '#F8BBD0';
ctx.fill();

ctx.stroke();

// Add rounded corners (加個圓角)

// Add `quadraticCurveTo(cpx, cpy, x, y)`
// `cpx` and `cpy` is the vertical turning point (`cpx` 和 `cpy` 為垂直轉折點)

ctx.moveTo(x + rx, y);  // Starting point (起始點)
ctx.lineTo(width + x - rx, y);
ctx.quadraticCurveTo(width + x, y, width + x, y + ry);
ctx.lineTo(width + x, height + y - ry);
ctx.quadraticCurveTo(width + x, height + y, width + x - rx, height + y);
ctx.lineTo(x + rx , height + y);
ctx.quadraticCurveTo(x , height + y, x, height - ry);
ctx.lineTo(x, y + ry);
ctx.quadraticCurveTo(x, y, x + rx, y);  // `x + rx, y` is back to the starting point (`x + rx, y` 是回到起始點)
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/rect <br>
https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/quadraticCurveTo

### Polygon (多邊形)

#### SVG

```html
<svg width="300" height="300">
  <polygon
    points="
      60,20
      100,40
      100,80
      60,100
      20,80
      20,40
    "
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/polygon

#### Canvas

```html
<canvas id="polygon" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#polygon');
const ctx = canvas.getContext('2d');

const [x1, y1] = [60, 20];
const [x2, y2] = [100, 40];
const [x3, y3] = [100, 80];
const [x4, y4] = [60, 100];
const [x5, y5] = [20, 80];
const [x6, y6] = [20, 40];

ctx.beginPath();

ctx.moveTo(x1, y1);
ctx.lineTo(x2, y2);
ctx.lineTo(x3, y3);
ctx.lineTo(x4, y4);
ctx.lineTo(x5, y5);
ctx.lineTo(x6, y6);

ctx.lineTo(x1, y1);

ctx.fillStyle = '#F8BBD0';
ctx.fill();

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();

// or

const points = [
  60, 20,
  100, 40,
  100, 80,
  60, 100,
  20, 80,
  20, 40
];

ctx.moveTo(points[0], points[1]);

for (let i = 2, l = points.length - 1; i < l; i += 2) {
  ctx.lineTo(points[i] , points[i + 1]);
}

ctx.lineTo(points[0], points[1]);
```

### Path (路徑)

M = moveTo (起始點), `d="M25 50"` <=> `ctx.moveTo(25, 50)`

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <path
    d="M25 50"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

```js
ctx.beginPath();

ctx.moveTo(25, 50);

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

L = lineTo (至指定點), `d="L50 75"` <=> `ctx.lineTo(50, 75)`

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <path
    d="
      M25 50
      L50 75
    "
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

```js
ctx.beginPath();

ctx.moveTo(25, 50);
ctx.lineTo(50, 75);

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

H = horizontal lineTo, `d="H100"` <=> `ctx.lineTo(100, x)`

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <path
    d="
      M25 50
      H100
    "
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

```js
ctx.beginPath();

ctx.moveTo(25, 50);
ctx.lineTo(100, 50);

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

V = vertical lineTo, `d="V100"` <=> `ctx.lineTo(x, 100)`

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <path
    d="
      M25 50
      V100
    "
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

```js
ctx.beginPath();

ctx.moveTo(25, 50);
ctx.lineTo(25, 100);

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

C = curveto

```js
bezierCurveTo()
```

S = smooth curveto

```js
bezierCurveTo()
```

Q = quadratic Bézier curve

```js
quadraticCurveTo()
```

T = smooth quadratic Bézier curveto

```js
quadraticCurveTo()
```

A = elliptical Arc

```js

```

Z = closePath (關閉路徑), `d="Z"` <=> `ctx.closePath()`<br>
Return a line from the end to the starting point (從終點連一條線回起點)

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <path
    d="
      M25 25
      L25 100
      L75 100
      Z
    "
    fill="none"
    stroke-width="3" stroke="#E91E63"
  />
</svg>
```

```js
ctx.beginPath();

ctx.moveTo(25, 25);
ctx.lineTo(25, 100);
ctx.lineTo(75, 100);
ctx.closePath();

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.stroke();
```

### Layer (圖層)

#### SVG

Single layer (單一圖層)

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <polygon id="third" [...] />
  <polygon id="second" [...] />
  <polygon id="first" [...] />
</svg>
```

Multiple layers (多個圖層)

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <g id="layer-1">
    <polygon id="third" [...] />
    <polygon id="second" [...] />
    <polygon id="first" [...] />
  </g>

  <g id="layer-2">
    <polygon [...] />
  </g>
</svg>
```

#### Canvas

```html

```

### Blur (模糊)

#### SVG

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <defs>
    <filter id="blur">
      <feGaussianBlur in="SourceGraphic" stdDeviation="7" />
    </filter>
  </defs>

  <circle
    cx="50" cy="50" r="40"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
    filter="url(#blur)"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feGaussianBlur

```html
<svg width="300" height="300" viewbox="0 0 300 300">
  <defs>
    <filter id="multi-blur" x="-75%" y="-50%" width="300%" height="200%">
      <!-- main -->
      <feGaussianBlur result="multi-blur" stdDeviation="2" />

      <!-- others -->
      <feOffset in="multi-blur" dx="20" dy="20" result="blur-1" />
      <feOffset in="multi-blur" dx="-50" dy="10" result="blur-2" />
      <feOffset in="multi-blur" dx="-30" dy="-35" result="blur-3" />
      <feOffset in="multi-blur" dx="50" dy="-15" result="blur-4" />

      <feMerge>
        <!-- others -->
        <feMergeNode in="blur-1" />
        <feMergeNode in="blur-2" />
        <feMergeNode in="blur-3" />
        <feMergeNode in="blur-4" />

        <!-- main -->
        <feMergeNode in="SourceGraphic" />
      </feMerge>
    </filter>
  </defs>

  <circle
    cx="50" cy="50" r="40"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
    filter="url(#multi-blur)"
    transform="translate(100, 100)"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feMerge

#### Canvas

```html
<canvas id="blur" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#blur');
const ctx = canvas.getContext('2d');
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/filter

### Shadow (陰影)

#### SVG

```html
<svg width="300" height="300">
  <defs>
    <filter id="shadow" x="0" y="0" width="200%" height="200%">
      <feOffset result="offOut" in="SourceAlpha" dx="12" dy="12" />
      <feGaussianBlur result="blurOut" in="offOut" stdDeviation="7" />
      <feBlend in="SourceGraphic" in2="blurOut" mode="normal" />
    </filter>
  </defs>

  <rect
    x="25" y="25"
    width="150" height="100"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
    filter="url(#shadow)"
  />
</svg>
```

```html
<svg width="300" height="300">
  <defs>
    <filter id="shadow-2">
      <feDropShadow dx="12" dy="12" stdDeviation="7" />
    </filter>
  </defs>

  <rect
    x="25" y="25"
    width="150" height="100"
    fill="#F8BBD0"
    stroke-width="3" stroke="#E91E63"
    filter="url(#shadow-2)"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/filter <br>
https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feOffset <br>
https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feGaussianBlur <br>
https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feBlend

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feDropShadow

#### Canvas

```html
<canvas id="shadow" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#shadow');
const ctx = canvas.getContext('2d');

const [dx, dy, stdDeviation] = [12, 12, 7];

const [x, y] = [25, 25];
const [width, height] = [150, 100];

ctx.shadowColor = 'black';
ctx.shadowOffsetX = dx;
ctx.shadowOffsetY = dy;
ctx.shadowBlur = stdDeviation;

ctx.fillStyle = '#F8BBD0';

ctx.lineWidth = '3';
ctx.strokeStyle = '#E91E63';

ctx.fillRect(x, y, width, height);
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/filter <br>
https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/shadowOffsetX <br>
https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/shadowOffsetY <br>
https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/shadowBlur

### Linear Gradient (線性漸層)

#### SVG

```html
<svg width="300" height="300">
  <defs>
    <linearGradient id="linear">
      <stop offset="10%" stop-color="#E91E63" />
      <stop offset="90%" stop-color="#F8BBD0" />
    </linearGradient>
  </defs>

  <rect
    x="25" y="25"
    width="150" height="100"
    fill="url(#linear)"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/linearGradient <br>
https://developer.mozilla.org/en-US/docs/Web/SVG/Element/stop

#### Canvas

```html
<canvas id="linear" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#linear');
const ctx = canvas.getContext('2d');

const offset = [10, 90];  // Percentage (百分比)

const [x, y] = [25, 25];
const [width, height] = [150, 100];

const lg = ctx.createLinearGradient(0, 0, x + width, 0);

lg.addColorStop(offset[0] / 100, '#E91E63');
lg.addColorStop(offset[1] / 100, '#F8BBD0');

ctx.fillStyle = lg;

ctx.fillRect(x, y, width, height);
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createLinearGradient

### Radial Gradient (放射性漸層)

#### SVG

```html
<svg width="300" height="300">
  <defs>
    <radialGradient id="radial">
      <stop offset="10%" stop-color="#F8BBD0" />
      <stop offset="90%" stop-color="#E91E63" />
    </radialGradient>
  </defs>

  <ellipse
    cx="150" cy="100" rx="100" ry="50"
    fill="url(#radial)"
  />
</svg>
```

https://developer.mozilla.org/en-US/docs/Web/SVG/Element/radialGradient

#### Canvas

```html
<canvas id="radial" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#radial');
const ctx = canvas.getContext('2d');

const offset = [10, 90];  // Percentage (百分比)

const [cx, cy, rx, ry] = [150, 100, 100, 50];

ctx.ellipse(cx, cy, rx, ry, 0, 0, 2 * Math.PI);

const rg = ctx.createRadialGradient(150, 100, 0, 150, 100, 100);

rg.addColorStop(offset[0] / 100, '#F8BBD0');
rg.addColorStop(offset[1] / 100, '#E91E63');

ctx.fillStyle = rg;

ctx.fill();
```

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createRadialGradient

### Text (文字)

```html
<svg width="300" height="300">
  <text x="10" y="25">Text</text>
</svg>
```

# Three-dimensional (立體圖形)

```html
<canvas id="glcanvas" width="300" height="300"></canvas>
```

```js
const canvas = document.querySelector('#glcanvas');
const gl = canvas.getContext('webgl2');
```
