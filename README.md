# react-p5-wrapper

A component to integrate [P5 JS](https://p5js.org/) sketches into [React JS](https://reactjs.org/) apps.

## Demo & Examples

Live demo: [and-who.github.io/react-p5-wrapper](http://and-who.github.io/react-p5-wrapper/)

To build the examples locally, run:

```
npm install
npm start
```

Then open [`localhost:3001`](localhost:3001) in a browser.

For more details see the source code in our [examples](https://github.com/and-who/react-p5-wrapper/tree/master/example/src).

## Installation

Install the package with `npm` and save it to your project:

```
npm install react-p5-wrapper --save
```

## Usage

```js
// file:src/App.jsx
import P5Wrapper from 'react-p5-wrapper';

function App() {
  let sketch = (p5) => {
    p5.setup = () => {
      ...
    }

    p5.draw = () => {
      ...
    };
  }

  return <P5Wrapper sketch={sketch} />;
}

export default App;
```

### Properties

- `sketch`: This is the sketch script which should be executed in the p5 canvas.
- You can also add as many custom properties as you want.

In the below example you see the `myCustomRedrawAccordingToNewPropsHandler` function, which is called when the properties of a wrapper component are changed.

```js
// file:src/App.jsx
import P5Wrapper from 'react-p5-wrapper';

function App() {
  let sketch = (p5) => {
    let rotation = 0;

    p5.setup = () => p5.createCanvas(600, 400, p5.WEBGL);

    p5.myCustomRedrawAccordingToNewPropsHandler = (props) => {
      if (props.rotation) {
        rotation = (props.rotation * Math.PI) / 180;
      }
    };

    p5.draw = () => {
      p5.background(100);
      p5.normalMaterial();
      p5.noStroke();
      p5.push();
      p5.rotateY(rotation);
      p5.box(100);
      p5.pop();
    };
  }

  return <P5Wrapper sketch={sketch} rotation={rotation}/>;
}

export default App;
```

### Children

To render a component on top of the sketch, simply add it as a child of the `P5Wrapper` component.

## Development

**NOTE:** The source code for the component is in `src` directory.

To build, watch and serve the examples which will also watch the component source, run:

```
npm start
```

## License

The MIT License (MIT)

Copyright (c) 2016 Andreas Wolf and [contributors](https://github.com/and-who/react-p5-wrapper/graphs/contributors).
