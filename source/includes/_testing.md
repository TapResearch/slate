# Testing your integration

> Create a test campaign

```shell
curl -X POST https://www.tapresearch.com/api/v1/campaigns \
-H "Authorization: Basic BASE64_ENCODED_EMAIL_ADDRESS_YOU_PROVIDED:API_TOKEN" \
-H "Content-Type: application/json" \
-d '{
  "name": "TEST - my integration",
  "length_of_interview": 10,
  "incidence": 50,
  "country_language_id": 1,
  "supplier_link": "https://api.samplecompany.com/surveys/23423?id="
}'
```

> Sample Response - the new campaign is paused (status 5)

```json
{
    "id": 11598926,
    "name": "TEST - my integration",
    "status": 5,
    "length_of_interview": 10,
    "incidence": 50,
    "country_language_id": 1,
    "supplier_link": "https://api.samplecompany.com/surveys/23423?id="
}
```

> Retire the test campaign when you are done

```shell
curl -X PUT https://www.tapresearch.com/api/v1/campaigns/11598926 \
-H "Authorization: Basic BASE64_ENCODED_EMAIL_ADDRESS_YOU_PROVIDED:API_TOKEN" \
-H "Content-Type: application/json" \
-d '{"status": 3}'
```

There is no separate test server. Test your integration in production, at `https://www.tapresearch.com`, with your existing API token,
using HTTP basic authentication with your email address and API token as described in [Authentication](#authentication).

Production is live: an active campaign is shown to real respondents, and you will be charged for each complete. Follow the steps below
so that a test campaign never goes live.

1. Name every test campaign with a `TEST` prefix (for example `TEST - my integration`), so it can be told apart from your real campaigns.
2. Create the campaign with `POST https://www.tapresearch.com/api/v1/campaigns`. A campaign created through the API always starts paused
(status 5), even if you pass a different status. Check for `"status": 5` in the response.
3. Exercise the routes your integration uses against your test campaign. Keep it paused the whole time.
4. When you are done, set the campaign's status to 3 (Complete). Campaigns can not be deleted through the API; quotas can.
Email **api_support@tapresearch.com** about test campaigns you no longer need.

Route | What to test
----- | ------------
`POST https://www.tapresearch.com/api/v1/campaigns/realtime_feasibility` | [Feasibility](#realtime-feasibility) for your settings and quotas, without creating a campaign.
`GET https://www.tapresearch.com/api/v1/campaigns` | [List your campaigns](#list-your-campaigns).
`POST https://www.tapresearch.com/api/v1/campaigns` | [Create a campaign](#create-a-campaign). It starts paused (status 5).
`GET https://www.tapresearch.com/api/v1/campaigns/:id` | [Get a specific campaign](#get-a-specific-campaign).
`PUT https://www.tapresearch.com/api/v1/campaigns/:campaign_id` | [Update a campaign](#update-a-campaign). Never set status 2 on a test campaign.
`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_quotas` | [Create a campaign quota](#create-a-campaign-quota).
`GET`, `PUT` or `DELETE https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_quotas/:id` | [Get, update or delete a campaign quota](#campaign-quotas).
`GET https://www.tapresearch.com/api/v1/campaigns/:id/redirect_test` | [Redirect URL](#redirect-url): try the respondent redirect. It works while the campaign is paused and records a test entry on the campaign.

<aside class="warning">
Never set the status of a test campaign to 2 (Active). As a safety net, a campaign can not be set to active until it has at least one quota
with num_respondents greater than 0, but a test campaign that has quotas can still go live.
</aside>
