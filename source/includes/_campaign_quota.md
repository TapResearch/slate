# Campaign Quotas

## Create a campaign quota

Create a quota for a specific campaign.

> Sample Request Payload - 32 respondents who are between the ages of 18-24, 30-34 and male.

```json
{
  "num_respondents": 32,
  "campaign_qualifications": [
    {
      "question_id": 42,
      "pre_codes": [
        18,
        19,
        20,
        21,
        22,
        23,
        24,
        30,
        31,
        32,
        33,
        34
      ]
    },
    {
      "question_id": 43,
      "pre_codes": [
        1
      ]
    }
  ]
}
```

> Sample Response - Remember to record the id that is returned.

```json
{
  "id": 274771,
  "num_respondents": 32,
  "campaign_qualifications": [
    {
      "question_id": 42,
      "pre_codes": [
        18,
        19,
        20,
        21,
        22,
        23,
        24,
        30,
        31,
        32,
        33,
        34
      ]
    },
    {
      "question_id": 43,
      "pre_codes": [
        1
      ]
    }
  ]
}
```

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_quotas`

### Required Parameters

### Campaign Quota
Parameter | Type | Description
--------- | ---- | -----------
num_respondents | Integer | The number of completes required before the quota is closed.
campaign_qualifications | Array | A list of objects that describe the qualifying criteria for the quota.

### Campaign Qualification
Parameter | Type | Description
--------- | ---- | -----------
qualification_id | Integer | The qualification identifier you want to associate with the quota.
pre_codes | Integer Array | A list of accepted pre-codes or values. See **Answer Types** section.


## Update a campaign quota

Update a quota for a specific campaign.

> Sample Request Payload - 50 respondents who are hispanic and live in specific zip code areas.

```json
{
  "num_respondents": 50,
  "campaign_qualifications": [
    {
      "question_id": 45,
      "pre_codes": [
        "95120",
        "94089",
        "94115",
      ]
    },
    {
      "question_id": 47,
      "pre_codes": [
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        10,
        11,
        12,
        13,
        14
      ]
    }
  ]
}
```

### HTTP Request

`PUT https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_quotas/:id`

<aside class=warning>
Since we currently don't allow you to destroy a campaign_qualification, all campaign_qualifications will be replaced
unless the campaign_qualifications array is empty.
</aside>

### Optional Parameters

### Campaign Quota
Parameter | Type | Description
--------- | ---- | -----------
num_respondents | Integer | The number of completes required before the quota is closed.
campaign_qualifications | Array | A list of objects that describe the qualifying criteria for the quota.

### Campaign Qualification
Parameter | Type | Description
--------- | ---- | -----------
question_id | Integer | The qualification identifier you want to associate with the quota.
pre_codes | Integer Array | A list of accepted pre-codes or values. See **Answer Types** section.

## Get a specific campaign quota

Get quota details along with associated campaign_qualifications.

> Sample Response

```json
{
  "id": 274771,
  "num_respondents": 32,
  "campaign_qualifications": [
    {
      "question_id": 42,
      "pre_codes": [
        18,
        19,
        20,
        21,
        22,
        23,
        24,
        30,
        31,
        32,
        33,
        34
      ]
    },
    {
      "question_id": 43,
      "pre_codes": [
        1
      ]
    }
  ]
}
```

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_quotas/:id`

### Required Parameters
`NONE`