# Users

Users are one of the main pillars of Firstbird.

## Get All Users

This endpoint retrieves all Users for your company.

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users?offset=0&limit=2147483647",
  "total": 1,
  "offset": 0,
  "limit": 2147483647,
  "first": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users?offset=0&limit=2147483647"
  },
  "last": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users?offset=0&limit=2147483647"
  },
  "items": [
    {
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000001",
      "id": "00000000-0000-0000-0000-000000000001",
      "companyId": "00000000-0000-0000-0000-000000000000",
      "firstName": "Test",
      "lastName": "User",
      "email": "test.user@firstbird.com",
      "department": {
        "id": "00000000-0000-0000-0000-000000000002",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/departments/00000000-0000-0000-0000-000000000002"
      },
      "location": {
        "id": "00000000-0000-0000-0000-000000000003",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/locations/00000000-0000-0000-0000-000000000003"
      },
      "locale": "en_US",
      "status": "ACTIVE",
      "incognito": false,
      "mainRole": "ROLE_COMPANY_ADMIN",
      "timeZone": "Europe/Vienna",
      "roles": [
        "ROLE_COMPANY_ADMIN",
        "ROLE_RECRUITER",
        "ROLE_TALENT_SCOUT"
      ],
      "profile_picture": {
        "id": "00000000-0000-0000-0000-000000000003",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000001/profile_picture"
      },
      "employeeId": "123456"
    }
  ]
}
```

`GET /v1/companies/{companyId}/users`

### Query Parameters

| Query Parameter | Required | Description                                                                                                                                  |
|:----------------|:---------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| mainRoles       | No       | Comma separated list of main roles which should be included in the response. Allowed: ROLE_COMPANY_ADMIN, ROLE_RECRUITER or ROLE_TALENT_SCOUT
| roles           | No       | Comma separated list of roles which should be included in the response. Allowed: ROLE_COMPANY_ADMIN, ROLE_RECRUITER or ROLE_TALENT_SCOUT
| locations       | No       | Comma separated list of location ids which should be included in the response.
| departments     | No       | Comma separated list of department ids which should be included in the response.
| inactives       | No       | Whether inactive users should be included in the response or not. Allowed: true or false
| incognitos      | No       | Whether incognito users should be included in the response or not. Allowed: true or false
| exclude         | No       | Comma separated list of user ids which should not be included in the response.
| query           | No       | Filter by user name or email.
| status          | No       | Comma separated list of statuses which should be included in the response. Allowed: ACTIVE or INACTIVE
| fields          | No       | See [Fields](#customizing-response-fields) documentation.
| limit           | No       | See [Pagination](#pagination) documentation.
| offset          | No       | See [Pagination](#pagination) documentation.
| sort            | No       | See [Sorting](#sorting) documentation.

### Response Fields

| Property           | Required | Description                                      |
|:-------------------|:---------|:-------------------------------------------------|
| href               | Yes      | The link to this user.
| id                 | Yes      | The id of this user.
| companyId          | Yes      | The company this user belongs to.
| firstName          | Yes      | The first name of this user.
| lastName           | Yes      | The last name of this user.
| email              | Yes      | The email of this user.
| department         | Yes      | The department this user belongs to.
| location           | Yes      | The location this user belongs to.
| locale             | Yes      | The locale of this user.
| status             | Yes      | The status of this user.
| incognito          | Yes      | Whether this user is in incognito mode or not.
| mainRole           | Yes      | The main role of this user.
| roles              | Yes      | All roles of this user.
| timeZone           | Yes      | The time zone of this user.
| profile_picture    | No       | The profile picture of this user.
| employeeId         | No       | The external employee id of this user.