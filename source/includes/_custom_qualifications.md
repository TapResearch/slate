# Custom Qualifications

## List custom qualifications


> Sample Response

```json
[
    {
        "name": "Food",
        "question_id": 45244321,
        "question_text": "What kind of food do you like?",
        "answer_type": 0,
        "en_translation": "What kind of food do you like?",
        "country_language_id": 1
    },
    {
        "name": "Television",
        "question_id": 45244399,
        "question_text": "What kind of TV do you watch?",
        "answer_type": 1,
        "en_translation": "What kind of TV do you watch?",
        "country_language_id": 1
    }
]
```


Get a list of your custom qualifications.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/custom_qualifications`

### Required Parameters

`NONE`

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Qualification name
question_id | Integer | This value will be used to fetch qualification details.
question_text | String | This is the question text that will be served to our respondents.
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.
en_translation | String | The english translation of the question.
country_language_id | integer | Id value specifying country language code of the qualification.

## Get a specific qualification

> Sample Response

```json
{
    "name": "Animal question",
    "question_id": 100067795,
    "question_text": "What kind of animal are you?",
    "answer_type": 0,
    "en_translation": "What kind of animal are you?",
    "country_language_id": 1,
    "qualification_answers": [
        {
            "option_text": "Bird",
            "pre_code": 1,
            "en_translation": "Bird"
        },
        {
            "option_text": "Cat",
            "pre_code": 2,
            "en_translation": "Cat"
        }
    ]
}
```

Get a specific qualification including answers.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/custom_qualifications/:question_id?country_language_id=1`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
question_id | Integer | The question id of the qualification to retrieve.
country_language_id | Integer | Country language targeting for the qualification to retrieve. 

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Qualification name
question_id | Integer | This value will be used to fetch qualification details.
question_text | String | This is the question text that will be served to our respondents.
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.
en_translation | String | The english translation of the question.
country_language_id | integer | Id value specifying country language code of the qualification.
qualification_answers | List | List of qualification answers for this qualification.

## Create a custom qualification

> Sample Request Payload

```json
{
  "answer_type":0,
  "name":"Animal question",
  "question_text":"What kind of animal are you?",
  "country_language_id":1
}
```

> Sample Response

```json
{
    "name": "Animal question",
    "question_id": 100067796,
    "question_text": "What kind of animal are you?",
    "answer_type": 0,
    "en_translation": "What kind of animal are you?"
}
```

Create a new custom qualification.

### HTTP Request

`POST https://www.tapresearch.com/api/v1/custom_qualifications`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
name | String | Qualification name
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.
question_text | String | This is the question text that will be served to our respondents.
country_language_id | integer | Id value specifying country language code of the qualification.


### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Qualification name
question_id | Integer | This value will be used to fetch qualification details.
question_text | String | This is the question text that will be served to our respondents.
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.
en_translation | String | The english translation of the question.

## Update a custom qualification

> Sample Request Payload

```json
{
  "question_id": 100067796,
  "answer_type":0,
  "name":"What kind of food do you like?",
  "question_text":"What kind of food do you like?",
  "country_language_id":1
}
```

> Sample Response

```json
{
    "name": "Animal question",
    "question_id": 100067796,
    "question_text": "What kind of food do you like?",
    "answer_type": 0,
    "en_translation": "What kind of food do you like?"
}
```

Update an existing custom qualification.

### HTTP Request

`PUT https://www.tapresearch.com/api/v1/custom_qualifications`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
question_id | Integer | The question id of the qualification to update.
name | String | Qualification name
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.
question_text | String | This is the question text that will be served to our respondents.
country_language_id | integer | Id value specifying country language code of the qualification.


### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Qualification name
question_id | Integer | This value will be used to fetch qualification details.
question_text | String | This is the question text that will be served to our respondents.
answer_type | Integer | This will determine how campaign_qualifications pre-codes are generated for quotas. See **Answer Types** section for more information.
en_translation | String | The english translation of the question.



## Create a qualification answer

> Sample Request Payload

```json
{
  "option_text":"Cat"
}
```

> Sample Response

```json
{
    "option_text": "Cat",
    "pre_code": 1,
    "en_translation": "Cat"
}
```

