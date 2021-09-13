# Custom Screeners

A custom screener is targeting criteria that you can define yourself. These qualifications behave similarly to the qualifications available in the [/qualifications](http://docs.tapresearch.com/#list-all-qualifications) endpoint, however they are not re-usable. Each time a custom screener is used, it must be re-created.

## Create a custom qualification

Create a custom qualification question.

> Sample Request 

```json
{
    "name": "My qualification",
    "question_text": "What do you want to do with your life?",
    "answer_type": 0,
    "country_language_id": 1
}

```

> Sample Response 

```json
{
    "name": "My qualification",
    "question_id": 100112709,
    "question_text": "What do you want to do with your life?",
    "answer_type": 0,
    "en_translation": "What do you want to do with your life?",
    "country_language_id": 1
}
```

### HTTP Request

`POST https://www.tapresearch.com/api/v1/custom_qualifications`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
question_text | String | This is the question text that will be served to our respondents.
answer_type | Integer | The answer format to be used for the qualification. Mapping information may be found [here](https://help.tapresearch.com/en/articles/5569336-answer-type-mappings-for-custom_qualifications-endpoint).
country_language_id | Integer | Country language targeting for the qualification.

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Name of the custom qualification.
customer_id | Integer | The unique identifier associated with your account. See **Callbacks** section for more information. This is set automatically and unable to be edited.

### Response
Parameter | Type | Description
--------- | ---- | -----------
name | String | Name of the custom qualification.
question_id | Integer | This value will be used to fetch qualification details.
question_text | String | This ans the question text that will be served to our respondents.
answer_type | Integer | The answer format to be used for the qualification. Mapping information may be found [here](https://help.tapresearch.com/en/articles/5569336-answer-type-mappings-for-custom_qualifications-endpoint).git
country_language_id | Integer | Country language targeting for the qualification.
en_translation | String | The English translation of the question.

## Create a custom qualification answer

Create a custom qualification answer to correspond with your custom qualifications.

> Sample Request Payload - Update custom qualification name

```json
{
    "option_text": "Corporate Chef"
}
```

> Sample Response 

```json
{
    "option_text": "Corporate Chef",
    "pre_code": 4,
    "en_translation": "Corporate Chef",
    "country_language_id": 1
}
```

### HTTP Request

`POST https://www.tapresearch.com/api/v1/custom_qualifications/:question_id/custom_qualification_answers`


### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The answer text that is shown to our respondents.

### Response
Parameter | Type | Description
--------- | ---- | -----------
option_text | String | The answer text that is shown to our respondents.
pre_code | Integer | This is the value(s) you will be passing into the campaign_qualifications pre_codes array to describe which respondents qualify for a survey.
en_translation | String | The English translation of the question.
country_language_id | Integer | Country language targeting for the qualification.

## Create a campaign qualification

Create a campaign qualification which will allow you to associate your custom qualifications and answers to a specific campaign.

> Sample Request Payload - 

```json
{
    "question_id": 100112713,
    "pre_code_values": "1"
}
```

> Sample Response 

```json
{
    "id": 50394692475,
    "question_id": 100112713,
    "pre_codes": [
        1
    ]
}
```

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_qualifications`


### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This the unique identifier of the campaign qualification.You will need to use this parameter to update a specific campaign qualification.
question_id | Integer | This value will be used to fetch qualification details.
pre_code_values | String | The pre_code value received in the response of returned when creating a custom qualification answer. See **Create a custom qualification answer** for more information.


### Response
Parameter | Type | Description
--------- | ---- | -----------
question_id | Integer | This value will be used to fetch qualification details.
pre_codes | Array of Integers | Values to be passed in the pre_codes array to describe which respondents qualify for a survey.

## Update a campaign qualification

Update the pre_code_values for a specified campaign qualification.

> Sample Request

```json
{
    "pre_code_values": "2"
}

```

> Sample Response

```json
{
    "id": 50395232189,
    "question_id": 100112748,
    "pre_codes": [
        2
    ]
}

```

### HTTP Request

`PUT https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_qualifications/:id`

###  Optional Parameters

Parameter | Type | Description
--------- | ---- | -----------
pre_code_values | String | The pre_code value received in the response of returned when creating a custom qualification answer. See **Create a custom qualification answer** for more information.


## Delete a campaign qualification

Remove a campaign qualification

### HTTP Request

`DELETE https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_qualifications/:id`

###  Required Parameters

Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This the unique identifier of the campaign qualification.