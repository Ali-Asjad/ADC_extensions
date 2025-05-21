**Title**: Example by ADC - v1.1 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Carly Huitema, Paul Knowles

**Date released**: 

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

This overlay adds examples (in multiple languages) to a schema.

**Canonicalization Rules**:

The ordering overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/example/1.1)

Then there objects with the name of each attribute which are lexicographically ordered and the contents of each attribute named object are also lexicographically ordered.

**Example**: ??? (are these still up to date?)

```
"example":{
  "capture_base": "Etszl9LgLUjllI950rd2lO6rF5-BP_jGzXGBPkFZCZFA",
  "digest": "XXXX",
  "type": "spec/overlays/example/1.0",
  "language": "eng",
  "examples": {
    "Albumin_concentration": "52.69",
    "Glucose_concentration": "8.7",
    "Sample _name": "Carlys_sample",
    "Sample_type": "BLD003"
  }
}

{
  "capture_base": "Etszl9LgLUjllI950rd2lO6rF5-BP_jGzXGBPkFZCZFA",
  "digest": "XXXX",
  "type": "spec/overlays/example/1.0",
  "language": "ar",
  "examples": {
    "Albumin_concentration": "52.69",
    "Glucose_concentration": "8.7",
    "Sample _name": "عينة",
    "Sample_type": "BLD003"
  }
}
```


**Rules summary**: 



**Test case**: 

```

```

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/) 
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)
