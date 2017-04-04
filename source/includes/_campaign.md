# Campaigns

## List your campaigns

> Sample Response

```json
[
  {
      "cpi": "3.15",
      "days_in_field": 3,
      "id": 14706,
      "incidence": 10,
      "length_of_interview": 20,
      "name": "Test Survey 1",
      "status": 2,
      "supplier_link": "https://api.samplecompany.com/survey/1?id=",
      "total_remaining": 6,
      "max_daily_completes": null,
      "renentry_interval": null,
      "country_language_id": 1
  },
  {
      "cpi": "3.69",
      "days_in_field": 10,
      "id": 14707,
      "incidence": 20,
      "length_of_interview": 15,
      "name": "Test Survey 2",
      "status": 2,
      "supplier_link": "https://api.samplecompany.com/survey/2?id=",
      "total_remaining": 37,
      "max_daily_completes": null,
      "renentry_interval": null
      "country_language_id": 1
  }
]
```

Get a list of campaigns that are accessible by the authenticated user.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns`

### Required Parameters
`NONE`


### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
country_language_id | Integer | Optional id value used to specify which set of campaigns to get by country language code.

### Response

Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier. You will need to use this parameter to get campaign details or update a specific campaign.
name | String | Name of the campaign
cpi | String | This is the amount you will payout per complete.
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota.
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
status | Integer | This value will be returned as a 2(Active), 3(Complete), or 5(Paused).
length_of_interview | Integer | How many minutes will it take to complete the survey?
total_remaining | Integer | This is the number of completes left before the survey is complete. This value is the sum of num_respondents found inside associated campaign_quotas.
supplier_link | String | The entry URL when a respondent has qualified for the survey.
max_daily_completes | Integer | Total completes allowed per day.
reentry_interval | Integer | Time allowed for a respondent to re-enter this campaign. Never - null, Unlimited - 0, Days - number
country_language_id | Integer | Which country_language this campaign belongs to.

## Create a campaign

> Sample Request Payload

```json
{
  "name": "Test Survey",
  "days_in_field": 3,
  "length_of_interview": 10,
  "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
  "incidence": 50,
  "country_language_id": 1,
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
  "days_in_field": 3,
  "id": 14724,
  "incidence": 50,
  "length_of_interview": 10,
  "name": "Test Survey",
  "status": 5,
  "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
  "total_remaining": 0,
  "max_daily_completes": null,
  "country_language_id": 1,
  "supported_devices": [
      0,
      2
  ]
}
```

Create a campaign with campaign-only metadata. Quotas, exclusions, and qualifications will need to be added through other routes.

<aside class="info">
Campaigns will be a paused state after creation. You will need to manually update the campaign to set it to active.
</aside>


### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Name of the campaign
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
length_of_interview | Integer | How many minutes will it take to complete the survey?
country_language_id | Integer | Id value used to specify which country_language code this campaign should belong to.
supplier_link | String | The entry URL when a respondent has qualified for the survey. This URL can be configured to accept various respondent values. See below:


### supplier_link formatting

**Transaction ID (required)**

Specify where you want this ID to appear using {ID}:
https://api.samplecompany.com/surveys/23423?id={ID}

OR

It will be automatically appended to the end of the URL:
https://api.samplecompany.com/surveys/23423?&id=

This value must be passed back in the [status callback URLs](#callbacks).

**Respondent ID**

https://api.samplecompany.com/surveys/23423?respondent_id={RESPONDENT_ID}&id={ID}

This is the unique alphanumeric ID for this respondent.

**Retarget Identifier**

https://api.samplecompany.com/surveys/23423?retarget_id={RETARGET_IDENTIFIER}&id={ID}

{RETARGET_IDENTIFIER} will be replaced with the retargeting_id as provided in [Campaign Retargeting](#campaign-retargeting).

If a replacement_id is specified in [Campaign Retargeting](#campaign-retargeting), that value will be used instead.

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota. Default value is 5.
supported_devices | Integer Array | Pass in 0 (tablet), 1 (mobile), and/or 2 (desktop).
max_daily_completes | Integer | Number of completes that will be allowed per day for this campaign.
reentry_interval | Integer | Time allowed for a respondent to re-enter this campaign. Never - null, Unlimited - 0, Minutes - number

## Update a campaign

> Sample Request Payload - Change name and length of interview for a campaign.

```json
{
  "name": "New Survey Name",
  "length_of_interview": 10
}
```

> Sample Request Payload - Set a campaign to active, allow mobile respondents, and set a maximum complete amount for 250.

```json
{
  "status": 2,
  "max_daily_completes": 250,
  "supported_devices": [
    1
  ]
}
```

> Sample Request Payload - Set a reentry interval for 5 days for a respondent. 

```json
{
  "reentry_internval": 7200
}
```

> Sample Response

```json
{
  "name": "Test Survey",
  "days_in_field": 8
  "cpi": "2.50",
  "length_of_interview": 10,
  "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
  "incidence": 50,
  "max_daily_completes": 250,
  "reentry_interval": 7200,
  "supported_devices": [
    0,
    2
  ]
}
```

Update a campaign that belongs to the authenticated user.

<aside class="info">
You can not update the country_language code after creating a campaign. Please create a new one if you need to change your campaign's country_language.
</aside>

### HTTP Request

`PUT https://www.tapresearch.com/api/v1/campaigns/:campaign_id`

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
status | Integer | Only 2 (Active), 3 (Complete), 5 (Paused) will be accepted.

See [Create Campaign](#create-a-campaign) for additional parameters

## Get a specific campaign

> Sample Response

```json
{
  "cpi": "3.15",
  "days_in_field": 12,
  "id": 14706,
  "incidence": 20,
  "length_of_interview": 20,
  "name": "Test Survey #123",
  "status": 2,
  "supplier_link": "https://api.samplecompany.com/surveys/234230?id=",
  "total_remaining": 6,
  "max_daily_completes": 250,
  "country_language_id" : 1,
  "supported_devices": [
    0,
    1,
    2
  ],
  "campaign_relationships" : [
    "campaign_id": 14706,
    "related_campaign_id": 14709,
    "id": 538
  ]
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

Retrieve campaign metadata along with associated quotas, exclusions, and qualifications.

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

## Feasibility

> Sample Response

```json
{
  "campaign_quotas": [
    {
        "id": 446003,
        "estimated_completes": 32
    }
  ],
  "estimated_completes": 32,
  "over_num_days": 5,
  "id": 30309
}
```

Get the total estimated number of completes based on your campaign quotas.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns/:campaign_id/feasibility`

### Required Parameters
`NONE`

## Realtime Feasibility

> Sample Request

```json
{
  "incidence":20,
  "length_of_interview" : 10,
  "days_in_field" : 5,
  "campaign_quotas" : [
    {
      "num_respondents": 10,
      "campaign_qualifications": [
        {
          "question_id": 97,
          "pre_codes": [
            662,
            525
          ]
        }
      ]
    },
    {
      "num_respondents": 20,
      "campaign_qualifications": [
        {
          "question_id": 42,
          "pre_codes": [
              18,
              19,
              20,
              21,
              22
          ]
        }
      ]
    }
  ]
}
```

> Sample Response

```json
{
  "campaign_quotas": [
    {
      "estimated_completes": 3
    },
    {
      "estimated_completes": 20
    }
  ],
  "estimated_completes": 23,
  "over_num_days": 5
}
```

Get the total estimated number of completes without having to create a campaign.

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/realtime_feasibility`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
length_of_interview | Integer | How many minutes will it take to complete the survey?
campaign_quotas | Array | See "create a campaign quota" subsection.

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota. Default value is 5.
