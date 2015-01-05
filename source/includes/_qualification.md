# Qualifications

## List all qualifications

Get quota details along with associated campaign_qualifications.

> Sample Response

```json

```

### HTTP Request

`GET https://www.tapresearch.com/api/v1/qualifications`

<aside class="warning">
Qualifications that are sourced from **staging.tapresearch.com** may have different question_ids than the qualifications sourced from **www.tapresearch.com.**
</aside>

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Qualification name
question_id | Integer | This value will be used to fetch qualification details.
question_text | String | This is the question text that will be served to our respondents.
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.

## Get a specific qualification

Get quota details along with associated campaign_qualifications.

<aside class=info>
Qualifications with an answer_type = 5 will have an empty qualification_answer array.
</aside>

> Sample Response

```json

```

### HTTP Request

`GET https://www.tapresearch.com/api/v1/qualifications/:question_id`

### Required Parameters
--------- | ---- | -----------
question_id | Integer | This value will be returned with each record through the /qualifications route.

### Response

### Qualification Answers
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The answer text that is shown to our respondents.
pre_code | Integer | This is value you will be passing into the campaign_qualifications pre_codes array to describe which respondents qualify for a survey.