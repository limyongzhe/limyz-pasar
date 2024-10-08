# Table name: Person

![image1](https://github.com/user-attachments/assets/5a0eeef4-06fc-4abb-90bf-f2ca9d65190f)

| | Destination field | Source field | Logic | Comment field |
| --- | --- | --- | --- | --- |
| 1 | person_id | anon_case_no | Autogenerated number for each distinct `anon_case_no`, based on the earliest visit (`session_start_date`) for each `anon_case_no`, and prioritizing non-null data using the following SQL code:<br><br>ROW_NUMBER() OVER (ORDER BY session_startdate, person_source_value) | Ensure `anon_case_no` uniquely identifies individuals, as it's not unique in the source. Note: non-idempotent process. |
| 2 | gender_concept_id | gender | MALE -> 8507<br>FEMALE -> 8532 | |
| 3 | year_of_birth | operation_startdate<br>age_time_of_surgery | YEAR(operation_startdate) - age_time_of_surgery | |
| 4 | month_of_birth | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |
| 5 | day_of_birth | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |
| 6 | birth_datetime | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |
| 7 | race_concept_id | race | Join with source_to_concept_map.source_code for the `race_concept_id` | Malaysian = nationality, from country Malaysia <br> Malay = of Malay descent. Can be from a different country e.g. China but be Malay descent <br><br> [Accepted Race Concepts](https://athena.ohdsi.org/search-terms/terms?domain=Race&standardConcept=Standard&page=3&pageSize=15&query=)
| 8 | ethnicity_concept_id | <i style="color:gray;">NULL</i> | 0 | |
| 9 | location_id | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |
| 10 | provider_id | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |
| 11 | care_site_id | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |
| 12 | person_source_value | anon_case_no | | Ensure `anon_case_no` uniquely identifies individuals, as it's not unique in the source. |
| 13 | gender_source_value | gender | MALE<br>FEMALE | |
| 14 | gender_source_concept_id | gender | 0 | May omit |
| 15 | race_source_value | race | Chinese<br>Other Races<br>Indian<br>Malay | |
| 16 | race_source_concept_id | race | 0 | May omit |
| 17 | ethnicity_source_value | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |
| 18 | ethnicity_source_concept_id | <i style="color:gray;">NULL</i> | <i style="color:gray;">NULL</i> | |