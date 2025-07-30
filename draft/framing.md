**Title**: Framing by ADC - v1.1

**Community Grouping**: community/adc/extension/v1.1

**Authors**: Carly Huitema, Paul Knowles, Steven Mugisha Mizero

**Date released**:

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**: Framing objects to ontologies and controlled vocabularies is critical for data interoperability and harmonization. This extension adds semantic context by linking schema objects to standardized external concepts. For example, a schema may use uM for units, while UCUM standardizes it as umol/L, enabling consistent interpretation across communities.

In OCA, three types of information are contextually framed:

1. **Attributes** where the schema attribute is framed to a term drawn from another concept such as an ontology or controlled vocabulary.
2. **Units** where a schema unit is framed to a unit drawn from another concept.
3. **Entry codes** where a schema entry code term is framed to a term drawn from another concept.

**Canonicalization Rules**:

The framing overlays begins with the canonical ordering of ADC extension overlays.

1. `d` (digest of the overlay)
2. `type` (community/overlay/adc/framing/1.1)
3. overlay properties (e.g. `attribute_framing`, `unit_framing`, `entry_code_framing`) and their conanicalization rules are defined in their respective overlays section.

**Example**:

**Capture base:** showing the schema attributes to be framed:

```
{
  "type": "spec/capture_base/1.0",
  "digest": "Etszl9LgLUjllI950rd2lO6rF5-BP_jGzXGBPkFZCZFA",
  "classification": "RDF106",
  "attributes": {
    "Albumin_concentration": "Numeric",
    "Glucose_concentration": "Numeric",
    "Sample _name": "Text",
    "Sample_type": "Text"
  },
  "flagged_attributes": []
}
```

**Unit overlay:** showing the schema units to be framed:

```
{
  "capture_base": "Etszl9LgLUjllI950rd2lO6rF5-BP_jGzXGBPkFZCZFA",
  "digest": "Ec3I2X4FNoPhi7Raqo1PE3nP977BN4It-ZMmqLvc6z_w",
  "type": "spec/overlays/unit/1.0",
  "metric_system": "",
  "attribute_units": {
    "Albumin_concentration": "mg/dL",
    "Glucose_concentration": "mg/dL"
  }
}
```

**Entry code overlay:** showing the schema entry codes to be framed:

```
{
  "capture_base": "Etszl9LgLUjllI950rd2lO6rF5-BP_jGzXGBPkFZCZFA",
  "digest": "EHg4AoXVKZrgFMN_c91qo4b9sgF3mWAtAtqn7no85Ldo",
  "type": "spec/overlays/entry_code/1.0",
  "attribute_entry_codes": {
    "Sample_type": [
      "BLD001",
      "BLD002",
      "BLD003",
      "BLD004",
      "BLD005"
    ]
  }
}

// Entry Overlay

{
  "capture_base": "Etszl9LgLUjllI950rd2lO6rF5-BP_jGzXGBPkFZCZFA",
  "digest": "EiX132uHOFWph3kwBvjnkalbGDYagttuKr97olGRLOy4",
  "type": "spec/overlays/entry/1.0",
  "language": "en",
  "attribute_entries": {
    "Sample_type": {
      "BLD001": "No_preserv_no_anti-coag",
      "BLD002": "K2_EDTA",
      "BLD003": "sodium_citrate",
      "BLD004": "sodium_heparin",
      "BLD005": "acid_citrate_dextrose"
    }
  }
}

```

### Framing Overlays and Relationships

To describe the framing relationship between OCA schema objects and external concepts, the [Simple Standard for Sharing Ontological Mappings](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9216545/) (SSSOM) [1](<(https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9216545/)>) is used.

Only the four required SSSOM metadata elements are utilized:

| OCA                       | SSSOM                  |
| ------------------------- | ---------------------- |
| attribute/unit/entry_code | subject_id             |
| term_id                   | object_id              |
| predicate_id              | predicate_id           |
| framing_justification     | matching_justification |

As mentioned above, there are three type of information in OCA being framed, thus three types of framing overlays: Attribute framing overlay, Unit framing overlay, and Entry code framing overlay.

Each framing overlay type can have more than one overlays of the same variant. Each variant is of a single source of external concept being used to frame the OCA schema objects.

With this after after adding the `d` and `type`,`framing_metadata` MUST follow.

```
// the structure of framing metadata

"framing_metadata": {
    "frame_id": "SNOMEDCT", // Identifier of resource (SAIDs, DOIs, PURLs, or common names e.g. UCUM)
    "frame_label": "Systematized Nomenclature of Medicine Clinical Terms", // Label of resource (e.g. Unified Code for Units of Measure)
    "frame_location": "https://bioportal.bioontology.org/ontologies/SNOMEDCT", // Location of resource (e.g. https://ucum.org/)
    "frame_version": "2023AA" // Resource version (e.g. 2.1).
  },
```

**Attribute framing overlay example**

```
"attribute_framing":{
  "d": "XXXX",
  "type": "spec/overlays/attribute_framing/1.1",
  "framing_metadata": {
    "id": "SNOMEDCT",
    "label": "Systematized Nomenclature of Medicine Clinical Terms",
    "location": "https://bioportal.bioontology.org/ontologies/SNOMEDCT",
    "version": "2023AA"
  },
  "attributes": {
    "Albumin_concentration": {
      "framing_justification": "semapv:ManualMappingCuration",
      "predicate_id": "skos:exactMatch",
      "term_id": ""
    },
    "Glucose_concentration": {
      "framing_justification": "semapv:ManualMappingCuration",
      "predicate_id": "skos:exactMatch",
      "term_id": ""
    },
    "Sample_type": {
      "framing_justification": "semapv:ManualMappingCuration",
      "predicate_id": "skos:exactMatch",
      "term_id": ""
    }
  }
}
```

