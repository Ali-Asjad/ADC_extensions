**Title**: Ordering by ADC: version: 1.0

**Authors**: Carly Huitema, Mathew Mozaffari

**Date released**: _date of version release_

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:
 Preserving the order of attributes and entry codes can be very important for understanding data and for data entry and display. This overlay lets creators specify the ordering of attributes and entry codes of a specific schema bundle.

**Canonicalization Rules**:
The ordering overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/adc/ordering/1.0)

Next, the overlay contains order_attributes and order_entry_codes which are ordered lexicographically according to [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3). 

Inside order_attributes is an array of attributes which are insertion ordered. Inside order_entry_codes are attributes which are ordered lexicographically, with arrays of entry codes for each attribute which are insertion ordered.

**Example**: 
 - Provide at least one example of the overlay which has been fully canonicalized and serialized (in JSON) for calculating the correct overlay SAID value. 
 - The capture_base SAID does not need to reference a specific capture_base but MUST be well formed. 
 - The capture_base example SAID is used in the calculations of the overlay SAID. 
 - The example MAY be formatted with line breaks and indentations, including reorganizing objects for readability after the SAID has been calculated.

```
{
  "d": "#####Ordering_overlay_SAID####",
  "type": "community/adc/ordering/1.0",
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
 - Each entry code (for each attribute) MUST appear at most once, and MAY appear zero times.


**Test case**: 
 - At least one fully worked example MUST be provided.
 - The worked example MUST be a fully canonicalized, JSON serialized oca_package with SAIDs calculated. 
 - The fully worked example MUST include a minimal set of capture_base and any other overlays that the documented overlay depends on and MAY include more overlays. 
 - The example MUST NOT be transformed for readability or altered in any way that would interfere with the reproducible calculation of the SAID directly from the test case example.

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/) 
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
