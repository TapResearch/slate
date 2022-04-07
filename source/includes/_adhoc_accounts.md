# Adhoc Accounts

## Create an Adhoc Account

Create an adhoc account also known as a buyer that can subsequently be provided in requests to the [/campaigns](#campaigns) endpoint using the parameter 'buyer_account_id'.

> Sample Request Payload

```json
{
    "buyer_name":"buyer",
    "buyer_identifier":"buyer1234"
}
```

> Sample Response

``` json
{
    "id": 1,
    "buyer_name": "buyer",
    "buyer_identifier": "buyer1234"
}
```
### HTTP Request

`POST https://www.tapresearch.com/api/v1/adhoc_accounts`

<aside class="info">
While the below parameters are optional at least one of the two are required.
</aside>

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
buyer_name | String | Name of the buyer.
buyer_identifier | String | Identifier of the buyer.

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
id | Integer | ID to be passed in as the 'buyer_account_id' when using the [/campaigns](#campaigns) endpoint.
buyer_name | String | Name of the buyer.
buyer_identifier | String | Identifier of the buyer.



