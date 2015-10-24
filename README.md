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
    - [Preserve Aspect Ratio](#preserve-aspect-ratio)
      - [Align values](#align-values)
      - [Meet or slice values](#meet-or-slice-values)
  - [SVG Elements](#svg-elements)
    - [Graphical Elements](#graphical-elements)
    - [Container Elements](#container-elements)
    - [Gradient Elements](#gradient-elements)
    - [Styling SVGs with CSS](#styling-svgs-with-css)

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

[Example](examples/preserve-aspect-ratio.html)

This is used to crop and position graphics that don't exactly fit within the viewport.

The dimensions of the viewBox don't have to be in proportion to the viewport.
`preserveAspectRatio` allows us to control what happens when the width and height
between viewport and viewBox are not proportional.

If don't want to maintain aspect ratio, set to `none`. This will allow graphic to be squeezed and stretched.

```html
<svg width="100" height="300" viewBox="0 0 400 400" preserveAspectRatio="none">
  <!-- content... -->
</svg>
```

Any other value than `none`, will force the graphic to have uniform scaling and will preserve aspect ratio of viewBox.

Two parameters are passed to `preserveAspectRatio`:

* align: in the form of x and y
* meet or slice: viewBox should meet edges of viewport (similar to css background-size contain)
or slice off the extra, which is like css background-size cover.

#### Align values

* none
* xMinYMin - left top
* xMidYMin - middle top
* xMaxYMin - right top
* xMinYMid - left middle
* xMidYMid - middle middle
* xMaxYMid - right middle
* xMinYMax - left bottom
* xMidYMax - middle bottom
* xMaxYMax - right bottom

#### Meet or slice values

* meet - shrink image such that all edges are contained within viewport
* slice - trims off excess

## SVG Elements

Types of elements include graphical, container, gradient, and animation.

Common graphical elements include:
Circle, ellipse, line, path, polygon, polyline, rect, text, use

Common container elements include:
defs, g, symbol, svg

Two types of gradient elements:
linearGradient, radialGradient

### Graphical Elements

[Example](examples/graphical-elements.html)

Most graphical elements can have the following attributes:

* fill: fill the element with color
* stroke: sets the outline color
* stroke-width: sets the size of the stroke

`ellipse` takes a centerpoint defined by cx and cy, and also two radii rx and ry

`rect` needs x and y to determine where its top-left corner will be positioned.
Can also add rounded corners by setting rx and ry.

`line` creates straight line between two points defined by x1, y1 and x2, y2

`polyline` is a collection of connected line elements. Points are defined as a list
in the form x1, y1, x2, y2, etc...

`polygon` similar to polyline, but first and last points connect.

`path` contains a set of points, lines and arcs. All other shapes can be defined in terms of path.

Path data attribute defined with `d`. It can contain:

* M: moveTo
* L: lineTo
* Arcs, cubic, and quadratic bezier curves
* Z: closepath

moveTo is starting point of the path

lineTo draws straight lines from one point to another

closepath connects current point to initial point with straight line

`text` is used to add fully accessible text within an SVG graphic. x and y specify its position.

`use` reference other svg elements for reuse and render them in a given location.

### Container Elements

[Example](examples/container-elements.html)

`defs` contains items intended for later reuse. Everything in defs element is not rendered until referenced.

`g` is used to group a collection of items. For example, if want to animate multiple elements at once,
or style all their fill colors the same.

`symbol` defines graphical template objects to be instantiated by `<use>` elements.
Similar to `use`, it's not rendered until referenced by an object.
An advatage over use is `symbol` can define its own `viewBox` and `preserveAspectRatio` attributes.

### Gradient Elements

[Example](examples/gradient-elements.html)

Gradients are not rendered on their own, rather they are defined in a `defs` section,
then used as a fill in a graphical element via `url(#gradientId)`. Can also be used in css.

They contain stops which define what color the gradient should be at certain points.
stop offsets range in value from 0 - 100%.

`linearGradient` by default is horizontal. Use x1, x2, y1 and y2 values to flip it to vertical

`radialGradient` require a circle to be defined to set their outermost stop position at 100%,
defined with cx, cy and r. Also requires a focual point for the innermost stop position at 0%,
specified with fx and fy. If focal point is not defined, cx and cy values will be used.

### Styling SVGs with CSS

Attributes such as `fill` and `stroke` should be replaced with `class` and styled with css.

Many SVG prsentation attributes are available to be styled using css.
