# Concepts

The following information is essential to understanding how the Firstbird API functions. You should familiarize yourself with it before moving on to the rest of this guide.

## Base URL

All URLs referenced in the API documentation begin with the following base URL:

`
https://api.1brd.com/v1/
`

This is the base URL for Firstbird’s public API. Please note that we only support `HTTPS`

## Resource Format
The Firstbird REST API currently only supports JSON resource representations.

## Authentication

```code
POST https://api.1brd.com/oauth/token
Content-Type: application/x-www-form-urlencoded
Accept: application/json
Authorization: Basic {apikey:apisecret base64 encoded}

grant_type=client_credentials&scope=read%20write
```

> This returns following response

```json
{
  "access_token": "youraccesstoken",
  "token_type": "bearer",
  "expires_in": 2147483646,
  "scope": "read write",
  "jti": "ede67ad4-60ac-4526-8c54-083d6e83ae46"
}
```

As Firstbird uses OAuth2 authentication mechanism, you can authenticate your services using OAuth2 Client Credentials authentication method. To authenticate a Company Administrator needs to generate an API key and API secret within the account settings. With the key and the secret you can request a so called Bearer token from our API with the request to the right.

### Authenticating Requests

> The access token can be used to authenticate for any further request.

```code
GET /v1/{anyrequest}
Authorization: Bearer youraccesstoken
```

To authenticate any request from now on you have to add the access token your received in `access_token` field to the `Authorization` header of the request, prefixed with “Bearer”.

## Creating Resources

You create a resource by submitting an HTTP **POST** to a resource URL. Any POST body must be represented as **JSON**. Requests that contain body content must specify the HTTP `Content-Type` header with a value of `application/json`.

Responses to your create POST calls will contain:

* An HTTP Status Code indicating success or failure (possible codes can be found below)
* Any HTTP Headers
* A Response Body, which will contain the created entity resource (if the call succeeded), or a detailed error (if the call failed)

### Status Codes
| Response Code                | Description                                                                                                              |
|:-----------------------------|:-------------------------------------------------------------------------------------------------------------------------|
| `201 CREATED`                | The request was successful, we created a new resource, and the response body contains the representation.                |
| `400 BAD REQUEST`            | The data given in the POST failed validation. Inspect the response body for details.                                     |
| `401 UNAUTHORIZED`           | Authentication credentials are required to access the resource. All requests must be authenticated.                      |
| `403 FORBIDDEN`              | The supplied authentication credentials are not sufficient to access the resource.                                       |
| `404 NOT FOUND`              | We could not locate the resource based on the specified URL.                                                             |
| `405 METHOD NOT ALLOWED`     | POST is not supported for the resource.                                                                                  |
| `409 CONFLICT`               | You cannot create or update a resource because another resource already exists or conflicts with one you are submitting. |
| `415 UNSUPPORTED MEDIA TYPE` | You did not specify the request `Content-Type` header to have a value of `application/json`.                             |
| `500 SERVER ERROR`           | We could not create or update the resource. Please try again.                                                            |
| `503 SERVICE UNAVAILABLE`    | We are temporarily unable to service the request. Please wait for a bit and try again.                                   |

## Updating Resources
If you want to update a resource, submit an HTTP PUT request to the resource’s URL. Any request body must be represented as JSON. You must submit all attributes. As with the creation POST calls, requests that contain body content must specify the HTTP `Content-Type` header with a value of `application/json`.

Responses to your update requests will contain:

* An HTTP Status Code indicating success or failure (possible codes can be found below)
* Any HTTP Headers
* A Response Body, which will contain the created entity resource (if the call succeeded), or a detailed error (if the call failed)

### Status Codes

