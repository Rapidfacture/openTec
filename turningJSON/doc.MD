# Docu of JSON format for turned parts



Turned parts are stored by an array of contour elements which hold further details (dimensions, features, etc.).

The basic document structure consists of three parts:

    {
        "meta": {}, // some meta info about drawing in this obj
        "innerContour": [], // array of contour elements
        "outerContour": [], // array of contour elements
    }


## Meta Information



The following meta information is used for the drawing:

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

Ideas: could also consist "size" (diameter/length), "weight".


## Contour elements


Inner and outer contour use the same structure for describing the contour.



### Example contour element



    [{
        "type": "cylinder",		// Elementtyp: Zylinder-, Konus- oder Kreiselement

        "meta": {			// Metadatenteil
            "index": 0,			// Index um die Elemente anzuordnen und zur vertauschen
            "selection": false,		// Element angewählt/selektiert
            "version": 0,		// Versionshistorie, Elemente speichern => „Bearbeiten Rückgängig“
            "dimension-type": 0	// Bemaßungsart bei Konus- oder Kreiselementen
        },
        "left": {			// Daten des linken Elementabschnitts
            "dimension": {		// Bemaßung; hier: das erste Durchmessermaß
                "value": 50,		// Wert in mm
                "tolerance-pos": 0.2	// Positiver Toleranzwert in mm
            }
        },
        "middle": {			// Daten des mittleren Elementabschnitts
            "dimension": {		// Bemaßung; hier: Längenbemaßung; relative d.h. Elementlänge
                "value": 20,		// Wert in mm
                "link-to-element": 0	// Verknüpfung des Längenmaßes zu anderen Elementen
            },
            "face": {			// Oberflächendefinition; hier: Bezug auf Mantelfläche
                "surface-roughness": 30	// Oberflächenrauheit Rz in µm
            }
        },
        "right": {			// Daten des rechten Elementabschnitts
            "dimension": {		// Bemaßung; hier: zweites Durchmessermaß
                "value": 50,		// Wert in mm
                "tolerance-neg": 0.2,	// Negativer Toleranzwert in mm
                "steady": "true"		// Stetige Verknüpfung des Durchmessers mit dem Nachbarelement
            },
            "edge": {			// Definition der Kante rechts
                "value": 2,		// Größe in mm
                "type": "radius"		// Typ: Radius, Fase oder Freistich
            },
            "feature": {			// Bearbeitungen auf der rechten Stirnfläche des Elements
                "groove": {}		// Nut
            }
        },
    },
    {} // next element ...
    ]
