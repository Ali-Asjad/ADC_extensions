**Title**: Sensitive by ADC - v1.1 - DRAFT

**Community Grouping**: community/adc/extension/vXX

**Authors**: Steven Mugisha Mizero, Carly Huitema

**Date released**: May 15, 2025

This overlay follows official OCA Package requirements documented at [https://github.com/agrifooddatacanada/OCA_package_standard](https://github.com/agrifooddatacanada/OCA_package_standard)

**Description**:

This overlay corrects for the missing sensitive (aka flagged) attributes that were previously in the capture base. This information is now in a new sensitive overlay.

**Canonicalization Rules**:

The ordering overlay begins with the canonical ordering of OCA overlays.
1) d (digest of the overlay)
2) capture_base (capture base SAID the overlay is specific to)
3) type (community/overlays/adc/range/1.1)

Then there is the sensitive_attributes object with an array of sensitive attributes in lexicographical order.

**Example**: 

```
{
  "d": "EAgeUSa7JMG9oxJHUKTEBz4chJLWE5ayTq2rvBHo_P5R",
  "type": "community/overlays/adc/sensitive/1.1",
  "sensitive_attributes": [
    "farm",
    "latitude",
    "longitude",
    "samplers"
  ]
}
```


**Rules summary**: 
- only attributes which are listed in the capture base can appear in the sensitive overlay.
- 


**Test case**: 

