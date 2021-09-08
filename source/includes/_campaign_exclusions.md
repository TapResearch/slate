# Campaign Exclusions

## Create a campaign exclusion

> Sample Request Payload - A sampling of valid and invalid player_ids and transaction_ids.

```json
{
  "player_ids": [
    "d35d05c7577ba0c11af91d75b522db18",
    "a356e6e1b1ee8b1ea21ebba41f6b18d6",
    "a356e6e1b1ee8b1ea21ebba41f6b18d6",
    "b57024d5a31f3d24934a7e8f60741d2b",
    "3b73ae4ddacc3b164a9efb56b3f5ad49"
  ],
  "transaction_ids": [
    "111111",
    "212334545",
    "00001e90514db20ed1003395d08d4285",
    "000023fc28bc5c1761a7d9075809f29f",
    "00002a30869515a24565d7647c052165",
    "00003ccc46583c2464ee326bf80aa528"
  ]
}
```

> Sample Response 

``` json
{
    "player_ids_excluded": [
        "3b73ae4ddacc3b164a9efb56b3f5ad49",
        "a356e6e1b1ee8b1ea21ebba41f6b18d6",
        "b57024d5a31f3d24934a7e8f60741d2b"
    ],
    "player_ids_not_found": [
        "d35d05c7577ba0c11af91d75b522db18"
    ],
    "transaction_ids_excluded": [
        "00002a30869515a24565d7647c052165",
        "00003ccc46583c2464ee326bf80aa528"
    ],
    "transaction_ids_not_found": [
        "111111",
        "212334545",
        "00001e90514db20ed1003395d08d4285",
        "000023fc28bc5c1761a7d9075809f29f"
    ]
}
```

Create player and/or transaction exclusions for a specific campaign. 

### HTTP Request

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_exclusions`

<aside class="info">
While optional at least one of either player_ids or transaction_ids must be used in your request.
</aside>

### Optional Parameters
Parameter | Type | Description 
--------- | ---- | ----------- 
player_ids | Array of strings | Specify the player_ids to be excluded for the applicable campaign.
transaction_ids | Array of strings | Specify the transaction_ids to be excluded for the applicable campaign.

### Response 
Parameter | Type | Description
--------- | ---- | -----------
player_ids_excluded | Array of strings | A list of player_ids that were found and excluded.
player_ids_not_found | Array of strings | A list of player_ids that were not found.
transaction_ids_excluded | Array of strings | A list of transaction_ids that were found and excluded.
player_ids_excluded | Array of strings | A list of transaction_ids that were not found and excluded.




