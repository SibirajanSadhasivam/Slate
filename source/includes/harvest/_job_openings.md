# Job Openings

This endpoint is used to managing openings on jobs.

## The job opening object

```json
[
    {
        "id": 123,
        "opening_id": "OPENED-1",
        "status": "open",
        "opened_at": "2015-11-19T19:53:32.565Z",
        "closed_at": null,
        "application_id": null,
        "close_reason": null,
      	"custom_fields": {
    	    "employment_type": "Full-Time",
             "maximum_budget": "$81.5k"
  	},
  	"keyed_custom_fields": {
    	    "employment_type": {
      		"name": "Time type",
      		"type": "single_select",
      		"value": "Full-Time"
    	    },
    	    "budget": {
      		"name": "Maximum Budget",
      		"type": "short_text",
      		"value": "$81.5k"
    	    }
    	}
    },
    {
        "id": 123,
        "opening_id": "CLOSED-1",
        "status": "closed",
        "opened_at": "2015-11-19T19:53:32.565Z",
        "closed_at": "2015-12-14T19:53:32.565Z",
        "application_id": 65565,
        "close_reason": {
          "id": 678,
          "name": "Hired - Backfill"
        },
      	"custom_fields": {
    	    "employment_type": "Full-Time",
             "maximum_budget": "$81.5k"
  	},
  	"keyed_custom_fields": {
    	    "employment_type": {
      		"name": "Time type",
      		"type": "single_select",
      		"value": "Full-Time"
    	    },
    	    "budget": {
      		"name": "Maximum Budget",
      		"type": "short_text",
      		"value": "$81.5k"
    	    }
    	}
    }
]
```

### Noteworthy Attributes

| Attribute | Description |
--------- | -----------
| id | The opening's unique identifier |
| opening_id | This is a text string used to identify the opening. This is defined by the users and may be null. |
| status | Either "open" or "closed" |
| opened_at | This is the date and time this opening was created. |
| closed_at | This is when the opening was closed; usually via the opening being filled. This should be null for opened openings. |
| application_id | The application that was used to fill this opening. This should only be set on a closed opening, null otherwise. |
| custom_fields | These are the custom fields that are specific to openings. This index, along with keyed_custom_fields, may not be included if your organization does not have access to custom fields on openings.

## GET: List Job Openings

```shell
curl 'https://harvest.greenhouse.io/v1/jobs/{job_id}/openings' -H "Authorization: Basic MGQwMzFkODIyN2VhZmE2MWRjMzc1YTZjMmUwNjdlMjQ6"
```
> The above command returns JSON structured like this:

```json
[
  {
      "id": 123,
      "opening_id": "OPENED-1",
      "status": "open",
      "opened_at": "2015-11-19T19:53:32.565Z",
      "closed_at": null,
      "application_id": null,
      "close_reason": null,
      "custom_fields": {
    	  "employment_type": "Full-Time",
          "maximum_budget": "$81.5k"
      },
      "keyed_custom_fields": {
          "employment_type": {
      	      "name": "Time type",
      	      "type": "single_select",
      	      "value": "Full-Time"
    	  },
    	  "budget": {
      	      "name": "Maximum Budget",
      	      "type": "short_text",
      	      "value": "$81.5k"
    	  }
      }
  },
  {
      "id": 123,
      "opening_id": "CLOSED-1",
      "status": "closed",
      "opened_at": "2015-11-19T19:53:32.565Z",
      "closed_at": "2015-12-14T19:53:32.565Z",
      "application_id": 65565,
      "close_reason": {
          "id": 678,
          "name": "Hired - Backfill"
      },
      "custom_fields": {
    	  "employment_type": "Full-Time",
          "maximum_budget": "$81.5k"
      },
      "keyed_custom_fields": {
          "employment_type": {
      	      "name": "Time type",
      	      "type": "single_select",
      	      "value": "Full-Time"
    	  },
    	  "budget": {
      	      "name": "Maximum Budget",
      	      "type": "short_text",
      	      "value": "$81.5k"
    	  }
      }
  }
]
```

List all of a job's openings

### HTTP Request

`GET https://harvest.greenhouse.io/v1/jobs/{job_id}/openings`

### URL Paramters

| Parameter | Description |
--------- | -----------
| job_id | The ID of the job for which you want to retrieve openings.

