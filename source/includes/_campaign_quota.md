# Campaign Quotas

## Create a campaign quota

Create a quota for a specific campaign.

> Sample Request Payload

```json
```

> Sample Response

```json

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

> Sample Request Payload

```json
```

> Sample Response

```json
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

```

### HTTP Request

`GET https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_quotas/:id`

### Required Parameters
`NONE`