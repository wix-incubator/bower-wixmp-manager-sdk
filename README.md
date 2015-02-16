## Wix Media Platform Manager SDK

### Overview
This SDK provides capabilities to work with media static files against wix media services. It includes support of several
sources such us 

* Private Media
* External Sources (Flickr, Instagram, Picasa, and Facebook)

You can get Folders and Items from any source, as well perform search and modifications. See [API](./API.md) for more information.

### Installation
Wix Media Platform has only one hard dependency for Promises - [Bluebird](https://github.com/petkaantonov/bluebird)

In order to install the lib, run:

```bash 
bower install wixmp-manager
```
    
Then add the following lines to your `index.html` file:

```html
<script src="bower_components/bluebird/js/browser/bluebird.js"></script>
<script src="bower_components/wixmp-manager-sdk/dist/wixmp-manager.min.js"></script>
```

#### AMD
For the usage with `requirejs`, add the following code to the requirejs config

```js
paths: {
  bluebird: 'bower_components/bluebird/js/browser/bluebird',
  wixmp: 'bower_components/wixmp-manager-sdk/dist/wixmp-manager.amd'
}
```

And you can inject the wixmp module in the requirejs module, for example

```js
define(['wixmp'], function(sdk) {
  var mySource = sdk.Source(sdk.sources.PUBLIC);
});
```

### Usage
The library is accessible via global variable `wixmp`, unless you are using AMD version as described above.
In order to start working with the SDK, you need to create a new source
of media files and pass the constructor of the future source:

```js
var myPublicMedia = wixmp.Source(wixmp.source.PUBLIC);
```

SDK already has several sources built-in and each of them is accessible via enum `wixmp.sources`.
The `Source` constructor creates the instance of a new source with different methods that are divided into 4 main namespaces:
`items`, `folders`, `item`, and `folder`. Each API call return a promise. In case of success, it is resolved with received data,
and in case of failure - with error object.
 
#### Implementing your own source
In case you would like to implement your own source, just pass a constructor function in `wixmp.Source()` instead of built-in
constructor.

```js
var myCustomSource = wixmp.Source(function myCustomSourceCtor(settings, emitFunc, http) {
  // your source code
}, {});
```
The constructor function is invoked with 3 arguments: settings for the source, `emit` function that can be used to emit events
for API calls. E.g. `emit(eventName)`. The last argument is `http` util that allows to make http calls. 
 

## Author
[Wix.com]()

## License
Copyright (C) 2015 Wix.com <sergeyb@wix.com>
Licensed under the MIT license.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
