# [Image Cropper](https://github.com/fengyuanchen/cropper)

> A simple jQuery image cropping plugin.

- [Demo](http://fengyuanchen.github.io/cropper)



## Features

- Supports touch
- Supports zoom
- Supports rotation
- Supports canvas
- Supports [options](#options)
- Supports [methods](#methods)
- Supports [events](#events)
- Supports multiple croppers
- Cross-browser support



## Main

```
dist/
├── cropper.css     ( 5 KB)
├── cropper.min.css ( 4 KB)
├── cropper.js      (50 KB)
└── cropper.min.js  (19 KB)
```



## Getting started

### Quick start

Four quick start options are available:

- [Download the latest release](https://github.com/fengyuanchen/cropper/archive/master.zip).
- Clone the repository: `git clone https://github.com/fengyuanchen/cropper.git`.
- Install with [NPM](http://npmjs.org): `npm install cropper`.
- Install with [Bower](http://bower.io): `bower install cropper`.



### Installation

Include files:

```html
<script src="/path/to/jquery.js"></script><!-- jQuery is required -->
<link  href="/path/to/cropper.css" rel="stylesheet">
<script src="/path/to/cropper.js"></script>
```



### Usage

Initialize with `$.fn.cropper` method.

```html
<!-- Wrap the image or canvas with a block element -->
<div class="container">
  <img src="picture.jpg">
</div>
```

```js
$('.container > img').cropper({
  aspectRatio: 16 / 9,
  crop: function(data) {
    // Output the result data for cropping image.
  }
});
```

#### Notes

- The size of the cropper inherits from the size of the image's parent element (wrapper), so be sure to wrap the image with a visible block element.

- The outputing cropped data bases on the original image size, so you can use them to crop the image directly.

- If you try to start cropper on a cross-origin image, please make sure that your browser supports HTML5 [CORS settings attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes), and your image server supports the `Access-Control-Allow-Origin` option.


#### Known issues

- About `getCroppedCanvas` method: The `canvas.drawImage` API in some Mac OS / iOS browsers will rotate an image with EXIF Orientation automatically, so the output cropped canvas may be incorrect. To fix this, you may upload the cropped data and crop the image in the server-side, see the example: [Crop Avatar](examples/crop-avatar). Or you may handle the EXIF Orientation in server first before to use cropper.



## Options

You may set cropper options with `$().cropper(options)`.
If you want to change the global default options, You may use `$.fn.cropper.setDefaults(options)`.


### aspectRatio

- Type: `Number`
- Default: `NaN`

Set the aspect ratio of the crop box. By default, the crop box is free ratio.


### crop

- Type: `Function`
- Default: `null`

This function will be executed when changes the crop box or image.


### preview

- Type: `String` (**jQuery selector**)
- Default: `''`

Add extra elements (containers) for previewing.

**Notes:**

- The maximum width is the initial width of preview container.
- The maximum height is the initial height of preview container.
- If you set an `aspectRatio` option, be sure to set the preview container with the same aspect ratio.


### strict

- Type: `Boolean`
- Default: `true`

In strict mode, the canvas cannot be smaller than the container, and the crop box cannot be outside of the canvas.


### responsive

- Type: `Boolean`
- Default: `true`

Rebuild the cropper when resize the window.


### checkImageOrigin

- Type: `Boolean`
- Default: `true`

By default, the plugin will check the image origin, and if it is a cross-origin image, a `crossOrigin` attribute will be added to the image element and a timestamp will be added to image url to enable "getCroppedCanvas".

Added timestamp will reload image to enable "getCroppedCanvas" on cross-origin image.

Adding `crossOrigin` attribute to image will stop adding timestamp to image url, and stop reload of image.


### background

- Type: `Boolean`
- Default: `true`

Show the grid background of the container.


### modal

- Type: `Boolean`
- Default: `true`

Show the black modal above the crop box.


### guides

- Type: `Boolean`
- Default: `true`

Show the dashed lines above the crop box.


### highlight

- Type: `Boolean`
- Default: `true`

Show the withe modal above the crop box (highlight the crop box).


### autoCrop

- Type: `Boolean`
- Default: `true`

Enable to crop the image automatically when initialize.


### autoCropArea

- Type: `Number`
- Default: `0.8` (80% of the image)

A number between 0 and 1. Define the automatic cropping area size (percentage).


### dragCrop

- Type: `Boolean`
- Default: `true`

Enable to remove the current crop box and create a new one by dragging over the image.


### movable

- Type: `Boolean`
- Default: `true`

Enable to move the crop box.


### resizable

- Type: `Boolean`
- Default: `true`

Enable to resize the crop box.


### zoomable

- Type: `Boolean`
- Default: `true`

Enable to zoom the image.


### mouseWheelZoom

- Type: `Boolean`
- Default: `true`

Enable to zoom the image by wheeling mouse.


### touchDragZoom

- Type: `Boolean`
- Default: `true`

Enable to zoom the image by dragging touch.


### rotatable

- Type: `Boolean`
- Default: `true`

Enable to rotate the image.


### minContainerWidth

- Type: `Number`
- Default: `300`

The minimum width of the container.


### minContainerHeight

- Type: `Number`
- Default: `150`

The minimum height of the container.


### minCropBoxWidth

- Type: `Number`
- Default: `0`

The minimum width of the crop box.


### minCropBoxHeight

- Type: `Number`
- Default: `0`

The minimum height of the crop box.


### build

- Type: `Function`
- Default: `null`

A shortcut of the "build.cropper" event.


### built

- Type: `Function`
- Default: `null`

A shortcut of the "built.cropper" event.


### dragstart

- Type: `Function`
- Default: `null`

A shortcut of the "dragstart.cropper" event.


### dragmove

- Type: `Function`
- Default: `null`

A shortcut of the "dragmove.cropper" event.


### dragend

- Type: `Function`
- Default: `null`

A shortcut of the "dragend.cropper" event.


### zoomin

- Type: `Function`
- Default: `null`

A shortcut of the "zoomin.cropper" event.


### zoomout

- Type: `Function`
- Default: `null`

A shortcut of the "zoomout.cropper" event.



## Methods

General usage:

```js
$().cropper('method', argument1, , argument2, ..., argumentN)
```


### move(offsetX, offsetY)

- **offsetX**:
  - Type: `Number`
  - Moving size (px) in the horizontal direction
- **offsetY**:
  - Type: `Number`
  - Moving size (px) in the vertical direction

Move the image.

```js
$().cropper('move', 1, 0)
$().cropper('move', 0, -1)

```


### zoom(ratio)

- **ratio**:
  - Type: `Number`
  - Zoom in: requires a positive number (ratio > 0)
  - Zoom out: requires a negative number (ratio < 0)

Zoom the image.

```js
$().cropper('zoom', 0.1)
$().cropper('zoom', -0.1)
```


### rotate(degree)

- **degree**:
  - Type: `Number`
  - Rotate right: requires a positive number (degree > 0)
  - Rotate left: requires a negative number (degree < 0)

Rotate the image. Requires CSS3 [Transforms3d](http://caniuse.com/transforms3d) support (IE 10+).

```js
$().cropper('rotate', 90)
$().cropper('rotate', -90)
```


### enable()

Enable (unfreeze) the cropper.


### disable()

Disable (freeze) the cropper.


### reset()

Reset the image and crop box to the initial states.


### clear()

Clear the crop box.


### replace(url)

- **url**:
  - Type: `String`
  - A new image url.

Replace the image and rebuild the cropper.


### destroy()

Destroy the cropper and remove the instance from the image.


### getData()

- (return value):
  - Type: `Object`
  - Properties:
    - `x`: the offset left of the cropped area
    - `y`: the offset top of the cropped area
    - `width`: the width of the cropped area
    - `height`: the height of the cropped area
    - `rotate`: the rotated degrees of the image

Get the cropped area data in the original image for cropping image.

![a schematic diagram of data's properties](assets/img/data.png)


### getContainerData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `width`: the current width of the container
    - `height`: the current height of the container

Output the container size data.


### getImageData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `left`: the offset left of the image
    - `top`: the offset top of the image
    - `width`: the width of the image
    - `height`: the height of the image

Output the image position and size.


### getCanvasData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `left`: the offset left of the canvas
    - `top`: the offset top of the canvas
    - `width`: the width of the canvas
    - `height`: the height of the canvas

Output the canvas (image wrapper) position and size.


### setCanvasData(data)

- **data**:
  - Type: `Object`
  - Properties:
    - `left`: the new offset left of the canvas
    - `top`: the new offset top of the canvas
    - `width`: the new width of the canvas
    - `height`: the new height of the canvas

Change the canvas (image wrapper) position and size.


### getCropBoxData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `left`: the offset left of the crop box
    - `top`: the offset top of the crop box
    - `width`: the width of the crop box
    - `height`: the height of the crop box

Output the crop box position and size.


### setCropBoxData(data)

- **data**:
  - Type: `Object`
  - Properties:
    - `left`: the new offset left of the crop box
    - `top`: the new offset top of the crop box
    - `width`: the new width of the crop box
    - `height`: the new height of the crop box

Change the crop box position and size.


### getCroppedCanvas([options])

- **options** (optional):
  - Type: `Object`
  - properties
    - `width`: the destination width of the output canvas
    - `height`: the destination height of the output canvas
    - `fillColor`: a color to fill any alpha values in the output canvas

- (return  value):
  - Type: `HTMLCanvasElement`
  - A canvas drawn the cropped image.

- Browser support:
  - Basic image: requires [Canvas](http://caniuse.com/canvas) support (IE 9+).
  - Rotated image: requires CSS3 [Transforms3d](http://caniuse.com/transforms3d) support (IE 10+).
  - Cross-origin image: requires HTML5 [CORS settings attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) support (IE 11+).

Get a canvas drawn the cropped image.

> After then, you can display the canvas as an image directly, or use [canvas.toDataURL](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL) to get a Data URL, or use [canvas.toBlob](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toBlob) to get a blob and upload it to server with [FormData](https://developer.mozilla.org/en/XMLHttpRequest/FormData) if the browser supports these APIs.

```js
$().cropper('getCroppedCanvas')

$().cropper('getCroppedCanvas', {
  width: 160,
  height: 90
});
```

### setAspectRatio(aspectRatio)

- **aspectRatio**:
  - Type: `Number`
  - Requires a positive number.

Change the aspect ratio of the crop box.


### setDragMode([mode])

- **mode** (optional):
  - Type: `String`
  - Default: `''`
  - Options: `'crop'`, `'move'`

Change the drag mode.

**Tips:** You can toggle the "crop" and "move" mode by double click on the cropper.



## Events

### build.cropper

This event fires when a cropper instance starts to load a image.


### built.cropper

This event fires when a cropper instance has built completely.


### dragstart.cropper

- **event.dragType**:
  - "crop": create a new crop box
  - "move": move the canvas
  - "zoom": zoom in / out the canvas by dragging touch.
  - "e": resize the east side of the crop box
  - "w": resize the west side of the crop box
  - "s": resize the south side of the crop box
  - "n": resize the north side of the crop box
  - "se": resize the southeast side of the crop box
  - "sw": resize the southwest side of the crop box
  - "ne": resize the northeast side of the crop box
  - "nw": resize the northwest side of the crop box
  - "all": move the crop box

This event fires when the crop box starts to change.

> Related original events: "mousedown", "touchstart".

```
$('img').on('dragstart.cropper', function (e) {
  console.log(e.type); // dragstart
  console.log(e.namespace); // cropper
  console.log(e.dragType); // ...
});
```

### dragmove.cropper

- **event.dragType**: The same as "dragstart.cropper".

This event fires when the crop box is changing.

> Related original events: "mousemove", "touchmove".


### dragend.cropper

- **event.dragType**: The same as "dragstart.cropper".

This event fires when the crop box stops to change.

> Related original events: "mouseup", "mouseleave", "touchend", "touchleave", "touchcancel".


### zoomin.cropper

This event fires when a cropper instance starts to zoom in its canvas.


### zoomout.cropper

This event fires when a cropper instance starts to zoom out its canvas.



## No conflict

If you have to use other plugin with the same namespace, just call the `$.fn.cropper.noConflict` method to revert to it.

```html
<script src="other-plugin.js"></script>
<script src="cropper.js"></script>
<script>
  $.fn.cropper.noConflict();
  // Code that uses other plugin's "$().cropper" can follow here.
</script>
```



## Browser Support

- Chrome 38+
- Firefox 33+
- Internet Explorer 8+
- Opera 25+
- Safari 5.1+

As a jQuery plugin, you also need to see the [jQuery Browser Support](http://jquery.com/browser-support/).



## [License](LICENSE.md)

Released under the [MIT](http://opensource.org/licenses/mit-license.html) license.



## Related projects

- [ngCropper](https://github.com/koorgoo/ngCropper) - AngularJS wrapper for Cropper.
- [ember-cli-cropper](https://github.com/anilmaurya/ember-cli-cropper) - Ember cli addon for Cropper.
