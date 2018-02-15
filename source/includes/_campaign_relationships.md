# Campaign Relationships

## Add Exclusion

> Sample Request Payloads

```json
{
  "campaign_id": 1234,
  "related_campaign_id": 5678
}
```

> Sample Response

```json
{
  "campaign_id": 1234,
  "related_campaign_id": 5678,
  "id": 222 
}
```

Excludes campaigns from being shown together for a user.

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaign_relationships/`

### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
campaign_id | Integer | Unique campaign id to be excluded from the related campaign.
related_campaign_id | Integer | Unqiue campaign id to be excluded from the related campaign. 

### Response
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | Unique campaign relationship id. Used to identify the relationship between campaigns. 
campaign_id | Integer | Unique campaign id to be excluded from the related campaign.
related_campaign_id | Integer | Unqiue campaign id to be excluded from the related campaign. 


## Remove Exclusion

Remove campaign exclusion.

### HTTP Request

`DELETE https://www.tapresearch.com/api/v1/campaign_relationships/:id`


### Required Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | Unique campaign relationship id. Used to identify the relationship between campaigns. 
