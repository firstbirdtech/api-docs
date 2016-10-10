# Departments

Departments represent any unit of organization within your company, as an example, we here at Firstbird have the departments **Sales**, **IT and Marketing** & **PR**

## Get All Departments

This endpoint retrieves all departments that are configured for you company.

> This request returns JSON structured like this:

### HTTP Request

```json
[
  {
    "id": "50018463-d804-46ae-90a7-8187a12e6540",
    "name": "Sales"
  },
  {
    "id": "02a11025-4397-40b8-aa24-e09af0d784b0",
    "name": "Marketing & PR"
  },
  {
    "id": "5a768e73-3344-4a03-80cf-48f0c717f8f8",
    "name": "Product Development"
  }
]
```

`GET /v1/companies/{companyId}/departments`

## Get a Single Department
To get a single Department by it’s Id you have to use following request:

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "id": "02a11025-4397-40b8-aa24-e09af0d784b0",
  "name": "Marketing & PR"
}
```

`GET /v1/companies/{companyId}/departments/{departmentId}`

## Create a Department

To create a new Department for your Company use following request

### HTTP Request

> This is an example request body

```json
{
  "name":"Business Development"
}
```

> This request returns JSON structured like this:

```json
{
  "id": "54d49fa7-97cb-4502-bb55-4217cb281b3f"
}
```

`POST /v1/companies/{companyId}/departments`

### Parameters

| Property | Description                                                                                     |
|:---------|:------------------------------------------------------------------------------------------------|
| name     | The name of your new Department. We recommend to keep the names unique for all your Departments |

## Updating a Departments Status

To allow correct displaying of your Jobs and other entities using Departments on the one side and the need to remove outdated Departments we allow to set Departments inactive which is done with the following request:

### HTTP Request

> This is an example request body

```json
{
  "status":"INACTIVE"
}
```

`PUT /v1/companies/{companyId}/departments/{departmentId}/status`

### Parameters
| Property | Description                                                           |
|:---------|:----------------------------------------------------------------------|
| status   | New status of a the Department. Possible values are: INACTIVE, ACTIVE |