| Response Code                | Description                                                                                                              |
|:-----------------------------|:-------------------------------------------------------------------------------------------------------------------------|
| `200 OK`                     | The request was successful and the response body contains the resource requested.                                        |
| `400 BAD REQUEST`            | The data given in the POST failed validation. Inspect the response body for details.                                     |
| `401 UNAUTHORIZED`           | Authentication credentials are required to access the resource. All requests must be authenticated.                      |
| `403 FORBIDDEN`              | The supplied authentication credentials are not sufficient to access the resource.                                       |
| `404 NOT FOUND`              | We could not locate the resource based on the specified URL.                                                             |
| `405 METHOD NOT ALLOWED`     | POST is not supported for the resource.                                                                                  |
| `409 CONFLICT`               | You cannot create or update a resource because another resource already exists or conflicts with one you are submitting. |
| `415 UNSUPPORTED MEDIA TYPE` | You did not specify the request `Content-Type` header to have a value of `application/json`.                             |
| `500 SERVER ERROR`           | We could not create or update the resource. Please try again.                                                            |
| `503 SERVICE UNAVAILABLE`    | We are temporarily unable to service the request. Please wait for a bit and try again.                                   |

## Deleting Resources
To delete a resource, make an HTTP `DELETE` request to the resource URL. Note that not all Firstbird API resources support `DELETE`.

### Status Codes

| Response Code             | Description                                                                                         |
|:--------------------------|:----------------------------------------------------------------------------------------------------|
| `200 OK`                  | The request was successful and the response body contains the resource requested.                   |
| `401 UNAUTHORIZED`        | Authentication credentials are required to access the resource. All requests must be authenticated. |
| `403 FORBIDDEN`           | The supplied authentication credentials are not sufficient to access the resource.                  |
| `404 NOT FOUND`           | We could not locate the resource based on the specified URL.                                        |
| `405 METHOD NOT ALLOWED`  | POST is not supported for the resource.                                                             |
| `500 SERVER ERROR`        | We could not create or update the resource. Please try again.                                       |
| `503 SERVICE UNAVAILABLE` | We are temporarily unable to service the request. Please wait for a bit and try again.              |

## Error Responses

```json
{
  "status" : 404,
  "code" : "4040",
  "message": "Oops!",
  "message" : "The resource you have called couldn't be found"
}
```

REST API responses indicating an error or warning are represented by a proper response HTTP status code (403, 404, etc) along with a response body containing the following information:

| Attributes         | Type   | Description                                                                                     |
|:-------------------|:-------|:------------------------------------------------------------------------------------------------|
| `status`           | Number | The corresponding HTTP status code.                                                             |
| `code`             | Number | A Firstbird specific error code that can be used to obtain more information.                    |
| `message`          | String | A simple, easy to understand message that you can show directly to your application’s end-user. |
| `developerMessage` | String | A clear explanation with technical details that might assist a developer calling our API.       |

## Collection Resource

A Collection Resource is a resource containing other resources. It is known as a Collection Resource because it is itself a first class resource - it has its own attributes in addition to the resources it contains.

If you want to interact with multiple resources, you must do so with a Collection Resource. Collection Resources also support additional behavior specific to collections, such as pagination, sorting, and searching.

The Collection response will contain the elements of the collection in the array-field `items`.

### Pagination

