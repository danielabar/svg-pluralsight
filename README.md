<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [SVG Fundamentals](#svg-fundamentals)
  - [Intro](#intro)
  - [How to Use SVG](#how-to-use-svg)
  - [SVG Layout](#svg-layout)
    - [Canvas](#canvas)
    - [Viewport](#viewport)
    - [Viewbox](#viewbox)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# SVG Fundamentals

> Learning SVG with Pluralsight

## Intro

Scalable vector graphics.

Can create with Adobe Illustrator, Sketch, or Inkscape.

Can also create by hand. For example, `circle` element takes `cx`, centerpoint along x axis,
`cy` centerpoint along y axis, and `r` radius.

By default, all SVG elements are colored black. To change this, add `fill` attribute.

## How to Use SVG

[Example](examples/how-to.html)

Can be referenced externally with an image tag or added as css background.

Can be embedded using an embed tag, object, or iframe.

Finally can be inlined in html using svg tag.

## SVG Layout

[Example](examples/layout.html)

Different from CSS layout and box model. Elements are positioned based on a co-ordinate system.

Consider an analogy of looking at stars in the sky through a telescope:

* largest level is view of the entire sky
* this can be narrowed down through the view of the telescope
* telescope can be used to zoom in and out of the view
* can change the direction or portion of the sky being looked at by pointing the  telescope in a different direction

Correlation to SVG components:

* sky === SVG drawing area, a.k.a _canvas_, an infinite space where elements can exist
* view through telescope === SVG _viewport_, it narrows the view focus, and crops out areas not of interest at time of viewing
* changing direction and zoom level === functions of the _viewBox_

### Canvas

When setting up an inline svg in html, don't need to do anything to setup Canvas,
it simply exists and is infinite.

### Viewport

The viewport is the viewable section of the canvas, and is set on the `svg` tag via `width` and `height` attributes (or in css).

Viewport width and height can be specified in any units (px, em, etc.)

Browser establishes co-ordinate system based on upper left hand corner of viewport,
such that x=0 is the top left corner, with x increasing towards the right.
And y=0 is the top left corner, with y increasing _downwards_.

### Viewbox

viewBox is an attribute of the svg element and consists of 4 co-ordinates: x, y, width and height.
In the example below, the viewBox is the same as dimensions as the viewPort.

```html
<svg width="300" height="100" viewBox="0, 0, 300, 100">
  <circle cx="150" cy="50" r="50"></circle>
</svg>
```

Increasing the width and height values of viewBox will achieve a "zoomed out" effect on the drawing.
In the example below, the co-ordinate system is altered by the viewBox to show 600 units of width
in a 300 unit width container, and 200 units of height, within a 100 unit container (viewport).

This makes every pixel in the viewPort cut in half wrt its dimensions.

```html
<svg width="300" height="100" viewBox="0, 0, 600, 200">
  <!-- content... -->
</svg>
```

To center a circle in these new co-ordinates, must change the cx and cy to 300 and 100 respectively.

### Preserve Aspect Ratio

This is used to crop and position graphics that don't exactly fit within the viewport.
