# OpenLayers Client Starter

Starter files for building a standalone OpenLayers client using otherwise vanilla JavaScript. Does not require webpack or any other bundling tool. Only uses native JavaScript modules to simplify development. Provides intellisense type completion in VSCode for the OpenLayers library.

OpenLayers (`V4.6.5`) is preinstalled and linked in debug format. You can source it over CDN or in minified formats if preferred [instructions below](#using-the-openLayers-cdn).

# Usage

Just write your [JavaScript module files](#using-javascript-modules) and serve the `index.html`. To serve the client you can use a Python HTTP server or the VSCode LiveServer extension.

The `index.js` file is set up as the entrypoint to the application. You can import module bits and initialize the JavaScript in this file.

## Serving Locally

> after starting the HTTP server open your browser to http://localhost:3000

### Serve with LiveServer extension

> right click the `src/index.html` file and select `Open with LiveServer`

### Serve with Python

> Python 3

```sh
$ python -m http.server -d src/ 3000
```

> Python 2

```sh
$ cd src/

$ python -m SimpleHTTPServer 3000
```

## Deployment

> Copy the `src/` directory to your HTTP server web directory

# Using JavaScript Modules

Normally all scripts loaded in the browser share a common global space for any namespaces declared in the scripts. This causes complications of using either dense single script files or working around delicate `<script>` element linking order. Not to mention namespace conflicts in the global scope.

> a namespace is a general term used to describe any uniquely named variable, function or class that has been declared in a given scope (a block or global)

JavaScript modules let you have distinct "global" scopes and explicitly state what should be shared between other modules files. Using modules can help break up giant script files into more readable, organized and portable pieces. In other words modules help make your code more...modular!

> modules revolve around control of private and shared namespaces

> one module exports the namespaces of its choice while another can decide which of those to import and use

JavaScript modules use the `<script type="module">` attribute to alert the browser that it should parse `import` and `export` statements. Modules behave in `strict` mode and have a number of other features and convenient behaviors. Basic usage of `import` and `export` are described in this guide. Use the resources below to dig deeper into how modules work:

- [MDN Modules Guide (high level)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
- [JavaScript.info (in depth)](https://javascript.info/modules-intro)

## Exporting

In order to import a namespace in a module it must first be exported by another module.

> a module can export a single default export, multiple named exports or a combination of the two

> any valid namespace can be exported although some depend on the type of export

> namespaces are declared using any declaration keyword from the list below

```js
let
var
const
class
function
```

### Default Export

A default export represents a single encapsulation of the main feature of a module. You can only have **one default export per module**.

> the default export does not retain its namespace when it gets imported (this will make more sense in the import section)

There are two cases for default exports

> the default export must be defined before the export statement

```js
// any valid namespace, function used as an example
function myFunc() {}

export default myFunc;
```

> the `class` keyword is special and can be declared and exported inline

```js
export default class ClassName {}
```

### Named Exports

Named exports can be used for a module to expose specific named features. **You can have any number of named exports in a module.**

> named exports retain their namespace when imported in another module

There are two ways to use named exports:

> inline export and declaration

```js
export const myVariable = "a value or object reference";
```

> export after declaration

```js
const myObject = {};

export myObject;
```

> multiple named exports in a single statement

```js
const myObject = {};
const myVariable = "";

export { myObject, myVariable };
```

## Importing

Once a module has declared its exports they can be imported in another module.

> a module can import a default export, named export or a combination of the two

> a module can decide what to import as well as what namespace to use

Importing from another module uses the `import from ""` syntax. The `from` keyword is used to provide the relative path to the module being imported.

> Note: browser modules must include the `.js` extension unlike NodeJS

When importing a default export the namespace it is given is defined by the importing module

> importing a default export

`src/exporting-module.js`

```js
export default class MyClass {}
```

`src/importing-module.js`

```js
// notice the namespace

import AClass from "./exporting-module.js";
```

# OpenLayers Alternate Sourcing

## Using the minified format

> enter the following commands to download the minified formats

> ~75% smaller in size in exchange for debugging support

```sh
$ curl https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol.css -o src/ol.css

$ curl https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol.js -o src/ol.js
```

## Using the OpenLayers CDN

Replace the local links in `index.html` with the CDN links for the CSS and JavaScript.

> V4.6.5: debug (non-minified) - 411KB

> use this for local development and debugging support

```html
<link
  rel="stylesheet"
  type="text/css"
  href="https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol-debug.css"
/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol-debug.js"></script>
```

> V4.6.5: minified lib - 144KB

> use this for deployment or if you don't need the full lib for debugging

```html
<link
  rel="stylesheet"
  type="text/css"
  href="https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol.css"
/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol.js"></script>
```
