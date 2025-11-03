**Title**: Form by ADC - v1.0 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Carly Huitema, Setayesh Sanavi 

**Date released**: 

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

The Form overlay extends OCA schemas with detailed form structure and presentation metadata. It allows schema authors to define multi-page layouts with organized sections, questions, and interactive elements, while supporting multiple languages.

Each Form overlay is language-specific, represented as a separate instance with its own SAID. All language versions reference the same capture_base and share identical UUIDs, ensuring structural consistency across translations.

The Form overlay enables the creation of structured, user-friendly data collection interfaces by supporting:
1. Page Organization – Define multiple pages with a clear, ordered layout.
2. Section Grouping – Organize questions within pages using named sections.
3. Question Attributes – Reference schema attributes as individual form questions.
4. Multi-language Support – Provide labels, descriptions, and placeholders in multiple languages using ISO 639-2 three-letter codes.
5. Interactive Elements – Configure input types, options, placeholders, and descriptions for each question.
6. Navigation Structure – Specify page order and sidebar navigation labels.


**Canonicalization Rules**:

The ordering overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/ordering/1.0)
4) language (Three-letter ISO 639-2 language code)
5) pages (Array of page structures)
6) page_order (Array of page identifiers)
7) page_labels (Object mapping identifiers to labels)
8) sidebar_label (Object mapping page identifiers to sidebar labels)
9) description (Object mapping identifiers/attributes to descriptions)
10) title (Form title string or empty string)
11) interaction (Array containing interaction configurations)

Next, the Form overlay enforces strict structural and serialization rules to ensure consistency across languages and implementations. All object properties and identifiers must be alphabetically or lexicographically ordered, according to [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3), while arrays follow the intended display sequence.

Each overlay instance is language-specific, defined using ISO 639-2 codes, with all identifiers referencing valid pages, sections, or attributes. For SAID generation, JSON must be serialized in a fully compact format without extra whitespace or line breaks. 

**Example**: 

**English Version:**
```json
{
  "d": "EL60wLpkzmWRMl7rNEY3xTNMMxVcdJoCiQDtymyNAE8A",
  "capture_base": "EJy00qaLu-iDKiciQykUt0j04xtRacUhyZoT-ZWch-uC",
  "type": "community/overlays/adc/form/1.1",
  "language": "eng",
  "pages": [
    {
      "attribute_order": ["name", "age"],
      "named_section": "page-uuid-1"
    }
  ],
  "page_order": ["page-uuid-1"],
  "page_labels": {
    "page-uuid-1": "Personal Information"
  },
  "sidebar_label": {
    "page-uuid-1": "Personal Info"
  },
  "description": {
    "page-uuid-1": "Please provide your personal details."
  },
  "title": "Registration Form",
  "interaction": [
    {
      "arguments": {
        "name": {
          "type": "Text",
          "placeholder": "Full name"
        },
        "age": {
          "type": "Numeric",
          "placeholder": "Age in years"
        }
      }
    }
  ]
}
```

**French Version:**
```json
{
  "d": "EFHzTOG8bPbPCdjyMhxCpAk3-gOPRpx0S3W3cUqVtgp8",
  "capture_base": "EJy00qaLu-iDKiciQykUt0j04xtRacUhyZoT-ZWch-uC",
  "type": "community/overlays/adc/form/1.1",
  "language": "fra",
  "pages": [
    {
      "attribute_order": ["name", "age"],
      "named_section": "page-uuid-1"
    }
  ],
  "page_order": ["page-uuid-1"],
  "page_labels": {
    "page-uuid-1": "Informations personnelles"
  },
  "sidebar_label": {
    "page-uuid-1": "Info personnelle"
  },
  "description": {
    "page-uuid-1": "Veuillez fournir vos coordonnées personnelles."
  },
  "title": "Formulaire d'inscription",
  "interaction": [
    {
      "arguments": {
        "name": {
          "type": "Text",
          "placeholder": "Nom complet"
        },
        "age": {
          "type": "Numeric",
          "placeholder": "Âge en années"
        }
      }
    }
  ]
}
```

**Note**: Both versions use the same `capture_base`, same page UUID (`page-uuid-1`), and same attribute names, but have different SAIDs (`d`) due to language-specific content.



**Rules summary**: 
The Form overlay follows strict validation rules to ensure consistency, clarity, and interoperability. It must include all required top-level fields in canonical order, use ISO 639-2 language codes, and maintain alignment between page identifiers, sections, and schema attributes. Arrays and objects must be properly ordered and canonicalized for accurate SAID calculation. While optional elements such as titles, placeholders, input types, and nested sections are supported for flexibility, all identifiers and attributes must reference valid schema elements. Duplicate identifiers, invalid language codes, and undefined attributes are strictly prohibited to preserve structural integrity and reliable data representation.



**Test case**: 

```
```

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/) 
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)
