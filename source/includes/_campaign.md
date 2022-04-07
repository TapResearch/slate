# Campaigns

## List your campaigns

> Sample Response

```json
{
    "id": 11611886,
    "cpi": null,
    "length_of_interview": 10,
    "name": "Test Survey",
    "total_remaining": 0,
    "status": 5,
    "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
    "incidence": 50,
    "reentry_interval": null,
    "days_in_field": 3,
    "max_daily_completes": null,
    "is_retarget": false,
    "is_maid_targeted": false,
    "retarget_count": 0,
    "supported_devices": [
        0,
        2
    ],
    "country_language_id": 1,
    "custom_campaign_qualifications": [],
    "buyer_account_id": 1,
    "campaign_quotas": [],
    "campaign_relationships": [],
    "redirect_test_url": "https://www.tapresearch.com/api/v1/campaigns/11611886/redirect_test"
}
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
name | String | Name of the campaign.
cpi | String | All CPIs are USD. This is the amount you will be charged per complete.
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota.
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
status | Integer | This value will be returned as a 2(Active), 3(Complete), 4(Archived), 5(Paused), 6(Reconciled) or 7(System Paused).
length_of_interview | Integer | How many minutes will it take to complete the survey?
total_remaining | Integer | This is the number of completes left before the survey is complete. This value is the sum of num_respondents found inside associated campaign_quotas.
supplier_link | String | The entry URL when a respondent has qualified for the survey.
max_daily_completes | Integer | Total completes allowed per day.
reentry_interval | Integer | Time allowed for a respondent to re-enter this campaign. Never - null, Unlimited - 0, Days - number
country_language_id | Integer | Country language targeting for this campaign. 
retarget_count | Integer | Total number of recontact records associated with the campaign.
buyer_account_id | Integer | ID associated wth creation of a buyer via the [/adhoc_accounts](#adhoc-accounts) route.


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
  "buyer_account_id": 1,
  "supported_devices": [
    0,
    2
  ]
}
```

> Sample Response

``` json
{
    "id": 11598926,
    "cpi": null,
    "length_of_interview": 10,
    "name": "Test Survey",
    "total_remaining": 0,
    "status": 5,
    "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
    "incidence": 50,
    "reentry_interval": null,
    "days_in_field": 3,
    "max_daily_completes": null,
    "is_retarget": false,
    "is_maid_targeted": false,
    "retarget_count": 0,
    "supported_devices": [
        0,
        2
    ],
    "country_language_id": 1,
    "custom_campaign_qualifications": [],
    "buyer_account_id": 1
}
```

Create a campaign with campaign-only metadata. Quotas, exclusions, and qualifications will need to be added through other routes.

<aside class="info">
Campaigns will be in a paused state after creation. You will need to manually update the campaign to set it to active.
</aside>


### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
name | String | Name of the campaign
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
length_of_interview | Integer | How many minutes will it take to complete the survey?
country_language_id | Integer | Country language targeting for this campaign. 
supplier_link | String | The entry URL when a respondent has qualified for the survey. This URL can be configured to accept various respondent values. See below:
cpi | Decimal | All CPIs are USD. This is the amount you will be charged per complete.


### supplier_link formatting

