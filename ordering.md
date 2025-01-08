**Title**: Ordering by ADC - v1.0 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Carly Huitema, Mathew Mozaffari

**Date released**: 

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

Preserving the order of attributes and entry codes can be very important for understanding data and for data entry and display. This overlay lets creators specify the ordering of attributes and entry codes of a specific schema bundle.

**Canonicalization Rules**:

The ordering overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/ordering/1.0)

Next, the overlay contains ordering_attributes and ordering_entry_codes which are ordered lexicographically according to [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3). 

Inside ordering_attributes is an array of attributes which are insertion ordered. Inside ordering_entry_codes are attributes which are ordered lexicographically, with arrays of entry codes for each attribute which are insertion ordered.

**Example**: 

```
{
  "d": "#####Ordering_overlay_SAID####",
  "type": "community/overlays/adc/ordering/1.0",
  "capture_base": "EK4blRtJ8S2_R0JVGPLTMtyHViNEUaby4SQ5aICyxUJz",
  "ordering_attribute": [
    "q1",
    "q3",
    "q4",
    "q2"
  ],
  "ordering_entry_codes": {
    "q1": [
      "Google",
      "ISNI",
      "ORCiD",
      "ResearcherID",
      "Scopus"
    ],
    "q4": [
      "001",
      "002",
      "003",
      "004",
      "005"
    ]
  }
}
```


**Rules summary**: 
 - Every attribute present in this overlay MUST be present in the capture_base of the source schema.
 - Each entry code present in this overlay MUST be present in the entry overlay of the source schema.
 - Each attribute MUST appear at most once, and MAY appear zero times.
 - Each entry code (in an entry code set) MUST appear at most once, and MAY appear zero times.


**Test case**: 


## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/) 
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)
