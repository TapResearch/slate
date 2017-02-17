# Campaign Relationships

## Add Exclusion

> Sample Request Payloads

```json
{

}
```

> Sample Response

```json
{
 
}
```

Add respondent/device ID targeting to a campaign

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_retarget`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
respondent_ids / device_ids | Array | List of respondent or device IDs you want to target

### Response
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier. You will need to use this parameter to get campaign details or update a specific campaign.
name | String | Name of the campaign
cpi | String | This is the amount you will payout per complete.
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota.
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
is_retarget | Boolean | True if the campaign has respondent/device ID targeting.
status | Integer | This value will be returned as a 2(Active), 3(Complete), or 5(Paused).
length_of_interview | Integer | How many minutes will it take to complete the survey?
total_remaining | Integer | This is the number of completes left before the survey is complete. This value is the sum of num_respondents found inside associated campaign_quotas.
supplier_link | String | The redirect URL when a respondent has qualified for the survey.

## Remove Respondents

> Sample Request Payload

```json
{
  "respondent_ids": [
    "e2c479d73ff8a256317356a2be25aed4",
    "47427850ed299431ad173ec32868dbe9"
  ]
}
```

> Sample Response

```json
{
  "cpi": "2.75",
  "days_in_field": 5,
  "id": 365,
  "incidence": 10,
  "is_retarget": true,
  "length_of_interview": 20,
  "name": "PO1607074800517",
  "status": 2,
  "supplier_link": "https://api.samplecompany.com/survey/1?id=",
  "total_remaining": 100
}
```

Remove respondent/device ID targeting to a campaign

### HTTP Request

`DELETE https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_retarget`

<aside class=info>
When removing respondents from a retargeting campaign, you can specify one, several, or all of the respondents. If there are respondents left on the campaign,
The campaign will still be in retarget mode.
</aside>

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
respondent_ids / device_ids | Array | List of respondent or device ids you want to target

### Response
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier. You will need to use this parameter to get campaign details or update a specific campaign.
name | String | Name of the campaign
cpi | String | This is the amount you will payout per complete.
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota.
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
is_retarget | Boolean | True if the campaign has respondent/device ID targeting.
status | Integer | This value will be returned as a 2(Active), 3(Complete), or 5(Paused).
length_of_interview | Integer | How many minutes will it take to complete the survey?
total_remaining | Integer | This is the number of completes left before the survey is complete. This value is the sum of num_respondents found inside associated campaign_quotas.
supplier_link | String | The redirect URL when a respondent has qualified for the survey.
