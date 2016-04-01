# qrstuv

A clean and modern QR code reader for browsers. Uses Promises for returning
results, rather than callbacks (Node-style or otherwise).

2011 Lazar Laszlo      http://lazarsoft.info
2014 Jess Telford      http://jes.st
2016 Stuart P. Bentley https://stuartpb.com/

This is a fork of a port to npm of Lazar Laszlo's port of ZXing qrcode scanner, [http://code.google.com/p/zxing](http://code.google.com/p/zxing).

Lazar's demo exhibits basically the same functionality as this module: [http://webqr.com](http://webqr.com)

## Prerequisites

Note that, as this library uses Promises, if you're supporting an environment
that doesn't provide a native Promise implementation, you'll need to include
a polyfill that provides Promise like [es6-shim][] (for browsers) or a module
that implements Promise like `bluebird` (for Node/Browserify).

If you're in a sandboxed module environment like Node, you'll need to
explicitly introduce your Promise module to this one:

```js
var qrcode = require('qrstuv');
qrcode.Promise = require('bluebird');
```

[es6-shim]: https://github.com/paulmillr/es6-shim

Of course, if you're using Node 4.0.0 or later, or a reasonably recent version
of Google Chrome or Mozilla Firefox, you don't have to worry about this, since
Promise is in the environment by default in all of these. Polyfilling promise
is, essentially, a legacy concern in 2016.

## Usage

```js
qrcode = require('qrstuv');
qrcode.decode(uri).then(function(result) {
  console.log(result); // Will output the decoded information
});
```

If `uri` is not passed, will instead extract image data from a `canvas` element
with `id="qr-canvas"`

[new from 2014.01.09]
For webcam qrcode decoding (included in the test.html) you will need a browser with getUserMedia (WebRTC) capability.

## Usage on Node

Since Node doesn't come with an implementation of Canvas or Image the way that
browsers do, you'll need to introduce your own. You can do this relatively
easily by installing the `canvas` module, which comes with both:

```js
var qrcode = require('qrstuv');
var Canvas = require('canvas');
qrcode.Canvas = Canvas;
qrcode.Image = Canvas.Image;

qrcode.decode(__dirname + '/qrcode.png').then(function(result) {
  console.log(result);
}
```
