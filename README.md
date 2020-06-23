# simple-painter [![npm](https://img.shields.io/npm/v/simple-painter.svg)](https://www.npmjs.com/package/simple-painter)
JavaScript painting plugin in a browser. <br>
Simple Painter based on HTML5/Canvas.
<br />
<br />

## Installing
```bash
$ npm install simple-painter
```
<br />
<br />

## Example
Please refer to the example/index.ts file.
- [https://goldenthumb.github.io/simple-painter](https://goldenthumb.github.io/simple-painter)
```bash
$ git clone https://github.com/goldenthumb/simple-painter.git
$ cd simple-painter
$ npm install
$ npm run start

Now open this URL in your browser: http://localhost:1234/
```
<br />
<br />

## API
### new SimplePainter(options)
Create instance.
```js
/**
 * @param {object} [options]
 * @param {HTMLCanvasElement} options.canvas
 * @param {width} [options.width]
 * @param {height} [options.height]
 * @param {boolean} [options.drawMouse]
 * @param {'freeLine'|'straightLine'|'rectangle'|'ellipse'|'arrow'} [options.type]
 * @param {string|CanvasGradient|CanvasPattern} [options.color]
 * @param {number} [options.thickness]
 * @param {CanvasLineCap} [options.lineCap]
 */

const painter = new SimplePainter({ canvas });
```

#### options
```
{   
    canvas,             // HTMLCanvasElement.
    width,              // Canvas width.
    height,             // Canvas height.
    drawMouse: true,    // allow draw by mouse or touch. Default is true
    type: 'freeLine',   // draw type. Default is 'freeLine'
    color: 'red',       // draw color. Default is 'red'
    thickness: 3,       // draw thickness. Default is 3
    lineCap: 'square',  // draw lineCap. Default is 'square'
}
```
<br />

#### painter.setOptions(options)
Change draw option. (by mouse or touch)

```js
painter.setOptions({
    type: 'rectangle',
    color: 'blue',
    thickness: 10,
    lineCap: 'round',
})
```
<br />

#### painter.setSize(size)
Change canvas size.

```js
painter.setSize({
    width: 500,
    height: 500,
})
```
<br />

#### painter.draw(Figure)
Add draw figure and render.

```js
import { FreeLine, Rectangle, Ellipse, StraightLine } from 'simple-painter';

painter.draw(
    new FreeLine({
        color: 'red',
        thickness: 3,
        lineCap: 'round',
    }, [
        { x: 0.537866461275263, y: 0.24183928841850494 },
        { x: 0.655767612752637, y: 0.14106861275263723 },
        { x: 0.654859612752637, y: 0.14429961275263721 },
        { x: 0.640327612752637, y: 0.19599561275263723 },
        { x: 0.638516127526372, y: 0.20245761275263723 },
    ])
);

painter.draw(
    new Rectangle({
        color: 'blue',
        thickness: 10,
        lineCap: 'round',
    }, {
        x: 0.45800570994602724,
        y: 0.29400569993626097
    }, {
        x: 0.6980057245944656,
        y: 0.46000571006809754
    })
);

painter.draw(
    new Ellipse({
        color: 'green',
        thickness: 2,
        lineCap: 'round'
    }, {
        x: 0.589660464410864,
        y: 0.39722129782530574
    }, {
        x: 0.8147651703463574,
        y: 0.5984210792366761
    })
);

painter.draw(
    new StraightLine({
        color: 'purple',
        thickness: 5,
        lineCap: 'square',
    }, {
        x: 0.589660464410864,
        y: 0.39722129782530574
    }, {
        x: 0.8147651703463574,
        y: 0.5984210792366761
    })
);

```
<br />

#### painter.undo()
Undo draw.

```js
painter.undo();
```
<br />

#### painter.redo()
Redo draw.

```js
painter.redo();
```
<br />

#### painter.clear()
Clear draw.

```js
painter.clear();
```
<br />

#### painter.destroy()
Remove events.

```js
painter.destroy();
```
<br />

#### painter.on(eventName, listener)
Add an event listener.<br />
Returns Function to remove the event listener.
<br />

##### Events
- drawStart - Event occurs when drawing starts.
- drawing - Event occurs when drawing.
- drawEnd - Event occurs when drawing is finished.

```js
/**
 * @param {object} data
 * @param {HTMLCanvasElement} data.canvas
 * @param {MouseEvent | TouchEvent} data.origin
 * @param {{x: number, y: number}} data.relativePosition
 */
painter.on('drawStart', (data) => {
    console.log(data);
});

painter.on('drawing', (data) => {
    console.log(data);
});

painter.on('drawEnd',(data) => {
    console.log(data);
});
```

<br />

### new FreeLine(drawStyle, positions)
Create instance.
```js
/**
 * @param {object} drawStyle
 * @param {string | CanvasGradient | CanvasPattern} [drawStyle.color]
 * @param {number} [drawStyle.thickness]
 * @param {CanvasLineCap} [drawStyle.lineCap]
 * 
 * @param {{x: number; y: number}[]} positions
 */
const freeLine = new FreeLine(drawStyle, positions);
```

<br />

### new Rectangle(drawStyle, startPosition, endPosition)
Create instance.
```js
/**
 * @param {object} drawStyle
 * @param {string | CanvasGradient | CanvasPattern} [drawStyle.color]
 * @param {number} [drawStyle.thickness]
 * @param {CanvasLineCap} [drawStyle.lineCap]
 * 
 * @param {{x: number; y: number}} startPosition
 * @param {{x: number; y: number}} endPosition
 */
const rectangle = new Rectangle(drawStyle, startPosition, endPosition);
```

<br />

### new Ellipse(drawStyle, startPosition, endPosition)
Create instance.
```js
/**
 * @param {object} drawStyle
 * @param {string | CanvasGradient | CanvasPattern} [drawStyle.color]
 * @param {number} [drawStyle.thickness]
 * @param {CanvasLineCap} [drawStyle.lineCap]
 * 
 * @param {{x: number; y: number}} startPosition
 * @param {{x: number; y: number}} endPosition
 */
const ellipse = new Ellipse(drawStyle, startPosition, endPosition);
```

<br />

### new StraightLine(drawStyle, startPosition, endPosition)
Create instance.
```js
/**
 * @param {object} drawStyle
 * @param {string | CanvasGradient | CanvasPattern} [drawStyle.color]
 * @param {number} [drawStyle.thickness]
 * @param {CanvasLineCap} [drawStyle.lineCap]
 * 
 * @param {{x: number; y: number}} startPosition
 * @param {{x: number; y: number}} endPosition
 */
const straightLine = new StraightLine(drawStyle, startPosition, endPosition);
```

<br />
<br />

## License
MIT

<br />