**Unit framing overlay example**

```
"unit_framing":{
  "d": "XXXX",
  "type": "spec/overlays/unit_framing/1.1",
  "framing_metadata": {
    "id": "UCUM",
    "label": "",
    "location": "https://ucum.org/",
    "version": ""
  },
  "units": {
    "mg/dL": {
      "framing_justification": "semapv:ManualMappingCuration"
      "predicate_id": "skos:exactMatch",
      "term_id": "mg/dL"
    }
  }
}
```

**Entry code framing overlay example**

```
"entry_code_framing":{
  "d": "XXXXX",
  "type": "spec/overlays/entry_code_framing/1.1",
  "framing_metadata": {
    "id": "SNOMEDCT",
    "label": "Systematized Nomenclature of Medicine Clinical Terms",
    "location": "https://bioportal.bioontology.org/ontologies/SNOMEDCT",
    "version": "2023AA"
  },
  "entry_codes": {
    "Sample_type": {
      "BLD001": {
        "framing_justification": "semapv:ManualMappingCuration"
        "predicate_id": "skos:closeMatch",
        "term_id": ""
      },
      "BLD002": {
        "framing_justification": "semapv:ManualMappingCuration",
        "predicate_id": "skos:broadMatch",
        "term_id": ""
      },
      "BLD003": {
        "framing_justification": "semapv:ManualMappingCuration",
        "predicate_id": "skos:broadMatch",
        "term_id": ""
      },
      "BLD004": {
        "framing_justification": "semapv:ManualMappingCuration",
        "predicate_id": "skos:broadMatch",
        "term_id": ""
      },
      "BLD005": {
        "framing_justification": "semapv:ManualMappingCuration",
        "predicate_id": "skos:broadMatch",
        "term_id": ""
      }
    }
  }
}
```

## Reference

### Rules for framing overlays

- For each framing overlay there must be a frame_id
- Within each overlay framing type (attribute, unit or entry_code) each frame_id must be unique.
- Not every term must be framed
- For each attribute or entry_code framing there can be only one skos:exactMatch per term.
  - Refer to Unresolved Questions for discussion on if other ontologies can be used for framing (e.g. owl:sameAs)
- For unit framing, each unit used in a schema can be framed only once.
- For unit framing, each unit can only be framed using skos:exactMatch
  - Refer to Unresolved Questions for discussion on if other ontologies can be used for framing (e.g. owl:sameAs)

### Predicate_id

Recommended to use skos terms for the mapping vocabulary (although other mapping schemas would be supported such as owl:)
|Skos term|Description|
|---|---|
|skos:closeMatch|closeMatch is used to link two concepts that are sufficiently similar that they can be used interchangeably in some information retrieval applications. In order to avoid the possibility of "compound errors" when combining mappings across more than two concept schemes, skos:closeMatch is not declared to be a transitive property.|
|skos:exactMatch|exactMatch is used to link two concepts, indicating a high degree of confidence that the concepts can be used interchangeably across a wide range of information retrieval applications. skos:exactMatch is a transitive property, and is a sub-property of skos:closeMatch.|
|skos:broadMatch|<A> skos:broadMatch <B> where B is broader than A. broadMatch is used to state an associative mapping link between two concepts.|
|skos:narrowMatch|<A> skos:narrowMatch <B> where B is narrower than A. skos:narrowMatch is owl:inverseOf the property skos:broadMatch.|
|skos:relatedMatch|relatedMatch is used to state an associative mapping link between two concepts.|

Source: [SKOS mapping vocabulary](https://www.w3.org/TR/skos-reference/#mapping)

### Framing_justification

Recommended to use the semapv terms for framing justification although other justification schemas would be supported.
|Semapv term|Description|
|---|---|
|semapv:MappingReview|A process that is concerned with determining if a mapping candidate (otherwise determined) is reasonable/correct.|
|semapv:ManualMappingCuration|A matching process that is performed by a human agent and is based on human judgment and domain knowledge.|
|semapv:LogicalReasoning|A matching process based on the inferences made by a logical reasoner.|
|semapv:LexicalMatching|A matching process based on a lexical comparison between one or more syntactic features of the subject with one or more syntactic features of the object.|
|semapv:CompositeMatching|A matching process based on multiple, possibly intertwined, matching approaches.|
|semapv:UnspecifiedMatching|A matching process based on an unspecified comparison.|
|semapv:SemanticSimilarityThresholdMatching||A matching process based on a minimum threshold of a score from a comparison based on a semantic similarity algorithm.|
|semapv:LexicalSimilarityThresholdMatching|A lexical matching process based on a minimum threshold of a score from a comparison based on a lexical similarity algorithm.|
|semapv:MappingChaining|A matching process based on the traversing of multiple mappings.|

Source: SEMAPV: [A Vocabulary for Semantic Mappings](https://github.com/mapping-commons/semantic-mapping-vocabulary) and [use in SSSOM](https://mapping-commons.github.io/sssom/mapping_justification/)

**Canonicalization Rules**:

**Example**:

```

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
