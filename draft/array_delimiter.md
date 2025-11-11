**Title**: Array Delimiter by ADC - v1.1 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Ali Asjad

**Date released**: Intentionally left empty

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

Array delimiter define how multiple values are represented within a single data field (cell) in flat/tabular files (e.g., CSV/TSV). This overlay specifies the character used to separate elements of such in-cell arrays and, optionally, attribute-specific overrides and quoting/escaping behavior for robust parsing across locales.

This is distinct from the file (field) delimiter configured by a file delimiter overlay (e.g., “,”, “;”, “\t”). Implementations MUST avoid ambiguity between the field delimiter and the array delimiter, or MUST use quoting/escaping rules that make parsing unambiguous. This overlay improves interoperability when attributes contain lists such as tags, multiple selections, or coordinate pairs in internationalized environments.

Keys defined by this overlay:
- `delimiter` (string, REQUIRED): Default in-cell array delimiter. MUST be exactly one Unicode code point in JSON string form (e.g., “|”, “;”, “,”, “\t”).
- `attributes` (object, OPTIONAL): Per-attribute overrides, keyed by attribute name. Each value is an object supporting:
  - `delimiter` (string, OPTIONAL): Attribute-specific array delimiter; same single-code-point requirement.
  - `element_quote_char` (string, OPTIONAL): Character used to quote individual array elements, default `"` if omitted.
  - `element_escape_char` (string, OPTIONAL): Character used to escape `element_quote_char` within an element. Defaults to the same value as `element_quote_char` if omitted.
  - `trim_whitespace` (boolean, OPTIONAL): If true, leading/trailing ASCII whitespace around unquoted elements SHOULD be trimmed during parse and SHOULD NOT be added during generation.
  - `allow_empty_elements` (boolean, OPTIONAL): If true, empty elements between adjacent delimiters are permitted and must be preserved in round-trip.

This overlay does not change attribute semantics; it specifies how lists are serialized into single fields for file-based exchange.

**Canonicalization Rules**:

The array_delimiter overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/array_delimiter/1.1)

All other object properties MUST follow [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3). Arrays, if present, are insertion ordered. For SAID generation, JSON MUST be serialized in a fully compact form without extraneous whitespace.

**Example**:

The following is a canonicalized overlay object. SAID values are illustrative.

```
"array_delimiter": {
  "d": "EGYdY1b3Yp0jM2qR7kQvFfT2mKf3sVb0cWn9xZp8Lu1H",
  "capture_base": "EIQhXN6TmYZDHixCkPBDu9LfM9k2u9Ek_iJmpRBszqbI",
  "type": "community/overlays/adc/array_delimiter/1.1",
  "attributes": {
    "coordinates": {
      "delimiter": ";",
      "trim_whitespace": false
    },
    "tags": {
      "delimiter": "|",
      "element_quote_char": "\"",
      "element_escape_char": "\"",
      "trim_whitespace": true,
      "allow_empty_elements": false
    }
  },
  "delimiter": "|"
}
```

**Rules summary**:

- `delimiter` MUST be present and MUST represent exactly one Unicode code point as a JSON string.
- `attributes` MAY provide per-attribute overrides; attribute names MUST exist in the capture_base.
- If `element_quote_char` is omitted, it defaults to `"`. If `element_escape_char` is omitted, it defaults to `element_quote_char`.
- If `trim_whitespace` is true, implementations SHOULD trim only when elements are not quoted.
- If `allow_empty_elements` is true, adjacent delimiters represent empty elements and MUST be preserved in parse and generation.
- The array delimiter SHOULD NOT be the same as the file (field) delimiter unless quoting/escaping renders parsing unambiguous.
- This overlay MUST NOT alter underlying data semantics or numeric formatting (see `decimal_separator` for decimal rendering).

**Test case**:

A fully canonicalized JSON oca_package with SAIDs populated for demonstrative purposes, including a minimal capture_base and the array_delimiter overlay in ADC extensions. Values are compact for SAID calculation reproduction.

```
{"d":"EHn2q6d3P5w0Xa9V4b7Kc2LmQ8sR1Tz6Ue3Jg0Mi5NoP","type":"oca_package/1.0","oca_bundle":{"v":"OCAA11JSON000411_","bundle":{"v":"OCAS11JSON0003xZ_","d":"EC8t4aVr6Qe1n9YwM2Kc5Lb0Jr7Hu3Do1Pz6Xg4Tf8Ui","capture_base":{"d":"EIQhXN6TmYZDHixCkPBDu9LfM9k2u9Ek_iJmpRBszqbI","type":"spec/capture_base/1.1","attributes":{"coordinates":"Text","tags":"Text"},"classification":"","flagged_attributes":[]},"overlays":{}}},"dependencies":[]},"extensions":{"adc":{"EIQhXN6TmYZDHixCkPBDu9LfM9k2u9Ek_iJmpRBszqbI":{"d":"EPb7y1Qe0Lk2R3vH8yR5fG6tD1cS4mV0XzAaQpLsWu3J","type":"community/adc/extension/1.0","overlays":{"array_delimiter":{"d":"EGYdY1b3Yp0jM2qR7kQvFfT2mKf3sVb0cWn9xZp8Lu1H","type":"community/overlays/adc/array_delimiter/1.1","attributes":{"coordinates":{"delimiter":";","trim_whitespace":false},"tags":{"allow_empty_elements":false,"delimiter":"|","element_escape_char":"\\\"","element_quote_char":"\\\"","trim_whitespace":true}},"delimiter":"|"}}}}}}
```

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/)
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)


