# Campaign Retargeting

## Add Respondents

> Sample Request Payloads

```json
{
  "retargeting_type": 1,
  "retargeting_ids": [
    {
      "id": "e2c479d73ff8a256317356a2be25aed4"
    }, {
      "id": "47427850ed299431ad173ec32868dbe9"
    }, {
      "id": "eeb784b657985398f24707e3f0969227"
    }, {
      "id": "69ca1702f0c1b9f508687e37b243e928"
    }, {
      "id": "1b240e62c891524bf62dab9dc18db028"
    }, {
      "id": "6385e12881c8ed49070411f309b43058"
    }
  ]
}
```

```json
{
  "retargeting_type": 0,
  "retargeting_ids": [
    {
      "id": "748F63F4-A2FA-4971-8154-11FE4D03C0C9",
      "replacement_id": "device_1"
    }, {
      "id": "DAFFA6A9-A37A-441E-9E65-73B79FC7B4B6",
      "replacement_id": "device_2"
    }, {
      "id": "82ACEFDA-06C1-4023-B897-F08ECBA330BB",
      "replacement_id": "device_3"
    }, {
      "id": "00000000-0000-0000-0000-000000000000",
      "replacement_id": "device_4"
    }, {
      "id": "8A7D2593-4835-4F04-BEBD-59FC2C3F3272",
      "replacement_id": "device_5"
    }, {
      "id": "C4FBAAB9-A853-498E-8843-6F6A4831C34B",
      "replacement_id": "device_6"
    }
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
  "length_of_interview": 20,
  "name": "PO1607074800517",
  "status": 2,
  "supplier_link": "https://api.samplecompany.com/survey/1?id=",
  "total_remaining": 100
}
```

Add respondent/device ID targeting to a campaign

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_retarget`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
retargeting_type | Integer | Specify the type of retargeting identifiers passed in. 0 (Transaction ID), 1 (Respondent ID), 2(Device ID)
retargeting_ids | Array | A list of objects that specify the following criteria.

### Retargeting Ids
Parameter | Type | Description
--------- | ---- | -----------
id | String | Required identifier used to target a respondent in a campaign.
replacement_id | String | Optional replacement value that is subsituted in the entry url. See campaign for details. 

### Response
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | This is the unique campaign identifier. You will need to use this parameter to get campaign details or update a specific campaign.
name | String | Name of the campaign
cpi | String | This is the amount you will payout per complete.
days_in_field | Integer | Number of days this campaign will be in the field. This value will be used to estimate feasibility for each associated campaign quota.
incidence | Integer | The percentage chance that a random respondent will qualify and complete the survey.
is_retarget | Boolean | Set to true for the first wave of a multi-wave recontact project. This will focus sampling on respondents who are more active, to improve recontact rates on subsequent waves.
status | Integer | This value will be returned as a 2(Active), 3(Complete), or 5(Paused).
length_of_interview | Integer | How many minutes will it take to complete the survey?
total_remaining | Integer | This is the number of completes left before the survey is complete. This value is the sum of num_respondents found inside associated campaign_quotas.
supplier_link | String | The entry URL when a respondent has qualified for the survey.

## Remove Respondents

> Sample Request Payload

```json
{
  "retargeting_type": 1,
  "retargeting_ids": [
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
When removing respondents from a retargeting campaign, you can specify one, several, or all of the respondents. If there are respondents left on the campaign, the campaign will still be in retarget mode.
</aside>

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
retargeting_type | Integer | Specify the type of retargeting identifiers passed in. 0 (Transaction ID), 1 (Respondent ID), 2(Device ID)
retargeting_ids | String Array | List of retargeting identifiers to remove.
