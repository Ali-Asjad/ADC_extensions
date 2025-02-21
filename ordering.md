**Title**: Ordering by ADC - v1.0 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Carly Huitema, Mathew Mozaffari, Steven Mugisha Mizero 

**Date released**: 

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

Preserving the order of attributes and entry codes can be very important for understanding data and for data entry and display. This overlay lets creators specify the ordering of attributes and entry codes of a specific schema bundle.

**Canonicalization Rules**:

The ordering overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/ordering/1.0)

Next, the overlay contains attributes_ordering and entry_code_ordering which are ordered lexicographically according to [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3). 

Inside attribute_ordering is an array of attributes which are insertion ordered. Inside entry_code_ordering are attributes which are ordered lexicographically, with arrays of entry codes for each attribute which are insertion ordered.

**Example**: 

```
{
  "ordering": {
    "d": "EJkDEAtiYL8R4udU35f_4wjycpJWhc7LoL5r_5tvdh_g",
    "type": "community/overlays/adc/ordering/1.0",
    "capture_base": "EF70aJqYCa9cAHDaR7qTl_T-4PzdLX5Vq2bH-YvFxLnS",
    "attribute_ordering": [
      "identifier",
      "colour"
    ],
    "entry_code_ordering": {
      "identifier": [
        "ORCiD",
        "ISNI",
        "ResearcherID",
        "Scopus",
        "Google"
      ],
      "colour": [
        "001",
        "002",
        "003",
        "004",
        "005"
      ]
    }
  }
}
```


**Rules summary**: 
 - Every attribute present in this overlay MUST be present in the capture_base of the source schema.
 - Each entry code present in this overlay MUST be present in the entry overlay of the source schema.
 - Each attribute MUST appear at most once, and MAY appear zero times.
 - Each entry code (in an entry code set) MUST appear at most once, and MAY appear zero times.


**Test case**: 

```
{"d":"EMofjM6x9h2u_tlrfr7rtRjx2D9QRR_BSOON36kIyIW3","type":"oca_package/1.0","oca_bundle":{"v":"OCAA11JSON000517_","bundle":{"v":"OCAS11JSON0004fa_","d":"EJQo7742IeTKxbfojVU5rlfTTjYR_0YBVwXd2AGvOFME","capture_base":{"d":"EF70aJqYCa9cAHDaR7qTl_T-4PzdLX5Vq2bH-YvFxLnS","type":"spec/capture_base/1.0","attributes":{"colour":"Text","identifier":"Text"},"classification":"","flagged_attributes":[]},"overlays":{"entry":[{"d":"EMmTvA5iZbHx8VVE29-SkZkuucR2qDIkEBtvKA_nDTwd","capture_base":"EF70aJqYCa9cAHDaR7qTl_T-4PzdLX5Vq2bH-YvFxLnS","type":"spec/overlays/entry/1.0","language":"eng","attribute_entries":{"colour":{"001":"Red","002":"Green","003":"Blue","004":"Yellow","005":"Orange"},"identifier":{"Google":"Google","ISNI":"ISNI","ORCiD":"ORCiD","ResearcherID":"ResearcherID","Scopus":"Scopus"}}}],"entry_code":{"d":"EMB_ZFw4xJ55wfl8rCVvRuMnN0TkDfOPlANRoMMdTw5z","capture_base":"EF70aJqYCa9cAHDaR7qTl_T-4PzdLX5Vq2bH-YvFxLnS","type":"spec/overlays/entry_code/1.0","attribute_entry_codes":{"colour":["001","002","003","004","005"],"identifier":["Google","ISNI","ORCiD","ResearcherID","Scopus"]}},"meta":[{"d":"ECSNfFTNMueiIipGRm9Hf1eNpW68Z14j77Ec5tmsK8OA","capture_base":"EF70aJqYCa9cAHDaR7qTl_T-4PzdLX5Vq2bH-YvFxLnS","type":"spec/overlays/meta/1.0","language":"eng","description":"A schema to demonstrate the attribute ordering and entry code ordering functionalities.","name":"Demonstration schema"}]}},"dependencies":[]},"extensions":[{"d":"EOHL6EPw73yl4XUfAGSO1mKrgp_SqjvkBpSv9M9Lfk9d","type":"community/adc/extension/1.0","bundle_digest":"EJQo7742IeTKxbfojVU5rlfTTjYR_0YBVwXd2AGvOFME","overlays":{"ordering":{"d":"EJkDEAtiYL8R4udU35f_4wjycpJWhc7LoL5r_5tvdh_g","type":"community/overlays/adc/ordering/1.0","capture_base":"EF70aJqYCa9cAHDaR7qTl_T-4PzdLX5Vq2bH-YvFxLnS","attribute_ordering":["identifier","colour"],"entry_code_ordering":{"identifier":["ORCiD","ISNI","ResearcherID","Scopus","Google"],"colour":["001","002","003","004","005"]}}}}]}
```

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/) 
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)
