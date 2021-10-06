---
title:  "Interactive Image Maps"
layout: blog
order: 3
topic: Javascript
topic_path: /docs/javascript/index.html
---
We can build interactive image maps in Javascript using the HTML `canvas` element. The `canvas` element is a container which permits Javascript to draw on the page. The `canvas` element supports paths, boxes, circles and other shapes drawn by Javascript running in the browser.

The HTML `map` tag is used to define an image map. An image map consists of a set of area elements. An image map can be defined as follows:
```html
<map name="map">
  <area shape="poly" id="a" coords="0,0,1,1,2,2,0,0" />
  <area shape="poly" id="b" coords="3,3,4,4,5,5,3,3" />
</map>
```

The `coords` attribute is a series of coordinate pairs. For the area with `id="a"`, the polygon is defined by the coordinates (0,0), (1,1), (2,2), (0,0).

### Define area poygons
Let's say we want to create an interactive map of the human body. We could pull an image with different muscle groups outlined.

<img src="{{ site.baseurl }}/assets/img/human-body.png">

We could use an image editing program to get the coordinates of different polygons within the image. For example, we could use two polygons to define the pectoral muscles. Using GIMP or another program, we could take the coordinates of those polygons and create an image map HTML element.

<img src="{{ site.baseurl }}/assets/img/human-body-highlighted.png">

```html
<map name="map">
  <area shape="poly" alt="Left pec" coords="181,131,182,171,188,178..." />
  <area shape="poly" alt="Right pec" coords="175,131,175,171,172,176..." />
</map
```

### Draw polygons
If we want to highlight the polygons when the user clicks one of the pectoral muscles, we will need to use some Javascript to draw on the `canvas` element. We can use the function `getElementsByTagName` to select all of the area elements in our image map.
```javascript
function drawAllShapes() {
  var elements = document.getElementsByTagName("area");

  for (let element of elements) {
    var coords = element.coords;
    drawShape(coords);
  }
}
```

Now that we have the coordinates of the polygon, we need to draw them on the canvas. We will use the `CanvasRenderingContext2D` to draw on the surface of the `canvas` element.

```javascript
function drawShape(coords) {
  var can = document.getElementById('myCanvas');
  var hdc = can.getContext('2d');

  // parse coordinates
  var mCoords = coords.split(',');

  // draw on context
  hdc.beginPath();
  hdc.beginPath();
  hdc.moveTo(mCoords[0], mCoords[1]);
  for (i=2; i<mCoords.length; i+=2)
  {
    hdc.lineTo(mCoords[i], mCoords[i+1]);
  }

  hdc.lineTo(mCoords[0], mCoords[1]);
  hdc.stroke();
}
```

In this way a user action can create a drawing on top of an image. The `canvas` element and its APIs are a hidden gem and are quite powerful!