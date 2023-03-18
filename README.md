# Readme

<!-- TOC -->

* [1.1 Introduction](#11-introduction)
* [1.2 ES6 modules](#12-es6-modules)
* [1.3 Features](#13-features)
* [1.4 Integration in your application](#14-integration-in-your-application)
  * [1.4.1 As an ES6 library (recommended method)](#141-as-an-es6-library-recommended-method)
  * [1.4.2 As an old-fashioned independent library (need update)](#142-as-an-old-fashioned-independent-library-need-update)
  * [1.4.3 As an UMD library (Angular, ...)](#143-as-an-umd-library-angular-)
* [1.5 Going further](#15-going-further)
* [1.6 Running the examples in debug mode](#16-running-the-examples-in-debug-mode)
* [1.7 Running the un-minified version of Cesium](#17-running-the-un-minified-version-of-cesium)
* [1.8 Limitations](#18-limitations)
* [1.9 Release process](#19-release-process)

<!-- /TOC -->

## 1.1 Introduction

OpenLayers - Cesium integration library. Create your map using [OpenLayers](https://openlayers.org/), and visualize it on a globe with [Cesium](https://cesiumjs.org).

See [live examples](https://openlayers.org/ol-cesium/examples/).

## 1.2 ES6 modules

Since version 2.0, the code is entirely based on ES6 modules and syntax.
It requires OpenLayers 6.x.
A convenient ES6 package `olcs` is available on npm.

## 1.3 Features

Switch smoothly between 2D and 3D and synchronize:

* Map context (bounding box and zoom level);
* Raster data sources;
* Vector data sources in 2D and 3D;
* Map selection (selected items);
* Animated transitions between map and globe view.

The library is configurable and extensible and allows:

* Lazy or eager loading of Cesium
* Limiting Cesium resource consumption (idle detection)

For synchronization of maps in projections other than EPSG:4326 and EPSG:3857 you need 2 datasets, see the customProj example.

## 1.4 Integration in your application

There are several ways to integrate OL-Cesium in your application.
In all cases OpenLayers and Cesium are peer-dependencies of OL-Cesium, your application need to depend on a compatible version of OpenLayers and of Cesium. Note that Cesium is accessed through the global `window.Cesium` object. OpenLayers is accessed through ES6 imports.

### 1.4.1 As an ES6 library (recommended method)

```bash
npm i --save olcs
```

Then import the parts you need. Example:

```js
import OLCesium from 'olcs/OLCesium.js';
const ol3d = new OLCesium({map: ol2dMap}); // ol2dMap is the ol.Map instance
ol3d.setEnabled(true);
```

In addition, you need to expose the Cesium library as `window.Cesium`.
For this, simply add the Cesium script to your html:

```html
<script type="text/javascript" src="..your_path../Cesium.js"></script>
```

For Cesium integration with Webpack, see [ol-cesium-webpack-example](https://github.com/gberaudo/ol-cesium-webpack-example).

### 1.4.2 As an old-fashioned independent library (need update)

* build the library in dist/olcs.js:

```bash
npm i --save olcs
npm run build-library
```

* get the CSS and JS from the full build at <https://openlayers.org/download/>

* use as follow:

```js
const ol3d = new olcs.OLCesium({map: ol2dMap}); // ol2dMap is the ol.Map instance
ol3d.setEnabled(true);
```

For the remaining steps, see the [old fashioned example](https://openlayers.org/ol-cesium/examples/oldfashioned.html).
Notably, you need the Cesium library.

### 1.4.3 As an UMD library (Angular, ...)

```bash
npm i --save ol-cesium
```

The UMD-specific build is located here: `node_modules/ol-cesium/dist/olcesium.umd.js`

Then import the parts you need. Example:

```js
import OLCesium from 'ol-cesium';
const ol3d = new OLCesium({map: ol2dMap}); // ol2dMap is the ol.Map instance
ol3d.setEnabled(true);
```

In addition, you need to expose the Cesium library as `window.Cesium`.
For this, simply add the Cesium script to your html:

```html
<script type="text/javascript" src="..your_path../Cesium.js"></script>
```

## 1.5 Going further

See the [examples](https://openlayers.org/ol-cesium/examples/).

If you are new to Cesium, you should also check the [Cesium tutorials](https://cesiumjs.org/tutorials).

## 1.6 Running the examples in debug mode

This is useful for contributing to Ol-Cesium, because it loads the
source files instead of a minified build:

```bash
make serve
```

will make the distribution examples available at <http://localhost:3000/examples>

## 1.7 Running the un-minified version of Cesium

Passing the parameter `?mode=dev` to an example will load the debug version of
Cesium instead of the minified one. This is helpful when something breaks inside
Cesium. In distribution mode, an un-minified version of OpenLayers and Ol-Cesium is
also loaded.

## 1.8 Limitations

* OpenLayers un-managed layers are not discoverable and as a consequence not
supported. Plain layers should be used instead of the synchronization managed
manually. See <https://github.com/openlayers/ol-cesium/issues/350>.

* OpenLayers interactions are not supported in 3d. See <https://github.com/openlayers/ol-cesium/issues/655>.

## 1.9 Release process

See [RELEASE.md](https://github.com/openlayers/ol-cesium/blob/master/RELEASE.md).
