# Campaigns

## List your campaigns

> Sample Response

```json
[
  {
      "cpi": "3.15",
      "id": 14706,
      "incidence": 10,
      "length_of_interview": 20,
      "name": "Test Survey 1",
      "status": 2,
      "supplier_link": "https://api.samplecompany.com/survey/1?id=",
      "total_remaining": 6
  },
  {
      "cpi": "3.69",
      "id": 14707,
      "incidence": 20,
      "length_of_interview": 15,
      "name": "Test Survey 2",
      "status": 2,
      "supplier_link": "https://api.samplecompany.com/survey/2?id=",
      "total_remaining": 37
  }
]
```

Get a list of campaigns that are accessible by the authenticated user.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns`

### Required Parameters
`NONE`

### Response

Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier. You will need to use this parameter to get campaign details or update a specific campaign.
name | String | Name of the campaign
cpi | String | This is the amount you will payout per complete.
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
status | Integer | This value will be returned as a 2(Active), 3(Complete), or 5(Paused).
length_of_interview | Integer | How many minutes will it take to complete the survey?
total_remaining | Integer | This is the number of completes left before the survey is complete. This value is the sum of num_respondents found inside associated campaign_quotas.
supplier_link | String | The redirect URL when a respondent has qualified for the survey.

## Create a campaign

> Sample Request Payload

```json
{
  "name": "Test Survey",
  "cpi": "2.50",
  "length_of_interview": 10,
  "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
  "incidence": 50,
  "supported_devices": [
    0,
    2
  ]
}
```

> Sample Response

``` json
{
  "cpi": "2.5",
  "id": 14724,
  "incidence": 50,
  "length_of_interview": 10,
  "name": "Test Survey",
  "status": 5,
  "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
  "total_remaining": 0,
  "supported_devices": [
      0,
      2
  ]
}
```

Create a campaign with campaign-only metadata. Quotas and qualifications will need to be added through other routes.

<aside class="info">
Campaigns will be a paused state after creation. You will need to manually update the campaign to set it to active.
</aside>

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Name of the campaign
cpi | String | This is the amount you will payout per complete.
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
length_of_interview | Integer | How many minutes will it take to complete the survey?
supplier_link | String | The redirect URL when a respondent has qualified for the survey. You will need to append 'id=' to the end of the redirect url so we can pass-through a sesssion identifier.

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
supported_devices | Integer Array | Pass in 0 (mobile), 1 (tablet), and/or 2 (desktop).

## Update a campaign

> Sample Request Payload

```json
{
  "name": "New Survey Name",
  "length_of_interview": 10
}
```

> Set a campaign to active and allow for only mobile respondents.

```json
{
  "status": 2,
  "supported_devices": [
    0
  ]
}
```

> Sample Response

```json
{
  "name": "Test Survey",
  "cpi": "2.50",
  "length_of_interview": 10,
  "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
  "incidence": 50,
  "supported_devices": [
    0,
    2
  ]
}
```

Update a campaign that belongs to the authenticated user.

### HTTP Request

`PUT https://www.tapresearch.com/api/v1/campaigns/:campaign_id`

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Name of the campaign
cpi | String | This is the amount you will payout per complete.
status | Integer | Only 2 (Active), 3 (Complete), 5 (Paused) will be accepted.
supplier_link | String | The redirect URL when a respondent has qualified for the survey. You will need to append 'id=' to the end of the redirect url so we can pass-through a sesssion identifier.
supported_devices | Integer Array | Pass in 0 (mobile), 1 (tablet), and/or 2 (desktop).

## Get a specific campaign

> Sample Response

```json
{
    "cpi": "3.15",
    "id": 14706,
    "incidence": 20,
    "length_of_interview": 20,
    "name": "Cint-83372",
    "status": 2,
    "supplier_link": "https://api.samplecompany.com/surveys/234230?id=",
    "total_remaining": 6,
    "supported_devices": [
        0,
        1,
        2
    ],
    "campaign_quotas": [
        {
            "id": 273057,
            "name": "Test Campaign Quota",
            "num_respondents": 6,
            "campaign_qualifications": [
                {
                    "question_id": 42,
                    "pre_codes": [
                        30,
                        31,
                        32,
                        33,
                        34,
                        35,
                        36,
                        37,
                        38,
                        39,
                        40
                    ]
                },
                {
                    "question_id": 43,
                    "pre_codes": [
                        1,
                        2
                    ]
                }
            ]
        }
    ]
}
```

Retrieve campaign metadata along with associated quotas and qualifications.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns/:id`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier.

## Reject completes for a campaign

> Sample Request

```json
{
   "respondent_ids": [
    "30c60dbff51a9b8155609534f27de291",
    "22d2dccca27f438876613c46e6d50db3",
    "904895ae97e7412530746b3b709ee9e0",
    "751b36f52152bc765803e65aefe4ace7",
    "b41f02bed5a07fd69b1675f938bdcd05"
  ]
}
```

Reject completes that did not meet your quality standards.

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:id/reject_completes`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier.
respondent_ids | Array of strings | Respondent ids that were attached to the id parameter when we sent the respondent into your survey.

<aside class="warning">
Respondents can qualify for multiple quotas. Hence, you will need to manually update num_respondents for quotas after rejecting completes.
</aside>