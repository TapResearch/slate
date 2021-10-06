# Changelog

## 10/6/2021
- Supplier Links
  - Added a separate section for Supplier Links to replace the supplier_link document found under Campaigns. 
  - Added a Security section to document the new optional substitution value {LINK_HASH} used for the purpose of appending an HMAC-SHA1 security hash to the end of the Supplier Link via the security_hash parameter.

## 9/8/2021
- Campaign Exclusions
  - Added /campaign_exclusions route that allows for the exclusion of transaction and player ids on specified campaigns.
- Campaign Export
  - Added /export_demographics route that allows for an CSV export of campaign information.
- Campaigns 
  - Added ability to include any question_id from the /qualifications route as a substitution value to the respondents demographics portion of supplier link attribute.
  - Added /redirect_test route that retrieves the redirect_test_url for a specific campaign.
- Custom Screeners
  - We now have the ability to create/edit/destroy custom screeners (qualifications) and as a result the following routes have been added.
      - /custom_qualifications 
      - /custom_qualification_answers
      - /campaign_qualifications
- Campaign Quotas
  - Added disclaimer on usage of multiple location qualifications on a single quota.

## 8/20/2021
- Callbacks 
  - Added Quality Term route.  
- Campaigns
  - Updated verbiage around CPI parameter to indicate the currency is always USD.

## 8/9/2021
- Campaign Quotas  
  - Name parameter can now be updated.  
  - Added is_clicked_balanced parameter.  
- Changelog  
  - Versions is now known as changelog and updated format to use date instead of version number.

## v1.07
- Campaigns
  - Added max_daily_completes as an optional attribute.
  - Added reenetry_interval as an optional attribute.
  - Added {RETARGETING_IDENTIFIER} substitution value to supplier link attribute.
- Campaign Retargeting
  - Update request payload structure. Allow replacement identifier as optional value for 
    each retarget.
- Campaign Relationships
  - Added /campaign_relationships route which will exlcude two campaigns from flow.

## v1.06
- Campaigns
  - Added /retarging route.

## v1.05
- Campaigns
  - Added /realtime_feasibility route.

## v1.04
- Campaigns
  - The CPI parameter is now read-only. We will generate the CPI value using our rate card.

## v1.03
- Campaigns
  - Added the campaign level /feasibility route.
- Callbacks
  - Added callback URLs.

## v1.02
- Campaigns
  - Added days_in_field as an optional attribute. Default value is 5.
- Campaign Quotas
  - Added /feasibility route which will return the estimated number of completes based on days_in_field.

## v1.01
- Campaigns
  - Added /reject_completes route.

## v1.00
- Campaigns
  - Get a list of campaigns that belong to you.
  - Create, update, and show a campaign.
- Campaign Quotas
  - Create, update, and show a campaign_quota
- Qualifications
  - Get a list of accepted targeting criteria.
  - Get answer options for a specific qualification.