# phoenix_ujs

**Unobtrusive vanilla JS toolset for Phoenix framework**

[![npm version](https://badge.fury.io/js/phoenix_ujs.svg)](https://badge.fury.io/js/phoenix_ujs)

## Purpose

A compact port of [jquery-ujs](https://github.com/rails/jquery-ujs) for Phoenix framework (the library is agnostic, so
  you can use it with other backends as well). The library **does not requires jQuery** and covers only essential needs:

- non-'GET' links (POST, PUT, PATCH, DELETE, etc)
- confirmation and/or remote request on clicking link or submitting form
- refreshing CSRF inputs in forms (fix browser form caching)

## Installation

```js
npm i --save phoenix_ujs
```
If your js build system supports commonjs `require` and/or `import` methods (**Brunch, Webpack, Browserify**) add the
next code at the top of your main js file:

```js
var UJS = require("phoenix_ujs");
// or
import "phoenix_ujs";
```

For other cases you can use one of the package files:
``` bash
~ : ls node_modules/phoenix_ujs
ujs.js      # browser version
ujs.min.js  # minified browser version
ujs.cjs.js  # commonjs version (used in `require` by default)
ujs.es.js   # ES6 version
```
To setup your backend - open layout file and add next at the top of the **<head>**:

```html
<html>
  <head>
    <!-- example for Phoenix framework -->
    <meta name="csrf-token" content="<%= get_csrf_token() %>"/>
    <!-- also meta tag can contain the next setting-attributes:
      csrf-param="_csrf_token"
      csrf-header="x-csrf-token"
      method-param="_method"
    -->
```

## Usage

```html
<!-- to specify non-get method add `ujs-method` -->
<a href="/request/post" ujs-method="post">Make a POST request</a>
<a href="/request/delete" ujs-method="delete">Make a DELETE request</a>
<a href="/request/patch" ujs-method="patch">Make a PATCH request</a>
```

```html
<!-- add confirmation with `ujs-confirm`  -->
<a href="/request/get" ujs-confirm="Are you sure?">Ask confirmation to open link</a>
<a href="/request/post" ujs-confirm="Are you sure?" ujs-method="post">Ask confirmation to make a POST request</a>
<form action="/request/post" method="POST" ujs-confirm="Are you sure?">
  <!-- ask confirmation when form is submitting -->
</form>
```

```html
<!-- make an ajax request on click if `ujs-remote` is present -->
<!-- the next event will be triggered:
  ajax:beforeSend - event before AJAX call. AJAX request can be canceled if handler will return `false`
  ajax:success - a success response (2xx status code)
  ajax:error - an error response (4xx, 5xx status code)
  ajax:complete - an response received with any status
-->
<a href="/request/patch" ujs-method="patch" ujs-remote>Patch remotely</a>
<form action="/request/post" method="POST" ujs-remote>
  <!--  AJAX form submitting -->
</form>
```

## TODO
- tests
- examples
