# Changelog

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