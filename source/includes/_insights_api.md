# Insights API

## List organization projects

> Sample Response

```json
{
  "data": {
    "id": "projects_list_683",
    "type": "projects_list",
    "attributes": {
      "page": 1,
      "pages": 2,
      "projects": {
        "data": [
          {
            "id": "87",
            "type": "project",
            "attributes": {
              "id": 87,
              "name": "A one time project",
              "project_type": "one_time",
              "campaigns": {
                "data": [
                  {
                    "id": "478",
                    "type": "campaign",
                    "attributes": {
                      "id": 478,
                      "status": "complete",
                      "complete_at": "2022-07-01T19:01:18.000Z",
                    },
                    "links": {
                      "results_url": "https://www.tapresearch.com/insights_api/projects/87/campaigns/478",
                      "columns_url": "https://www.tapresearch.com/insights_api/projects/87/campaigns/478/columns"
                    }
                  }
                ]
              }
            }
          },
          {
            "id": "318",
            "type": "project",
            "attributes": {
              "id": 318,
              "name": "A recurring project",
              "project_type": "recurring",
              "campaigns": {
                "data": [
                  {
                    "id": "509",
                    "type": "campaign",
                    "attributes": {
                      "id": 509,
                      "status": "complete",
                      "complete_at": "2022-07-01T19:01:18.000Z",
                    },
                    "links": {
                      "results_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/509",
                      "columns_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/509/columns"
                    }
                  },
                  {
                    "id": "510",
                    "type": "campaign",
                    "attributes": {
                      "id": 510,
                      "status": "complete",
                      "complete_at": "2022-07-07T19:01:18.000Z",
                    },
                    "links": {
                      "results_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/510",
                      "columns_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/510/columns"
                    }
                  },
                  {
                    "id": "511",
                    "type": "campaign",
                    "attributes": {
                      "id": 511,
                      "status": "active",
                      "complete_at": null,
                    },
                    "links": {
                      "results_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/511",
                      "columns_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/511/columns"
                    }
                  }
                ]
              }
            }
          }
        ]
      }
    }
  }
}
```

Get a list of projects for the organization. Request identity/organization is derived from the `Authorization` header.

**Note:** Projects that are still in draft are not returned.

### HTTP Request

`GET https://www.tapresearch.com/insights_api/projects`

### Required Parameters
`NONE`

### Optional Parameters
Parameter | Type | Description
--------- | ---- | -----------
project_type | `String` | Pass this parameter to return only projects of the specified type. Accepted values: `recurring` or `one_time`
page | `Integer` | Response is paginated, 30 projects per page. By default this endpoint returns the first page. If you have more than 30 projects, you will need to make subsequent requests using the `page` parameter.

