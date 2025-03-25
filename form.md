**Title**: Form by ADC - v1.0 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Carly Huitema, Setayesh Sanavi 

**Date released**: 

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:


**Canonicalization Rules**:

The ordering overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/ordering/1.0)

Next, the overlay contains attributes_ordering and entry_code_ordering which are ordered lexicographically according to [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3). 

Inside attribute_ordering is an array of attributes which are insertion ordered. Inside entry_code_ordering are attributes which are ordered lexicographically, with arrays of entry codes for each attribute which are insertion ordered.

**Example**: 

```
https://github.com/ClimateSmartAgCollab/questionnaire/blob/main/public/test.json

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
