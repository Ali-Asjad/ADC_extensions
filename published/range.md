**Title**: Range by ADC - v1.1

**Community Grouping**: community/adc/extension/vXX

**Authors**: Carly Huitema, Paul Knowles, Ryan Barrett

**Date released**: 25-05-2026

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

This overlay adds minimum and maximum values (inclusive or exclusive) for attributes with either numeric or date/time datatypes.

**Canonicalization Rules**:

The range overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/range/1.1)

Then there objects with the name of each attribute which are lexicographically ordered and the contents of each attribute named object are also lexicographically ordered.

**Example**: 

```
"range": {
            "d": "EMta65hl_7m-_1Arw_xDsLm5Ac1c-gFiTLxnXE8Ck46D",
            "capture_base": "EIQhXN6TmYZDHixCkPBDu9LfM9k2u9Ek_iJmpRBszqbI",
            "type": "community/overlays/adc/range/1.1",
            "attributes": {
              "attr_1": {
                "lower": "10",
                "lower_inclusive": true,
                "upper": "20",
                "upper_inclusive": true
              },
              "attr_2": {
                "lower": "2000-05-11",
                "lower_inclusive": true,
                "upper": "2005-05-11",
                "upper_inclusive": false
              }
            }
          }
```


**Rules summary**: 
- Only attributes with datatype Numeric or DateTime MAY have a range value
- A Numeric or DateTime datatype attribute MAY have a lower bound, an upper bound, or both
- If a lower and/or upper bound is given it MUST also include the appropriate lower_inclusive or upper_inclusive value which MUST be either true or false.
- The lower value MUST be lower than the upper value
- The format of the lower and upper values MUST match the format overlay


**Test case**: 

```
{"d":"EJP5d2We2-IK3EDpXI3iQDJxYUcx-rGVgDoW08f_3v5Z","type":"oca_package/1.0","oca_bundle":{"v":"OCAA11JSON0002fe_","bundle":{"v":"OCAS11JSON0002e1_","d":"EFKCawe2eHCk_bNFtFiOha32FSaS1U_O-3RNEVBwLRLM","capture_base":{"d":"EMV5IVcCcY78c8LuFuYAhQjVUFPRyMQchLYQo7qvOfbx","type":"spec/capture_base/1.1","attributes":{"RangeTestData":"Numeric"},"classification":"RDF106","flagged_attributes":[]},"overlays":{"format":{"d":"EDUU56TKUL4kahy1AGzfSIB8sOBX7JJjuv52vMQ-SP-i","capture_base":"EMV5IVcCcY78c8LuFuYAhQjVUFPRyMQchLYQo7qvOfbx","type":"spec/overlays/format/1.1","attribute_formats":{"RangeTestData":"^-?[0-9]+$"}},"meta":[{"d":"EJGW55JB6fNb7r0Tdnw8CJ8hqwiovSDVh_bocKNMJUht","capture_base":"EMV5IVcCcY78c8LuFuYAhQjVUFPRyMQchLYQo7qvOfbx","type":"spec/overlays/meta/1.1","language":"eng","description":"Schema generated for range overlay test","name":"TestSchema"}]}},"dependencies":[]},"extensions":{"adc":{"EMV5IVcCcY78c8LuFuYAhQjVUFPRyMQchLYQo7qvOfbx":{"d":"EKZjYN49Q2njt6tRc3eeA7J-5T31SjJVrPKhHiNyr-ma","type":"community/adc/extension/1.0","overlays":{"ordering":{"d":"EP-WgzX2XHwEzq7Dma4ZSz4PxRU3N2V_l3Gda5egXAbs","capture_base":"EMV5IVcCcY78c8LuFuYAhQjVUFPRyMQchLYQo7qvOfbx","type":"community/overlays/adc/ordering/1.0","attribute_ordering":["RangeTestData"],"entry_code_ordering":{}},"range":{"d":"EGlHuwbJRThDCLPTai68wukxgkJ90GaXd0AuEKoGrs6r","capture_base":"EMV5IVcCcY78c8LuFuYAhQjVUFPRyMQchLYQo7qvOfbx","type":"community/overlays/adc/range/1.0","attributes":{"RangeTestData":{"lower":"25","lower_inclusive":true,"upper":"75","upper_inclusive":true}}}}}}}}
```

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/) 
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)