Create a qualification answer for a qualification.

### HTTP Request

`POST https://www.tapresearch.com/api/v1/custom_qualifications/:question_id/qualification_answers?country_language_id=1`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
question_id | Integer | The question id of the qualification to update.
country_language_id | integer | Id value specifying country language code of the qualification.
option_text | String | The answer to be shown to the respondent.


### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The text of the answer.
pre_code | Integer | The code that corresponds to this answer.
en_translation | String | The english translation of the answer.

## Update a qualification answer

> Sample Request Payload

```json
{
  "option_text":"Dog"
}
```

> Sample Response

```json
{
    "option_text": "Dog",
    "pre_code": 1,
    "en_translation": "Dog"
}
```

Update a qualification answer.

### HTTP Request

`PUT https://www.tapresearch.com/api/v1/custom_qualifications/:question_id/qualification_answers/:pre_code?country_language_id=1`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
pre_code | Integer | The code that corresponds to the qualification answer to update.
question_id | Integer | The question id of the qualification to update.
country_language_id | integer | Id value specifying country language code of the qualification.
option_text | String | The updated answer to be shown to the respondent.


### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The text of the answer.
pre_code | Integer | The code that corresponds to this answer.
en_translation | String | The english translation of the answer.

## Delete a qualification answer

> Sample Request Payload

```json
{
  "option_text":"Dog"
}
```

> Sample Response

```json
{
    "option_text": "Dog",
    "pre_code": 1,
    "en_translation": "Dog"
}
```

Delete a qualification answer.

### HTTP Request

`DELETE https://www.tapresearch.com/api/v1/custom_qualifications/:question_id/qualification_answers/:pre_code?country_language_id=1`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
pre_code | Integer | The code that corresponds to the qualification answer to delete.
question_id | Integer | The question id of the qualification that the answer belongs to.
country_language_id | integer | Id value specifying country language code of the qualification that the answer belongs to..


### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The text of the answer.
pre_code | Integer | The code that corresponds to the deleted answer.
en_translation | String | The english translation of the deleted answer.


## Create a campaign qualification

> Sample Request Payload

```json
{
  "question_id":102067795,
  "pre_code_values":"1,3"
}
```

> Sample Response

```json
{
    "id": 15958433450,
    "question_id": 100067795,
    "pre_codes": [
        1,
        3
    ]
}
```

Add a previously created custom qualification to a campaign

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_qualifications`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
campaign_id | Integer | Id of the campaign to add targeting to.
question_id | Integer| Id of the qualification to add.
pre_code_values | String | Comma separated string of pre_codes that qualify a respondent for this campaign qualification.



### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | Primary key identifier of the created campaign qualifcation.
question_id | Integer | Question id corresponding to the qualification used to create the campaign qualification.
pre_codes | List | List of pre-codes that corresponding to qualifying answers.

## Update a campaign qualification

> Sample Request Payload

```json
{
  "pre_code_values":"2"
}
```

> Sample Response

```json
{
    "id": 15958433450,
    "question_id": 100067795,
    "pre_codes": [
        2
    ]
}
```

Update a custom qualification.

### HTTP Request

`PUT https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_qualifications/:id`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
id | Integer | Id of the campaign qualification to update.
campaign_id | Integer | Id of the campaign whose qualification to update.
pre_code_values | String | Comma separated string of pre_codes that qualify a respondent for this campaign qualification.



### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | Primary key identifier of the updated campaign qualifcation.
question_id | Integer | Question id corresponding to the qualification being updated.
pre_codes | List | List of pre-codes that corresponding to qualifying answers.


## Delete a campaign qualification


> Sample Response

```json
{
    "id": 15958433450,
    "question_id": 100067795,
    "pre_codes": [
        2
    ]
}
```

Delete a custom qualification.

### HTTP Request

`DELETE https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_qualifications/:id`

### Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
id | Integer | Id of the campaign qualification to update.
campaign_id | Integer | Id of the campaign whose qualification to update.


### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | Primary key identifier of the deleted campaign qualifcation.
question_id | Integer | Question id corresponding to the qualification being deleted.
pre_codes | List | List of pre-codes that corresponding to qualifying answers.


















