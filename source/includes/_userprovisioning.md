# User Provisioning

Please note that the base URL for user provisioning is

`https://profile.services.1brd.com`

## Ingest User Profiles

> This is an example request body

```json
{
  "users": [ 
    {
      "first_name":"Test",
      "last_name":"User",
      "personnel_number":"1234",
      "email_address":"test.user@firstbird.com",
      "location":"Vienna",
      "department":"IT"
    },
    {
      "first_name":"Test",
      "last_name":"User2",
      "personnel_number":"1235",
      "email_address":"test.user2@firstbird.com"
    }
  ]
}
```

You can use this endpoint to send multiple `UserInformation` objects as a list of `users`.
This will stage all users for provisioning.

### HTTP Request

`POST /v1/companies/{companyId}/users/ingest`

### UserInformation Objects

All request parameters are in `string` format.

| Field name        | Required | Description                                |
|:------------------|:---------|:-------------------------------------------|
| first_name        | Yes      | First name                                 |
| last_name         | Yes      | Last name                                  |
| personnel_number  | Yes      | The id of the employee in your system      |
| email_address     | Yes      | Email address                              |
| location          | No       | The location of the user                   |
| department        | No       | The department of the user                 |

## Create a User Profile

> This is an example request body

```json
{
  "first_name":"Test",
  "last_name":"User",
  "email_address":"test.user@firstbird.com",
  "personnel_number":"1234",
  "active":true
}
```

To create a new user profile, use following request:

### HTTP Request

`POST /v1/companies/{companyId}/users/profile`

### Parameters

| Field name        | Required | Description                                                                                |
|:------------------|:---------|:-------------------------------------------------------------------------------------------|
| first_name        | Yes      | First name                                                                                 |
| last_name         | Yes      | Last name                                                                                  |
| personnel_number  | Yes      | The id of the employee in your system                                                      |
| email_address     | Yes      | Email address                                                                              |
| location          | No       | The location of the user                                                                   |
| department        | No       | The department of the user                                                                 |
| active            | No       | A `boolean` value to activate or deactivate a user in firstbird. Default value is `true`.  |

## Update a User Profile

> This is an example request body

```json
{
  "first_name":"Test",
  "last_name":"User",
  "email_address":"test.user@firstbird.com",
  "personnel_number":"1234",
  "active":true
}
```

To update a user profile, use following request:

### HTTP Request

`PUT /v1/companies/{companyId}/users/profile`

## Delete a User Profile

To delete a user profile, use following request:

### HTTP Request

`DELETE /v1/companies/{companyId}/users/profile`

### Query Parameters

| Query Parameter | Required | Description                                                                    |
|:----------------|:---------|:-------------------------------------------------------------------------------|
| identifier      | Yes      | You may use either of the `personnel_number` or the email address of the user. |

## Get a User Profile

> The request returns JSON structured like this:

```json
{
  "first_name":"Test",
  "last_name":"User",
  "email_address":"test.user@firstbird.com",
  "personnel_number":"1234",
  "active":true
}
```

To get a user profile, use following request:

### HTTP Request

`GET /v1/companies/{companyId}/users/profile`

### Query Parameters

| Query Parameter | Required | Description                                                                    |
|:----------------|:---------|:-------------------------------------------------------------------------------|
| identifier      | Yes      | You may use either of the `personnel_number` or the email address of the user. |