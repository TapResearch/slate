# Campaign Export

## Create a campaign export

> Sample Request Payload - Request body in which you wish to filter on multiple transaction_ids and multiple player_ids.

```json
{
  "player_ids": [
    "1245",
    "64354556"
  ],
  "transaction_ids": [
    "111111",
    "212334545"
  ]
}
```

Create an export of campaign demographic data in a CSV format. More information on the formatting of the CSV returned in the response may be found [here](http://help.tapresearch.com/en/articles/5554409-export-a-csv-of-campaign-demographic-information-via-the-api).

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/export_demographics`

<aside class="info">
The optional parameters below may be passed as arrays in the body of the request or as single ids in the URL for filtering purposes.
</aside>

### Required Parameters
`NONE`

### Optional Parameters
Parameter | Type | Description 
--------- | ---- | ----------- 
transaction_ids | String or Array of strings | Any transaction_ids you wish to filter the CSV export on.
player_ids | String or Array of strings | Any player_ids you wish to filter the CSV export on.