```
{"d":"EMFKLEzNwa2syVcviH1cq_iFw-tbEp0HccCzxJFMC6ID","type":"oca_package/1.0","oca_bundle":{"v":"OCAA11JSON0012df_","bundle":{"v":"OCAS11JSON0012c2_","d":"EJG-0Kbhxs1d4JR3pAaOmBcQF-siH9DP2c_byyFsjV32","capture_base":{"d":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/capture_base/1.1","attributes":{"collect_date":"DateTime","collect_time":"DateTime","date_in":"DateTime","date_out":"DateTime","duration":"DateTime","farm":"Text","final_mass":"Numeric","initial_mass":"Numeric","latitude":"Text","longitude":"Text","moisture":"Numeric","paddock_id":"Numeric","sample_id":"Text","sample_type":"Text","samplers":["Text"],"temperature":"Numeric","time_in":"DateTime","time_out":"DateTime"},"classification":"RDF401","flagged_attributes":[]},"overlays":{"entry":[{"d":"ECUgIzLlZXBMhFbx-AdPxhBnfpN189yyup4yK4GoX3tU","capture_base":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/overlays/entry/1.1","language":"eng","attribute_entries":{"farm":{"A":"Hensall farm","B":"Guelph farm north","C":"Guelph farm south","D":"Lakeridge farm"},"samplers":{"Aedan":"Aedan","Isabella":"Isabella","Lila":"Lila","Makhi":"Makhi","Nathan":"Nathan","Zara":"Zara"}}}],"entry_code":{"d":"EDsl7KOkieN90UXtCedSIUsCtJIiqHTK8Ii-hwFw84Ls","capture_base":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/overlays/entry_code/1.1","attribute_entry_codes":{"farm":["A","B","C","D"],"samplers":["Aedan","Isabella","Lila","Makhi","Nathan","Zara"]}},"format":{"d":"EE9m3B-pSvlfqJEOi2nyIOMsgBJjEfx3KSsSdoYNodeg","capture_base":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/overlays/format/1.1","attribute_formats":{"collect_date":"^(\\d{4})-(0[1-9]|1[0-2])-(0[1-9]|[12]\\d|3[01])$","collect_time":"^([01]\\d|2[0-3]):([0-5]\\d):([0-5]\\d)$","date_in":"^(\\d{4})-(0[1-9]|1[0-2])-(0[1-9]|[12]\\d|3[01])$","date_out":"^(\\d{4})-(0[1-9]|1[0-2])-(0[1-9]|[12]\\d|3[01])$","duration":"^P(?!$)((\\d+Y)|(\\d+\\.\\d+Y))?((\\d+M)|(\\d+\\.\\d+M))?((\\d+W)|(\\d+\\.\\d+W))?((\\d+D)|(\\d+\\.\\d+D))?(T(?=\\d)((\\d+H)|(\\d+\\.\\d+H))?((\\d+M)|(\\d+\\.\\d+M))?(\\d+(\\.\\d+)?S)?)?$","farm":"^[A-Z]*$","final_mass":"^[-+]?\\d*\\.?\\d+$","initial_mass":"^[-+]?\\d*\\.?\\d+$","latitude":"^[NS]\\s?(?:[0-8]?\\d)°\\s?(?:[0-5]?\\d)'?\\s?(?:[0-5]?\\d(?:\\.\\d+)?)\\\"?$","longitude":"^[EW]\\s?(?:1[0-7]\\d|0?\\d{1,2})°\\s?(?:[0-5]?\\d)'?\\s?(?:[0-5]?\\d(?:\\.\\d+)?)\\\"?$","moisture":"^[-+]?\\d*\\.?\\d+$","paddock_id":"^-?[0-9]+$","sample_id":"^.{0,250}$","sample_type":"^.{0,50}$","temperature":"^[-+]?\\d*\\.?\\d+$","time_in":"^([01]\\d|2[0-3]):([0-5]\\d):([0-5]\\d)$","time_out":"^([01]\\d|2[0-3]):([0-5]\\d):([0-5]\\d)$"}},"information":[{"d":"EM_eBnd5d7Td0hvEn1URDvQDVcyOgisRf-EaMakdpLv8","capture_base":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/overlays/information/1.1","language":"eng","attribute_information":{"collect_date":"The date of sample collection","collect_time":"The time of sample collection","date_in":"The date the sample entered the lab","date_out":"The date the sample left the lab","duration":"The duration of the sample collection","farm":"The farm where the sample was collected","final_mass":"The final mass of the sample","initial_mass":"The initial mass of the sample","latitude":"The latitude where the sample was taken","longitude":"The longitude where the sample was taken","moisture":"The moisture content of the sample","paddock_id":"The paddock ID where the sample was collected","sample_id":"The unique identifier for the sample","sample_type":"The type of sample","samplers":"The people who collected the sample","temperature":"The temperature at the time of sample collection","time_in":"The time the sample entered the lab","time_out":"The time the sample left the lab"}}],"label":[{"d":"EM4mKhHhuYtz7Rycrw1K289IxxXwOHyqLy8A60FUZOg_","capture_base":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/overlays/label/1.1","language":"eng","attribute_categories":[],"attribute_labels":{"collect_date":"Collection Date","collect_time":"Collection Time","date_in":"Date In","date_out":"Date Out","duration":"Duration","farm":"Farm","final_mass":"Final Mass","initial_mass":"Initial Mass","latitude":"Latitude","longitude":"Longitude","moisture":"Moisture","paddock_id":"Paddock ID","sample_id":"Sample ID","sample_type":"Sample Type","samplers":"Samplers","temperature":"Temperature","time_in":"Time In","time_out":"Time Out"},"category_labels":{}}],"meta":[{"d":"EMKwjHRm8hIF8GK0dOGioXgwZfqf_zcPszXj_6s_mMQ7","capture_base":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/overlays/meta/1.1","language":"eng","description":"A schema describing soil samples together with water content measurements.","name":"soil"}],"unit":{"d":"ENZg3YRCFINxFNxAUXlQWTAXpFRok2MXQnXiMrbF285W","capture_base":"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt","type":"spec/overlays/unit/1.1","attribute_unit":{"final_mass":"g","initial_mass":"g","moisture":"%","temperature":"C"}}}},"dependencies":[]},"extensions":{"adc":{"EEs4WAywiDY8ScSrCWsw4fm75q9sdHeEnfP6S60cTsCt":{"d":"EA5jZlZmc6Y46SBStwqdYsKc-HvadmzZO9zB6EDVTb2z","type":"community/adc/extension/1.0","overlays":{"ordering":{"d":"EPOY9fKzN2jfV3xjCWW7XotenGgQsQryS5KfI6vJyedK","type":"community/overlays/adc/ordering/1.1","attribute_ordering":["farm","sample_type","collect_date","collect_time","latitude","longitude","duration","paddock_id","samplers","sample_id","date_in","temperature","time_in","initial_mass","date_out","final_mass","time_out","moisture"],"entry_code_ordering":{"farm":["A","B","C","D"],"samplers":["Aedan","Isabella","Lila","Makhi","Nathan","Zara"]}},"unit_framing":{"d":"EKUN0h-2nIBevAN9SMmsgQfITjrOdB_qkfIiL7u7D8a1","type":"community/overlays/adc/unit_framing/1.1","framing_metadata":{"id":"UCUM","label":"Unified Code for Units of Measure","location":"https://ucum.org/","version":""},"units":{"%":{"framing_justification":"semapv:ManualMappingCuration","predicate_id":"skos:exactMatch","term_id":""},"C":{"framing_justification":"semapv:ManualMappingCuration","predicate_id":"skos:exactMatch","term_id":""},"g":{"framing_justification":"semapv:ManualMappingCuration","predicate_id":"skos:exactMatch","term_id":""},"undefined":{"framing_justification":"semapv:ManualMappingCuration","predicate_id":"skos:exactMatch","term_id":""}}},"sensitive":{"d":"EAgeUSa7JMG9oxJHUKTEBz4chJLWE5ayTq2rvBHo_P5R","type":"community/overlays/adc/sensitive/1.1","sensitive_attributes":["farm","latitude","longitude","samplers"]}}}}}}
```

## Normative references
- [OCA specification v1.0.1](http://oca.colossi.network/specification/) 
- [3.2.3 Sorting of Object Properties](https://www.rfc-editor.org/rfc/rfc8785#section-3.2.3)
- [CESR Specification](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html) for SAID calculations
- [OCA Package Standard](https://github.com/agrifooddatacanada/OCA_package_standard)