> The following example shows a paginated response

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=0&limit=25",
  "total": 100,
  "offset": 25,
  "limit": 25,
  "first": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=0&limit=25"
  },
  "last": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=0&limit=25"
  },
  "next": {
    "href": "http://localhost:8081/api/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=25&limit=25"
  },
  "last": {
    "href": "http://localhost:8081/api/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=75&limit=25"
  },
  "items": [
    {
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
      "id": "0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
      "...":"..."
    },
    {
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/14e35b9e-669e-4e9a-bb23-2f2ea550318f",
      "id": "14e35b9e-669e-4e9a-bb23-2f2ea550318f",
      "...": "..."
    },
    "..."
  ]
}
```

If a Collection Resource represents a large enough number of resource instances, it will not include them all in a single response. Instead a technique known as pagination is used to break up the results into one or more pages of data. You can request additional pages as separate requests.

There are two optional query parameters that may be specified to control pagination:

| Query Parameter | Description                                                                                                                     |
|:----------------|:--------------------------------------------------------------------------------------------------------------------------------|
| `offset`        | The zero-based starting index in the entire collection of the first item to return. Default is 0.                               |
| `limit`         | The maximum number of collection items to return for a single request. Minimum value is 1. Maximum value is 100. Default is 25. |

| Field    | Description                                                                       |
|:---------|:----------------------------------------------------------------------------------|
| `href`   | The request line that has been used to get the current response                   |
| `total`  | Total number of all elements for the request (e.g., All Jobs the request matches) |
| `offset` | The offset used in the current request                                            |
| `limit`  | The limit used in the current request                                             |
| `first`  | The URL to get the first limit items of the collection                            |
| `next`   | The URL to the next limit items of the collection                                 |
| `last`   | The URL to the last limit or less items of the collection                         |


### Sorting

To sort collection resources there is the `sort` query parameter which allows you to specify the field and the sorting direction.

`GET /v1/companies/{companyId}/jobs?sort=title,asc`

`GET /v1/companies/{companyId}/jobs?sort=title,desc`

Please keep in mind that sorting does not work for all collection resources. If it is possible to sort the response, it will be explicitly mentioned. You are not able to sort nested properties as well as you are not able to sort for non-primitive object properties.

## Customizing Response Fields

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
  "id": "0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
  "location": {
    "id": "50c7be5d-3e2d-4e57-9394-87d5ffc7f50f",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/location/50c7be5d-3e2d-4e57-9394-87d5ffc7f50f"
  }
}
```

To fit your needs we allow to customize which fields are included in our responses. By default all available fields are included in a response. To select fields to be included use the fields query parameter which takes a comma separated list of fields. Take a look at the following Job request for an example:

`GET /v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a?fields=id,location`

## Links and Resource Expansion

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005",
  "id": "00000000-0000-0000-0000-000000000005",
  "company": {
    "id": "00000000-0000-0000-0000-000000000000",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
  },
  "location": {
    "id": "00000000-0000-0000-0000-000000000001",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/locations/00000000-0000-0000-0000-000000000001"
  },
  "department": {
    "id": "00000000-0000-0000-0000-000000000002",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/departments/00000000-0000-0000-0000-000000000002"
  },
  "reward": {
    "id": "00000000-0000-0000-0000-000000000003",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewards/00000000-0000-0000-0000-000000000003"
  },
  "...":"..."
}
```

At Firstbird we want to provide a powerful REST API which allows easy navigation through our services. Therefore we do not simply add the IDs of referenced resources to our responses but also provide links where you can find mor detailed information about the referenced resource. If you take a look at an example response where a single Job has been fetched you can see the properties company, location, department and reward which reference the Company the Job belongs to and the Location, Department And Reward which are associated to the Job. All objects contain their ID in `id` property and a link to the REST API Resource in property `href`.

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005",
  "id": "00000000-0000-0000-0000-000000000005",
  "company": {
    "id": "00000000-0000-0000-0000-000000000000",
    "name": "Firstbird",
    "domainName": "1bird",
    "website": "www.firstbird.eu"
  },
  "location": {
    "name": "Paris",
    "id": "00000000-0000-0000-0000-000000000001"
  },
  "department": {
    "name": "Finance",
    "id": "00000000-0000-0000-0000-000000000002"
  },
  "reward": {
    "name": "250€ Amazon Gift Card",
    "id": "00000000-0000-0000-0000-000000000003"
  },
  "...":"..."
}
```

`GET /v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005`

To make it even easier for you to use our API, it is possible to expand (include) often used referenced resources within the responses to avoid additional requests to those referenced resources. If you take a look on following Job requests as an example you can see that we expanded the company, location, department and reward resources which add their values you are allowed to see to the response. To specify which resources should get expanded you have to specify a comma separated list of fields for the expand query parameter.

`GET /v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005?expand=company,location,department,reward`
