# Testing your integration

You build and test your integration in production, at `https://www.tapresearch.com`,
with the same API token you will use when you go live. Authenticate every request with HTTP basic authentication as
described in [Authentication](#authentication).

This is safe because a campaign created through the API starts **Paused** (status 5), and a Paused campaign is never shown
to respondents. As long as your test campaigns stay Paused, no respondent will enter them and you will not be charged for any completes.

<aside class="warning">
Never set <code>status</code> to 2 (Active) on a test campaign. Active campaigns receive real respondents and you are charged for every complete.
</aside>

## Campaign statuses

Status | Name | What it means
------ | ---- | -------------
5 | Paused | The status every new campaign starts in. No respondents enter the survey.
2 | Active | The campaign is live and receives real respondents.
3 | Complete | The campaign is finished. No respondents enter the survey.

The API refuses to set a campaign to Active until it has at least one quota with `num_respondents` greater than 0. Treat
this as a safety net, not as the way you keep a test campaign offline: once your test has added a quota, only the
Paused status keeps it offline.

## Step 1: check feasibility

> Sample Request

```shell
curl -X POST -u "EMAIL_ADDRESS_YOU_PROVIDED:API_TOKEN" \
  -H "Content-Type: application/json" \
  https://www.tapresearch.com/api/v1/campaigns/realtime_feasibility \
  -d '{"incidence": 50, "length_of_interview": 10, "cpi": 1.5, "country_language_id": 1,
       "campaign_quotas": [{"num_respondents": 10,
         "campaign_qualifications": [{"question_id": 42, "pre_codes": [18, 19, 20, 21, 22]}]}]}'
```

`POST https://www.tapresearch.com/api/v1/campaigns/realtime_feasibility`

Estimates how many completes you can get without creating a campaign. See [Realtime Feasibility](#realtime-feasibility)
for the parameters.

## Step 2: create a test campaign

> Sample Request

```shell
curl -X POST -u "EMAIL_ADDRESS_YOU_PROVIDED:API_TOKEN" \
  -H "Content-Type: application/json" \
  https://www.tapresearch.com/api/v1/campaigns \
  -d '{"name": "TEST My first API campaign", "length_of_interview": 10, "incidence": 50,
       "cpi": 1.5, "country_language_id": 1,
       "supplier_link": "https://api.samplecompany.com/surveys/23423?id="}'
```

> Sample Response (shortened)

```json
{
  "id": 11598926,
  "name": "TEST My first API campaign",
  "status": 5,
  "total_remaining": 0
}
```

`POST https://www.tapresearch.com/api/v1/campaigns`

Start the name of every test campaign with `TEST` so you and our team can tell it apart from real work. Check that the
response shows `"status": 5`. Keep the `id`: the next steps use it. See [Create a campaign](#create-a-campaign) for every parameter.

## Step 3: add a quota

> Sample Request Payload

```json
{
  "num_respondents": 10,
  "name": "TEST age quota",
  "campaign_qualifications": [
    {
      "question_id": 42,
      "pre_codes": [18, 19, 20, 21, 22]
    }
  ]
}
```

`POST https://www.tapresearch.com/api/v1/campaigns/:campaign_id/campaign_quotas`

Quotas are nested under their campaign. The request body is the quota itself, not wrapped in another object. See
[Create a campaign quota](#create-a-campaign-quota) for every parameter, and [Lookups](#lookups) for question ids and pre-codes.

## Step 4: read and update

Route | What it does
----- | ------------
`GET /api/v1/campaigns` | Lists your campaigns.
`GET /api/v1/campaigns/:campaign_id` | Shows one campaign with its quotas.
`PUT /api/v1/campaigns/:campaign_id` | Updates a campaign, for example its name or length of interview. Leave `status` out, or send 5.
`GET /api/v1/campaigns/:campaign_id/campaign_quotas/:id` | Shows one quota.
`PUT /api/v1/campaigns/:campaign_id/campaign_quotas/:id` | Updates a quota.
`DELETE /api/v1/campaigns/:campaign_id/campaign_quotas/:id` | Deletes a quota.

## Step 5: try the respondent redirect

`GET https://www.tapresearch.com/api/v1/campaigns/:campaign_id/redirect_test`

Works on a Paused campaign. It returns your `supplier_link` with test values filled in, so you can check that your survey
accepts the respondent the way you expect without sending a real respondent. See [Redirect URL](#redirect-url).

## Step 6: clean up

> Sample Request Payload - Mark a test campaign Complete.

```json
{
  "status": 3
}
```

Campaigns cannot be deleted or archived through the API. When you are done with a test campaign:

1. Set it to Complete with `PUT /api/v1/campaigns/:campaign_id` and `"status": 3`.
2. Delete any quotas you no longer need with `DELETE /api/v1/campaigns/:campaign_id/campaign_quotas/:id`.
3. Email **api_support@tapresearch.com** with the ids of the test campaigns you no longer need.
