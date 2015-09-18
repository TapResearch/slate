# Qualifications

## List all qualifications

Get a list of supported targeting criteria.

> Sample Response

```json
[
  {
    "answer_type": 5,
    "name": "AGE",
    "question_id": 42,
    "question_text": "What is your age?"
  },
  {
    "answer_type": 0,
    "name": "GENDER",
    "question_id": 43,
    "question_text": "What is your gender?"
  },
  {
    "answer_type": 5,
    "name": "ZIP",
    "question_id": 45,
    "question_text": "What is your zip or postal code?"
  },
  {
    "answer_type": 0,
    "name": "HISPANIC",
    "question_id": 47,
    "question_text": "Are you of Hispanic, Latino, or Spanish origin?"
  },
  {
    "answer_type": 0,
    "name": "STATE",
    "question_id": 96,
    "question_text": "What is your state?"
  }
]
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

Get answer options to a specific qualification.

<aside class=info>
Qualifications with an answer_type = 5 will have an empty qualification_answer array.
</aside>

> Sample Response

```json
{
  "answer_type": 0,
  "name": "HISPANIC",
  "question_id": 47,
  "question_text": "Are you of Hispanic, Latino, or Spanish origin?",
  "qualification_answers": [
    {
      "option_text": "No , not of Hispanic, Latino, or Spanish origin",
      "pre_code": 1
    },
    {
      "option_text": "Yes, Mexican, Mexican American, Chicano",
      "pre_code": 2
    },
    {
      "option_text": "Yes, Cuban",
      "pre_code": 3
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Argentina ",
      "pre_code": 4
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Colombia ",
      "pre_code": 5
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Ecuador ",
      "pre_code": 6
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** El Salvadore ",
      "pre_code": 7
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Guatemala ",
      "pre_code": 8
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Nicaragua ",
      "pre_code": 9
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Panama ",
      "pre_code": 10
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Peru ",
      "pre_code": 11
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Spain ",
      "pre_code": 12
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Venezuela ",
      "pre_code": 13
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Other Country",
      "pre_code": 14
    },
    {
      "option_text": "Prefer not to answer",
      "pre_code": 15
    }
  ]
}
```

### HTTP Request

`GET https://www.tapresearch.com/api/v1/qualifications/:question_id`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
question_id | Integer | This value will be returned with each record through the /qualifications route.

### Response

### Qualification Answers
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The answer text that is shown to our respondents.
pre_code | Integer | This is value you will be passing into the campaign_qualifications pre_codes array to describe which respondents qualify for a survey.