### Response
Response follows the [JSON:API specification](https://jsonapi.org/format/). Each resource type returns a top-level `data` key, and within that, an `attributes` field containing the data.

<h3 style="margin: 30px 0 10px;">Top-Level Fields</h3>

Parameter | Type | Description
--------- | ---- | -----------
id | `String` | Unique identifier in the format: `projects_list_<Organization ID>`
type | `String` | Resource type: `projects_list`
attributes | `Object` | Object which contains the resource data (see below)

<h3 id="projects-list- style="margin: 30px 0 10px;"><code style="font-size: 15px;">data.attributes</code> Fields</h3>

Parameter | Type | Description
--------- | ---- | -----------
page | `Integer` | The current page being returned
pages | `Integer` | The total number of pages for this resource
projects | `Array of projects` | List of projects for the organization. If a `project_type` param was not specified, the list may contain both one-time and recurring projects (if they both exist). See below for [projects item attributes](#projects-item-fields).

<h3 id="projects-item-fields" style="margin: 30px 0 10px;"><code style="font-size: 15px;">projects</code> Attributes</h3>

Parameter | Type | Description
--------- | ---- | -----------
id | `Integer` | Project ID
name | `String` | Project name
project_type | `String` | Project type: `one_time` or `recurring`
campaigns | `Array of campaigns` | List of campaigns for the project. One-time projects will have only 1 campaign returned. Recurring project waves are in order using 0-based indexing where `wave_number = index + 1`. See below for [campaigns item attributes](#campaigns-item-fields) and [campaigns item links](#campaigns-item-links).

<h3 id="campaigns-item-fields" style="margin: 20px 0 10px;"><code style="font-size: 15px;">projects.campaigns</code> Attributes</h3>

Parameter | Type | Description
--------- | ---- | -----------
id | `Integer` | Campaign ID
status | `String` | Campaign status: `active` / `paused` / `complete` / `archived`
complete_at | `String` or `null` | Date completed in RFC 3339 format, or null (when campaign is not complete)

<h3 id="campaigns-item-links" style="margin: 20px 0 10px;"><code style="font-size: 15px;">projects.campaigns</code> Links</h3>

Parameter | Type | Description
--------- | ---- | -----------
results_url | `String` or `null` | Endpoint URL that returns the results CSV file, or null (when there's no responses yet).
columns_url | `String` or `null` | Endpoint URL that returns the CSV file headers mapping `{ column_id: "Column title" }`

## Get a specific project

> Sample Response

```json
{
  "data": {
    "id": "318",
    "type": "project",
    "attributes": {
      "id": 318,
      "name": "A recurring project",
      "project_type": "recurring",
      "campaigns": {
        "data": [
          {
            "id": "509",
            "type": "campaign",
            "attributes": {
              "id": 509,
              "status": "complete",
              "complete_at": "2022-07-01T19:01:18.000Z",
            },
            "links": {
              "results_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/509",
              "columns_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/509/columns"
            }
          },
          {
            "id": "510",
            "type": "campaign",
            "attributes": {
              "id": 510,
              "status": "complete",
              "complete_at": "2022-07-07T19:01:18.000Z",
            },
            "links": {
              "results_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/510",
              "columns_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/510/columns"
            }
          },
          {
            "id": "511",
            "type": "campaign",
            "attributes": {
              "id": 511,
              "status": "active",
              "complete_at": null,
            },
            "links": {
              "results_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/511",
              "columns_url": "https://www.tapresearch.com/insights_api/projects/318/campaigns/511/columns"
            }
          }
        ]
      }
    }
  }
}
```

Get a specific project by ID with its associated campaigns.

### HTTP Request

`GET https://www.tapresearch.com/insights_api/projects/:project_id`

### Required Parameters
`NONE`

### Response

Parameter | Type | Description
--------- | ---- | -----------
id | `Integer` | Project ID
name | `String` | Project name
project_type | `String` | Project type: `one_time` or `recurring`
campaigns | `Array of campaigns` | List of campaigns for the project. One-time projects will have only 1 campaign returned. Recurring project waves are in order using 0-based indexing where `wave_number = index + 1`. See below for [campaigns item attributes](#campaigns-item-fields) and [campaigns item links](#campaigns-item-links).

<h3 id="campaigns-item-fields" style="margin: 20px 0 10px;"><code style="font-size: 15px;">campaigns.attributes</code></h3>

Parameter | Type | Description
--------- | ---- | -----------
id | `Integer` | Campaign ID
status | `String` | Campaign status: `active` / `paused` / `complete` / `archived`
complete_at | `String` or `null` | Date completed in RFC 3339 format, or null (when campaign is not complete)

<h3 id="campaigns-item-links" style="margin: 20px 0 10px;"><code style="font-size: 15px;">campaigns.links</code></h3>

Parameter | Type | Description
--------- | ---- | -----------
results_url | `String` or `null` | Endpoint URL that returns the results CSV file, or null (when there's no responses yet).
columns_url | `String` or `null` | Endpoint URL that returns the CSV file headers mapping `{ column_id: "Column title" }`

## Get the CSV headers for a campaign

> Sample Response

```json
{
  "data": {
    "id": "columns_510",
    "type": "campaign_columns",
    "attributes": {
      "columns": {
        "id": "Id",
        "time": "Time",
        "panelist_id": "Panelist ID",
        "join_date": "Join date",
        "status": "Status",
        "pq_42": "Age",
        "pq_101": "Division",
        "pq_97": "Dma",
        "pq_113": "Ethnicity",
        "pq_43": "Gender",
        "pq_122": "Region",
        "pq_633": "Education",
        "pq_2189": "Employment",
        "pq_14785": "Household income",
        "pq_14785_non_bucketed": "Household income (raw value)",
        "pq_96": "State",
        "pq_45": "Zip",
        "pq_50017": "Birthday",
        "pq_50020": "Parent of children under 18",
        "tq_1325": "Do you ever travel internationally?",
        "tq_1326": "Which of the following countries have you visited?",
        "tq_1327": "Rank the following countries in order of places you want to visit.",
        "tq_1328": "Which of these factors is most important to you when considering international travel?",
      }
    }
  }
}
```

<span id="csv-columns">Returns the CSV file header mapping for a given campaign.</span>


### HTTP Request

`GET https://www.tapresearch.com/insights_api/:project_id/campaigns/:campaign_id/columns`

### Required Parameters
`NONE`


<h3 id="base-columns" style="margin: 20px 0 10px;">Base Data Columns</h3>

Column | Description
------ | -----------
id | Respondent session identifier
time | Session start timestamp
panelist_id | Unique respondent identifier
join_date | Respondent join date
status | Respondent survey result status (usually `Complete`)

<h3 id="demographic-columns" style="margin: 20px 0 10px;">Demographic Columns</h3>

Column | Description
------ | -----------
`pq_<Demographic ID>` | These columns represent the various demographic data points returned.

<h3 id="question-columns" style="margin: 20px 0 10px;">Survey Question Columns</h3>

Column | Description
------ | -----------
`tq_<Root Question ID>` | These columns represent the answers to the survey questions.

<aside style="font-size: 14px;"><b>Note:</b> <code style="font-size: 14px;">tq_*</code> columns always use the <b>root question ID</b>. This is critical for recurring projects, because the question IDs will remain constant across waves, <b>even if the question text is updated or changed</b>. This endpoint will return the specific version of the question text that was used for this wave/campaign.</aside>

## Get a campaign result CSV

Returns the CSV results export for a given campaign.

### HTTP Request

`GET https://www.tapresearch.com/insights_api/:project_id/campaigns/:campaign_id`


### Required Parameters
`NONE`

### Response

<h3 style="margin: 30px 0 10px;">HTTP Headers</h3>

Header | Value
------ | -----
Content-Type | `text/csv`
Content-Disposition | `attachment; filename="campaign_result_<Campaign ID>.csv"`

<h3 style="margin: 30px 0 10px;">CSV Format</h3>

Refer to the [CSV columns endpoint](#get-the-csv-headers-for-a-campaign) to see the data returned for a campaign.