### Querystring Parameters

| Parameter | Description |
--------- | -----------
| status | May contain either "opened" or "closed"; when set will return only open or closed openings, respectively. Returns all openings if this isn't set or set to an unrecognized value. |

This endpoint supports pagination. See the [Pagination](#pagination) section for more detail.

[See noteworthy response attributes.](#the-job-opening-object)

## GET: Single Opening For Job

```shell
curl 'https://harvest.greenhouse.io/v1/jobs/{job_id}/openings/{id}' -H "Authorization: Basic MGQwMzFkODIyN2VhZmE2MWRjMzc1YTZjMmUwNjdlMjQ6"
```

> The above command returns JSON structured like this:

```
{
    "id": 123,
    "opening_id": "OPENED-1",
    "status": "open",
    "opened_at": "2015-11-19T19:53:32.565Z",
    "closed_at": null,
    "application_id": null,
    "close_reason": null,
    "custom_fields": {
    	"employment_type": "Full-Time",
        "maximum_budget": "$81.5k"
    },
    "keyed_custom_fields": {
        "employment_type": {
      	    "name": "Time type",
      	    "type": "single_select",
      	    "value": "Full-Time"
    	},
    	"budget": {
      	    "name": "Maximum Budget",
      	    "type": "short_text",
      	    "value": "$81.5k"
    	}
    }
}
```

Retrieve the information for a single opening.

### HTTP Request

`GET https://harvest.greenhouse.io/v1/jobs/{job_id}/openings/{id}`

### URL Parameters

| Parameter | Description |
--------- | -----------
| job_id | The ID of the job for which you want to retrieve openings.
| id | The ID of the opening you want to retrieve. Note: this is NOT the `opening_id` which is mutable and defined by Greenhouse users, but the `id` of an opening, which is unique to that opening and not mutable. |


[See noteworthy response attributes.](#the-job-opening-object)

## DELETE: Destroy Openings

``` shell
curl -X DELETE 'https://harvest.greenhouse.io/v1/jobs/{job_id}/openings'
-H "On-Behalf-Of: {greenhouse user ID}"
-H "Authorization: Basic MGQwMzFkODIyN2VhZmE2MWRjMzc1YTZjMmUwNjdlMjQ6"
```

```json
{
    "ids": [123, 456, 789]
}
```

### HTTP Request

`DELETE https://harvest.greenhouse.io/v1/jobs/{job_id}/openings`

### Headers

Header | Description
--------- | -----------
On-Behalf-Of | ID of the user issuing this request. Required for auditing purposes.

### JSON Body Parameters

Parameter | Required | Type | Description
--------- | ----------- | ----------- | -----------
ids | yes | Array | An array of opening ids to delete. Important to note that these are not `opening_id` from the other endpoints, but the unique `id` identifier.

**Note**: Closed/Filled openings can't be destroyed. This request is idempotent and will return the number of items destroyed, the number of closed items that couldn't be destroyed, and the number of IDs that could not be found. If you were to run the same request twice, the destroyed ID count would decrease and the invalid ID count would increase.

> The above returns a JSON response, structured like this

```
{
    "success": "2 opening(s) destroyed. 1 opening(s) were closed and not destroyed. 0 id(s) were not found."
}
```

## PATCH: Edit Openings

``` shell
curl -X PATCH 'https://harvest.greenhouse.io/v1/jobs/{job_id}/openings/{d}'
-H "On-Behalf-Of: {greenhouse user ID}"
-H "Authorization: Basic MGQwMzFkODIyN2VhZmE2MWRjMzc1YTZjMmUwNjdlMjQ6"
```

```json
{
    "opening_id": "abc-123",
    "status": "closed",
    "close_reason_id": 1234
}
```

### HTTP Request

`PATCH https://harvest.greenhouse.io/v1/jobs/{job_id}/openings/{id}`

### Headers

Header | Description
--------- | -----------
On-Behalf-Of | ID of the user issuing this request. Required for auditing purposes.

### URL Parameters

Parameter | Description
--------- | -----------
job_id | The ID of the job on which to add new openings.
id | The ID of the opening. Note this is the immutable internal id, and not the free-text "opening_id" from the JSON body.

### JSON Body Parameters

Parameter | Required | Type | Description
--------- | ----------- | ----------- | -----------
opening_id | no | string | This is a string that contains an opening_id. This may be a blank string. Changing an opening_id may re-trigger approvals. For approvals to start recruiting, this will reset approvals only if the job is in draft mode. If the job is open for hiring, these approvals will not reset. For official job approvals, this will reset approvals only if the job is open.
status | no | string | This can be used to set an open opening to closed by using the word "closed".  Status may only be used to set an open opening to closed. It does not accept any other value and cannot be used to re-open a closed opening. If the last opening is closed, it will close the hiring plan.
close_reason_id | no | integer | When closing, you may provide a close_reason_id. Providing a close_reason_id without closing the opening will return an error.

**Note**: Only open openings may be patched. Attempting to patch a closed opening will return an error. If the job is closed at the same time the opening_id is changed, approvals will be ignored in favor of closing the opening.

> The above returns a JSON response, structured like this:

```
{
    "success": "true"
}
```

## POST: Create New Openings

``` shell
curl -X POST 'https://harvest.greenhouse.io/v1/jobs/{job_id}/openings'
-H "On-Behalf-Of: {greenhouse user ID}"
-H "Authorization: Basic MGQwMzFkODIyN2VhZmE2MWRjMzc1YTZjMmUwNjdlMjQ6"
```

```json
{
    "openings": [
      {
          "opening_id": "abc-123",
          "custom_fields": [ { "id": 123, "value": "some value" } ]
      },
      {"opening_id": null}
    ]
}
```

### HTTP Request

`POST https://harvest.greenhouse.io/v1/jobs/{job_id}/openings`

### Headers

Header | Description
--------- | -----------
On-Behalf-Of | ID of the user issuing this request. Required for auditing purposes.

### URL Parameters

Parameter | Description
--------- | -----------
job_id | The ID of the job on which to add new openings.

### JSON Body Parameters

Parameter | Required | Type | Description
--------- | ----------- | ----------- | -----------
openings | yes | Array | This an array of hashes, which can contain an opening ID and custom fields.
openings.opening_id | yes | Array | This is a string that contains an opening_id. One new opening will be created for each hash element in the array. Opening ID is not required to have a string value and may be null.  Greenhouse has an internal limit of 100 open openings. If you attempt to create more than 100 openings in a single request, or if this request would create more than 100 open openings, the request will fail.
openings.custom_fields[] | No | Array | Array of custom field objects containing new custom field values. Passing an empty array does nothing. If you have any required custom fields configured for openings, they must be supplied for each new opening, or the request will fail. See the "Custom Field Object Parameters" section below for more details.

**Note**: Adding new openings may re-trigger approvals. For approvals to start recruiting, this will reset approvals only if the job is in draft mode. If the job is open for hiring, these approvals will not reset. For official job approvals, this will reset approvals only if the job is open.

### Custom Field Object Parameters

The custom field parameter structure is different in the POST method than in GET methods and responses. Certain types of custom fields require different elements to be included. See below for the description of each item in a custom field element and what is required depending on the type.

Parameter | Required for | Description
---------- | -------------- | ----------------
id | all | The custom field ID for this particular custom field.  One of this or `name_key` is required.
name_key | all | The name key for this custom field. This can be found in Greenhouse while editing custom options as `Immutable Field Key`. One of this or `id` is required.
value | all | The new custom field value.  In most cases this will be a string or a number.  In the case of single-select or multi-select custom fields, this will be a custom field option ID or an array of custom field option IDs, respectively. In the case of single-select fields, this can also be a string that matches an existing option's name exactly. See the [Custom Field Object for more details](#the-custom-field-object).
| min_value | number_range, currency range | The minimum value for a range. Must be less than max_value.
| max_value | number_range, currency_range | The maximum value for a range. Must be greater than min_value
unit | currency | This contains the currency unit for a currency custom field. It is only required when updating a currency custom field.  This should accept any 3-character currency code from the ISO-4217 standard.

> The above returns a JSON response, structured like this:

```json
{
    "openings": [
        {
            "id": 123456,
            "opening_id": "abc-123",
            "open_date": "2017-10-02T19:53:32.565Z"
        },
        {
            "id": 123457,
            "opening_id": null,
            "open_date": "2017-10-02T19:53:32.565Z"
        }
    ]
}
```