<aside class=info>
More information on supplier_link formatting may be found under <a href="http://docs.tapresearch.com/#supplier-links">Supplier Links</a>.
</aside>

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
is_retarget | Boolean | Set to true for the first wave of a multi-wave recontact project. This will focus sampling on respondents who are more active, to improve recontact rates on subsequent waves.
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota. Default value is 5.
supported_devices | Integer Array | Pass in 0 (tablet), 1 (mobile), and/or 2 (desktop).
max_daily_completes | Integer | Number of completes that will be allowed per day for this campaign.
reentry_interval | Integer | Time allowed for a respondent to re-enter this campaign. Never - null, Unlimited - 0, Minutes - number.
buyer_account_id | Integer | ID associated wth creation of a buyer via the [/adhoc_accounts](#adhoc-accounts) route.

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
    "id": 11611886,
    "cpi": null,
    "length_of_interview": 10,
    "total_remaining": 0,
    "status": 5,
    "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
    "name": "New Survey Name",
    "incidence": 50,
    "days_in_field": 3,
    "is_retarget": false,
    "max_daily_completes": null,
    "reentry_interval": null,
    "country_language_id": 1,
    "is_maid_targeted": false,
    "supported_devices": [
        0,
        2
    ],
    "country_language_id": 1,
    "custom_campaign_qualifications": [],
    "buyer_account_id": 1
    "redirect_test_url": "http://www.tapresearch.com/api/v1/campaigns/11611886/redirect_test",
    "retarget_count": 0
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
    "id": 11611886,
    "cpi": null,
    "length_of_interview": 10,
    "name": "New Survey Name",
    "total_remaining": 500,
    "status": 5,
    "supplier_link": "https://api.samplecompany.com/surveys/23423?id=",
    "incidence": 50,
    "reentry_interval": null,
    "days_in_field": 3,
    "max_daily_completes": null,
    "is_retarget": false,
    "is_maid_targeted": false,
    "retarget_count": 0,
    "supported_devices": [
        0,
        2
    ],
    "country_language_id": 1,
    "custom_campaign_qualifications": [],
    "buyer_account_id": 1
    "campaign_quotas": [
        {
            "id": 54661616,
            "num_respondents": 500,
            "is_global": false,
            "name": "LocationQuota",
            "is_click_balanced": true,
            "campaign_qualifications": [
                {
                    "question_id": 96,
                    "pre_codes": [
                        37
                    ]
                },
                {
                    "question_id": 97,
                    "pre_codes": [
                        650
                    ]
                }
            ]
        }
    ],
    "campaign_relationships": [
        {
            "id": 56369643627,
            "campaign_id": 11611886,
            "related_campaign_id": 11598926
        }
    ],
    "redirect_test_url": "https://www.tapresearch.com/api/v1/campaigns/11611886/redirect_test"
}
```

Retrieve campaign metadata along with associated quotas, exclusions, and qualifications.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns/:id`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier.

## Redirect URL

> Sample Response

```json
{
    "redirect_test_url": "https://www.tapresearch.com/api/v1/campaigns/:id/redirect_test"
}
```

Retrieve the associated redirect_test_url for a specific campaign.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns/:id/redirect_test`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier.

## Reject completes for a campaign

> Sample Request

```json
{
   "transaction_ids": [
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
transaction_ids | Array of strings | Transaction ids that were attached to the id parameter when we sent the respondent into your survey.

<aside class="info">
The target number of completes for respective quotas will be auto-incremented based on the number of rejected completes.
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

{
  "campaign_quotas": [
      {
          "message": "We can't estimate feasibility for question ids: ( 723 )",
          "id": 959323
      }
  ],
  "estimated_completes": 0,
  "over_num_days": 5,
  "id": 153547
}

```

Get the total estimated number of completes based on your campaign quotas.

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns/:campaign_id/feasibility`

### Required Parameters
`NONE`

<aside class=warning>
Feasibility is unavailable for quotas created with certain question ids. In those cases, feasibility will return an appropriate message.
</aside>

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
cpi | Decimal | All CPIs are USD. This is the amount you will be charged per complete.
country_language_id | Integer | Country language targeting for this campaign.  


### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota. Default value is 5.

## Reconciliation

> Sample Request

```json
{
   "purchase_order":"tt489m900",
   "accepted_ids": [
    "30c60dbff51a9b8155609534f27de291",
    "22d2dccca27f438876613c46e6d50db3",
    "904895ae97e7412530746b3b709ee9e0",
    "751b36f52152bc765803e65aefe4ace7",
    "b41f02bed5a07fd69b1675f938bdcd05"
  ]
}
```

Reconcile a campaign using accepted survey complete ids.

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:id/reconcile`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier.
accepted_ids | Array of strings | Transaction ids of survey completes that were accepted.

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
purchase_order | String | Purchase order associated with the campaign.
