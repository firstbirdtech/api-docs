# Locations

Locations represent the geographical entities of your company. We here at Firstbird have only one Location which is **Vienna**

## Get All Locations

This endpoint retrieves all locations that are configured for you company.

> This request returns JSON structured like this:

### HTTP Request

```json
[
  {
    "id": "50c7be5d-3e2d-4e57-9394-87d5ffc7f50f",
    "name": "Paris"
  },
  {
    "id": "9aac4ea9-09c3-41f0-868f-e1183dca3542",
    "name": "Munich"
  },
  {
    "id": "bfb10c01-fa32-499a-bbdd-34b5f166c272",
    "name": "Vienna"
  }
]
```

`GET /v1/companies/{companyId}/locations`

### Query Parameters
| Parameter | Description                                                                                                                          |
|:----------|:-------------------------------------------------------------------------------------------------------------------------------------|
| query     | A comma seperated list of fields that should be contained in the response. See [Fields](#customizing-response-fields) documentation. |

## Get a Single Location
To get a single Location by it’s Id you have to use following request:

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "id": "50c7be5d-3e2d-4e57-9394-87d5ffc7f50f",
  "name": "Paris"
}
```

`GET /v1/companies/{companyId}/locations/{locationId}`

## Create a Location

To create a new Location for your Company use following request

### HTTP Request

> This is an example request body

```json
{
  "name":"Chicago"
}
```

> This request returns JSON structured like this:

```json
{
  "id": "54d49fa7-97cb-4502-bb55-4217cb281b3f"
}
```

`POST /v1/companies/{companyId}/locations`

## Updating a Locations Status

To allow correct displaying of your Jobs and other entities using Locations on the one side and the need to remove outdated Locations we allow to set Locations inactive which is done with the following request:

### HTTP Request

> This is an example request body

```json
{
  "status":"INACTIVE"
}
```

`PUT /v1/companies/{companyId}/locations/{locationId}/status`

### Parameters
| Property | Description                                                         |
|:---------|:--------------------------------------------------------------------|
| status   | New status of a the Location. Possible values are: INACTIVE, ACTIVE |
