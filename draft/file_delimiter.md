**Title**: File delimiters by ADC - v1.1 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Ali Asjad

**Date released**:

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

The File delimiters overlay standardizes how delimited text files (commonly .csv) are produced and consumed for a schema bundle. It defines the delimiter character and related serialization parameters that vary by locale and toolchain. This addresses internationalization concerns where, for example, semicolons (;) or tabs (\t) are used instead of commas when the comma is a decimal separator.

This overlay works alongside other presentation/formatting overlays. For example, numeric rendering (e.g., the character used as a decimal separator) is governed by the `decimal_separator` overlay, while the character that separates fields in exported/imported files is governed here by `file_delimiter`.

Keys defined by this overlay:
- `delimiter` (string, REQUIRED): The single-character field delimiter used between values. Allowed examples include ",", ";", "\t" (tab), and "|". Custom single-character Unicode delimiters are allowed; the value MUST represent exactly one Unicode code point in JSON string form.
- `data_start_row` (integer, OPTIONAL): The 1-based row index at which data rows begin. MUST be a positive integer. Row counting starts at 1. For example, `2` indicates that the data begins on row 2.
- `quote_char` (string, OPTIONAL): Character used to quote fields, default is `"` (double quote) if omitted.
- `escape_char` (string, OPTIONAL): Character used to escape `quote_char` inside quoted fields. If omitted, defaults to the same value as `quote_char`.
- `line_terminator` (string, OPTIONAL): Line break sequence for rows (e.g., "\n" or "\r\n"). If omitted, consumers MAY auto-detect; producers SHOULD default to "\n" unless platform constraints require otherwise.

This overlay does not change attribute semantics. It specifies file-level serialization behavior so CSV/TSV-like files can be correctly generated and parsed across locales.

**Canonicalization Rules**:

The file_delimiter overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/file_delimiter/1.1)
4) delimiter (string)
5) escape_char (string) (optional)
6) data_start_row (integer) (optional)
7) line_terminator (string) (optional)
8) quote_char (string) (optional)

Object properties MUST follow [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3). Arrays, if present, are insertion ordered. For SAID generation, JSON MUST be serialized in a fully compact form with no extraneous whitespace.

**Example**:

The following is a canonicalized overlay object. The SAID values are illustrative.

```
"file_delimiter": {
  "d": "EG3oB8w6wJ7wQm3m5k5tGzj5n2mK3D0tq8qg3lH8s9cY",
  "capture_base": "EIQhXN6TmYZDHixCkPBDu9LfM9k2u9Ek_iJmpRBszqbI",
  "type": "community/overlays/adc/file_delimiter/1.1",
  "delimiter": ";",
  "escape_char": "\"",
  "data_start_row": 2,
  "line_terminator": "\n",
  "quote_char": "\""
}
```

**Rules summary**:

- `delimiter` MUST be present and MUST represent exactly one Unicode code point as a JSON string (e.g., ",", ";", "|", or "\t" for tab).
- If `quote_char` is omitted, it defaults to `"` (double quote). If `escape_char` is omitted, it defaults to the same value as `quote_char`.
- If `line_terminator` is omitted, producers SHOULD use "\n" unless target environments require "\r\n"; consumers MAY auto-detect.
- If `data_start_row` is present, it MUST be a positive integer and row counting starts at 1. For example, `1` indicates data begins on the first row; `2` indicates a single header row.
- This overlay MUST NOT alter attribute semantics or numeric formatting; those concerns are addressed by other overlays (e.g., `decimal_separator`).

**Test case**:

The following is a fully canonicalized JSON oca_package with SAIDs populated for demonstrative purposes, including a minimal `capture_base` and the `file_delimiter` overlay in the ADC extensions. Values are compact and suitable for SAID calculation reproduction.

```
{"d":"EHg0k6g1B3Y6b4Z1b2J8dZgqB9iS0mQf2kR3yT8uV0Xa","type":"oca_package/1.0","oca_bundle":{"v":"OCAA11JSON000411_","bundle":{"v":"OCAS11JSON0003xZ_","d":"EB5d8hHq3Sg4a9VwT2MbL0cN7yQe6Rj3pP1Km8Do5UeZ","capture_base":{"d":"EIQhXN6TmYZDHixCkPBDu9LfM9k2u9Ek_iJmpRBszqbI","type":"spec/capture_base/1.1","attributes":{"amount":"Text","name":"Text"},
"classification":"","flagged_attributes":[]},"overlays":{}}},"dependencies":[]}
,"extensions":{"adc":{"EIQhXN6TmYZDHixCkPBDu9LfM9k2u9Ek_iJmpRBszqbI":{"d":"EP7b1wQe9Lk2N3vH8yR5fG6tD1cS4mV0XzAaQpLsWu3J","type":"community/adc/extension/1.0","overlays":{"file_delimiter":{"d":"EG3oB8w6wJ7wQm3m5k5tGzj5n2mK3D0tq8qg3lH8s9cY","type":"community/overlays/adc/file_delimiter/1.1","delimiter":";","escape_char":"\\\"","data_start_row":2,"line_terminator":"\n","quote_char":"\\\""}}}}}}
```

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/)
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)


