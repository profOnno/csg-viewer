# csg-viewer

[![GitHub version](https://badge.fury.io/gh/jscad%2Fcsg-viewer.svg)](https://badge.fury.io/gh/jscad%2Fcsg-viewer)
[![Build Status](https://travis-ci.org/jscad/csg-viewer.svg)](https://travis-ci.org/jscad/csg-viewer)

> 3D viewer for Csg.js / Openjscad csg/cag data : small, fast, simple

This is a very early version of this viewer ! Expect changes ! 

## Overview


## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Test](#test)
- [API](#api)

## Installation

```
npm install jscad/csg-viewer
npm install jscad/scad-api
```

## Usage

```javascript
// With ES6/2015 +
import makeViewer from 'csg-viewer'
// with commonjs
// import viewer creator function
const makeViewer = require('@jscad/csg-viewer')

const viewerOptions = {
  background: [0.211, 0.2, 0.207, 1], // [1, 1, 1, 1],//54, 51, 53
  meshColor: [0.4, 0.6, 0.5, 1],
  grid: {
    show: true,
    // size: [200,200],
    // ticks: [10, 1],
    color: [1, 1, 1, 1],
    // fadeOut: true // when set to true, the grid fades out progressively in the distance
  },
  // axes: {
  //    show: true
  // },
  // rendering: {
  //   background: [1, 1, 1, 1],
  //   meshColor: [1, 0.5, 0.5, 1], // use as default face color for csgs, color for cags
  //   lightColor: [1, 1, 1, 1],
  //   lightDirection: [0.2, 0.2, 1],
  //   lightPosition: [100, 200, 100],
  //   ambientLightAmount: 0.3,
  //   diffuseLightAmount: 0.89,
  //   specularLightAmount: 0.16,
  //   materialShininess: 8.0
  // },
  camera: {
    position: [450, 550, 700]
  },
  controls: {
    // autoRotate: {
    //   enabled: false,
    //   speed: 2.0 // 30 seconds per round when fps is 60
    // },
    limits: {
      maxDistance: 1600,
      minDistance: 0.01
    }
  }
}
// create viewer
const {csgViewer, viewerDefaults, viewerState$} = makeViewer(document.body, viewerOptions)
// and just run it, providing csg/cag data

let csg = cube({ size:5, center: [1,1,0]});

csgViewer(viewerOptions, {solids: csg})

//you can also just call the viewer function again with either/or new data or new settings
csgViewer({camera: { position: [0, 100, 100] }})

csg = sphere()
csgViewer({}, {solids: csg})

// and again, with different settings: it only overrides the given settings
csgViewer({controls: {autoRotate: {enabled: true}}})

```
When using `browserify` make sure to add the right flags, '-g' for global transform, else the shader code won't be transformed.
```
browserify src/example.js -g brfs -g glslify > dist/bundle.js
```
When using `budo` use the same flags:
```
budo src/example.js --css src/example.css --live -- -g brfs -g glslify
```
The `demo.css` in the example directory (`node_modules\@jscad\csg-viewer\demo.css`) is a good starting point. Without a similar `.css` file the csg-viewer won't be visible.

## Test

There are no unit tests for the 3d viewer, however there is a small demo that is very practical to iterate fast and to see something visual without a complicated setup:

type:

```npm run dev``` this will start the demo at `localhost:9966`

## API

Work in progress!


## Sponsors

* An earlier version of this viewer has been developped for and very kindly sponsored by [Copenhagen Fabrication / Stykka](https://www.stykka.com/)

## License

[The MIT License (MIT)](./LICENSE)
(unless specified otherwise)
