# Lookups 

## List all country languages 

### HTTP Request

`GET https://www.tapresearch.com/api/v1/country_languages`


> Sample Response

```json
[
  {
    "id": 1,
    "abbr": "en-US"
  },
  {
    "id": 2,
    "abbr": "en-CA"
  },
  {
    "id": 5,
    "abbr": "en-GB"
  },
  {
    "id": 9,
    "abbr": "en-AU"
  }
]
```

## List all qualifications

Get a list of supported targeting criteria.

> Sample Response

```json
[
  {
    "answer_type": 5,
    "name": "AGE",
    "question_id": 42,
    "question_text": "What is your age?",
    "en_translation": "What is your age?"
  },
  {
    "answer_type": 0,
    "name": "GENDER",
    "question_id": 43,
    "question_text": "What is your gender?",
    "en_translation": "What is your gender?"
  },
  {
    "answer_type": 5,
    "name": "ZIP",
    "question_id": 45,
    "question_text": "What is your zip or postal code?",
    "en_translation": "What is your your zip or postal code?"
  },
  {
    "answer_type": 0,
    "name": "HISPANIC",
    "question_id": 47,
    "question_text": "Are you of Hispanic, Latino, or Spanish origin?",
    "en_translation": "Are you of Hispanic, Latino, or Spanish origin?"
  },
  {
    "answer_type": 0,
    "name": "STATE",
    "question_id": 96,
    "question_text": "What is your state?",
    "en_translation": "What is your state?"
  }
]
```

### HTTP Request

`GET https://www.tapresearch.com/api/v1/qualifications?country_language_id=1`

<aside class="warning">
Qualifications that are sourced from **https://staging.tapresearch.com** may have different question_ids than the qualifications sourced from **www.tapresearch.com.**
</aside>

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
country_language_id | integer | Id value used to specify which set of qualifications to get by country language code.


### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Qualification name
question_id | Integer | This value will be used to fetch qualification details.
question_text | String | This is the question text that will be served to our respondents.
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.
en_translation | String | The english translation of the question.

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
  "en_translation": "Are you of Hispanic, Latino, or Spanish origin?",
  "qualification_answers": [
    {
      "option_text": "No , not of Hispanic, Latino, or Spanish origin",
      "pre_code": 1,
      "en_translation": "No , not of Hispanic, Latino, or Spanish origin"
    },
    {
      "option_text": "Yes, Mexican, Mexican American, Chicano",
      "pre_code": 2,
      "en_translation": "Yes, Mexican, Mexican American, Chicano"
    },
    {
      "option_text": "Yes, Cuban",
      "pre_code": 3,
      "en_translation": "Yes, Cuban"
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Argentina ",
      "pre_code": 4,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Argentina "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Colombia ",
      "pre_code": 5,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Colombia "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Ecuador ",
      "pre_code": 6,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Ecuador "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** El Salvadore ",
      "pre_code": 7,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** El Salvadore "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Guatemala ",
      "pre_code": 8,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Guatemala "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Nicaragua ",
      "pre_code": 9,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Nicaragua "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Panama ",
      "pre_code": 10,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Panama "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Peru ",
      "pre_code": 11,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Peru "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Spain ",
      "pre_code": 12,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Spain "
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Venezuela ",
      "pre_code": 13,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Venezuela ",
    },
    {
      "option_text": "Yes, another Hispanic, Latino, or Spanish origin *** Other Country",
      "pre_code": 14,
      "en_translation": "Yes, another Hispanic, Latino, or Spanish origin *** Other Country",
    },
    {
      "option_text": "Prefer not to answer",
      "pre_code": 15,
      "en_translation": "Prefer not to answer"
    }
  ]
}
```

### HTTP Request

`GET https://www.tapresearch.com/api/v1/qualifications/:question_id?country_language_id=1`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
question_id | Integer | This value will be returned with each record through the /qualifications route.
country_language_id | Integer | Id value used to specify which qualification to get by country language code. 

### Response

### Qualification Answers
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The answer text that is shown to our respondents.
pre_code | Integer | This is value you will be passing into the campaign_qualifications pre_codes array to describe which respondents qualify for a survey.
en_translation | String | The english translation of the answer.