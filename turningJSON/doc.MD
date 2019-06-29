# Docu of JSON format for turned parts



Turned parts are stored by an array of contour elements which hold further details (dimensions, features, etc.).


![alt text](img/samplePart.png "Example Part from RAPIDFACTURE CAD")


[See here](example.json) for a Code example.

The basic document structure consists of three parts:

```javascript
{
    "meta": {}, // some meta info about drawing in this obj
    "innerContour": [], // array of contour elements
    "outerContour": [], // array of contour elements
}
```

## Meta Information



The following meta information is used for the drawing:


```javascript
{
  "companyName": "RAPIDFACTURE",
  "marking": "Test Part",
  "drawingNumber": "1",
  "draftsman": "",
  "checker": "",
  "date": "",
  "scale": "auto",
  "paperSize": "A4",
  "units": "mm",
  "generalTolerance": "DIN 2768 - mittel",
  "material": "C45",
  "surface": "Ra 6,3",
  "innerEdge": "+0,3 bis +0,5",
  "outerEdge": "-0,1 bis -0,3"
}
```

Ideas: could also consist "size" (diameter/length), "weight".

## Contour


Inner and outer contour use the same structure for describing the contour.

### Example contour element

Every Contour Element has the baisc structure:

```javascript
{
    "meta":{},
    "left":{},
    "middle":{},
    "right":{}
}
```

![alt text](img/contourElemSections.png "Sections of the contour element")

"left", "middle" and "right" each hold one main dimension and can hold optional information about edges, faces and features.

There are three element types to represent the contour: cylinder, cone or circle. (Maybe we add another one with splines in the future)

![alt text](img/elementTypes.png "Sections of the contour element")



```javascript
[{
    "type": "cylinder",         // elementtype: cylinder, cone or circle

    "meta": {
        "dimension-type": 0     // cone and circle elements can have different definitions of their dimensions
    },
    "left": {
        "dimension": {          // left diameter
            "value": 50,        // value in mm
            "tolerance": {      // optional tolerance object
                "value": 0.1    // value in mm
                "type": "+"     // tolerance type; +, -, ±, +-; letters like "H, G, h, g" for fittings
            }

        }
    },
    "middle": {
        "dimension": {          // element length
            "value": 20,        // value in mm
            "link-to-element": 0// the end of the element can also be referenced to another element;
                                // element length stays the same
        },
        "face": {               // surface definition
            "surface-roughness": 30
        }
    },
    "right": {
        "dimension": {          // right diameter dimension
            "value": 50,        // value in mm
        },
        "edge": {               // edge definition
            "value": 2,         // size in mm
            "type": "radius"
        },
        "feature": {            // features
            "groove": {},
            "booring": {}
        }
    },
},
{} // next element ...
]
```

## Features

### Champfer / Radius

```js
{
   "type": "cylinder",
   "left": {
     "dimension": {
       "value": 30
     },
     "edge": { // R 1 mm radius  
       "dimension": {
         "value": 1
       },
       "type": "radius"
     }
   },
   "middle": {
     "dimension": {
       "value": 20
     }
   },
   "right": {
     "dimension": {
       "value": 30
     },
     "edge": { // 45° x 0.3 mm chamfer
       "dimension": {
         "value": 0.3
       },
       "type": "chamfer",
       "angle": 45
     }
   },
   "meta": {}
}
```



### Surface Quality
ToDo


### Text

```js
   // one contour element:
  {
      "type": "cylinder",
      "left": {
          "dimension": {
              "value": 30
          },
          "feature": {
              "text": [{ // text as array; written on left face
                  "content": "Left text"
              }]
          }
      },
      "middle": {
          "dimension": {
              "value": 20
          },
          "feature": {
              "text": [{ // text as array; written on the cylinder face
                  "content": "Body text"
              }]
          }
      },
      "right": {
          "dimension": {
              "value": 30
          }
          // text for right side can be placed here (like above for the left side)
      },
      "meta": {}
  }

```

## Knurl
```js
{
  "type": "cylinder",
  "left": {
    "dimension": {
      "value": 30
    }
  },
  "middle": {
    "dimension": {
      "value": 20
    },
    "face": {
      "knurl": { // knurl
        "profile": "RAA",
        "angle": 0,
        "pitch": 0.8
      }
    }
  },
  "right": {
    "dimension": {
      "value": 30
    }
  },
  "meta": {}
}
```

### Thread
ToDo

### Boring
ToDo

### Radial Boring
ToDo

### Milling
ToDo
