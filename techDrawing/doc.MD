# Technical Drawings using SVG




## Why SVG for Technical drawings



* SVG vs. Canvas:
    * SVG is good with fewer big objects and few colors (like in technical drawings)
    * scalable
    * direct export to file possible
    * [Code Examples of Canvas and SVG](https://www.safaribooksonline.com/blog/2012/04/17/using-html5-canvas-vs-svg/)

   Very good comparision on https://msdn.microsoft.com/library/gg193983%28v=vs.85%29.aspx

    ![alt text](https://i-msdn.sec.s-msft.com/dynimg/IC496493.png   "CANVAS vs SVG")




* development speed:
    * integrated event handling
    * style
    * elements: marker
* support:basic features are included almost in every browser; some advanced features not
    * https://en.wikipedia.org/wiki/Comparison_of_layout_engines_%28Scalable_Vector_Graphics%29
    * http://caniuse.com/#search=svg
* bad thing: no line breaks in SVG-TEXT available





##Recommendations


### SVG framework [d3](https://d3js.org/)


* creating and appending attributes: short code (50% shorter than pure JS), clean, readable. (main reason for me)

```javascript
var g = d3.select("#svg").append("g");

    g.append('line') // LEFT LINE
        .attr({
            'x1': x1 ? x1 : 0,
            'y1': 25,
            'x2': x2,
            'y2': 25
    });
```
* building diagrams is fast through built in feature for scales, axes
* function for zoom/scroll and drag&drop
* unified event handling for browser compatibility
* well documented, lots of examples
* fast
* binding JSON Data to SVG. For easy creating a diagrams from JSON. Very good feature for simple diagrams; we do not use it in the RAPIDFACTURE CAD - with major requirements to the data handling, "for loops" are more efficient and easy to use.


###Links

* [good SVG Tutorial by jenkov](http://tutorials.jenkov.com/svg/index.html); all important things included
* [Mozillas SVG-Element Reference](https://developer.mozilla.org/en-US/docs/Web/SVG/Element#Shape_elements)
* [SVG 1.1 Specification by W3C](https://www.w3.org/TR/SVG/expanded-toc.html)


### Main Frame



### Dimensions



### Symbols



### Hatching
