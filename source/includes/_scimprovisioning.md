# SCIM provisioning

The SCIM Microsoft Entra provisioning is a feature that allows you to manage user accounts in the Employee Referrals application using Microsoft Entra. This feature is useful for organizations that use Microsoft Entra as their identity provider and want to automate the user provisioning process.

## SCIM Admin Credentials

To set up SCIM Microsoft Entra provisioning, you need to have the following credentials:

* **Tenant URL**: The URL of your Radancy Referrals tenant. It follows the format `https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/`.
* **Bearer Token**: The token used to authenticate your requests.

The COMPANY ID is the unique identifier for your organization in the Employee Referrals application. You can find it in the Company ID Information of your Employee Referrals application in the account preferences, in the Integrations tab, under API Key Management.

To obtain the Bearer Token, you need to create a new API key in the Employee Referrals application. This token will be used to authenticate your requests to the SCIM Microsoft Entra provisioning API.

## Acquiring an OAuth Token

To acquire an OAuth token, you need to follow these steps in the Radancy Referrals application:

1. **Retrieve OAuth2 ClientId and Client Secret**: In the Employee Referrals application, navigate to the Integrations tab in the account settings and create a new API key. 
2. **Encode the ClientId and Client Secret**: Use Base64 encoding to encode the ClientId and Client Secret in the format `ClientId:ClientSecret`. This will be used in the Authorization header of your requests.

### Request an OAuth Token

To request an OAuth token, you need to send a POST request to the following endpoint:

`POST https://auth.1brd.com/oauth/token`

`Content-Type: application/x-www-form-urlencoded`

`Accept: application/json`

`Authorization: Basic {ClientId:ClientSecret Base64 encoded}`

>The authentication response will return a JSON object containing the access token, which you can use to authenticate your requests to the SCIM Microsoft Entra provisioning API.

```json
{
    "company_id": "2e6cc2fa-6a70-4dfe-b3ab-b012f25462db",
    "access_token": "YourAccessToken",
    "expires_in": 2147483646,
    "scope": "read write",
    "jti": "ede67ad4-60ac-4526-8c54-083d6e83ae46",
    "token_type": "Bearer"
}
```

The access token can be configured in the `Bearer Token` field in the Microsoft Entra provisioning settings.

## SCIM Microsoft Entra provisioning API

The SCIM Microsoft Entra provisioning API allows you to manage user accounts in the Employee Referrals application. The API follows the SCIM 2.0 standard and provides the following endpoints:

* **GET https://customer.services.1brd.com/api/scim/v2/ServiceProviderConfig**: Retrieve the service provider configuration for the SCIM Radancy Referrals provisioning API.
  
* **GET https://customer.services.1brd.com/api/scim/v2/ResourceTypes**: Retrieve the resource types for the SCIM Radancy Referrals provisioning API.
  
* **GET https://customer.services.1brd.com/api/scim/v2/Schemas**: Retrieve the schemas for the SCIM Radancy Referrals provisioning API.
  
* **GET https://customer.services.1brd.com/api/scim/v2/Schemas/User**: Retrieve the schema for the User resource type.
  
* **GET https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users**: Retrieve a list of users in the Employee Referrals application.
  
* **GET https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{USER ID}**: Retrieve a specific user by their ID.
  
* **POST https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users**: Create a new user in the Employee Referrals application.
  
* **PUT https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{USER ID}**: Update an existing user in the Employee Referrals application.

* **PATCH https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{USER ID}**: Update a specific user by their ID.
  
* **DELETE https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{USER ID}**: Delete a user from the Employee Referrals application.

## Custom User Attributes

The SCIM Microsoft Entra provisioning API supports custom attributes. You can use custom attributes to store additional information about users in the Employee Referrals application. Custom attributes are defined in the Employee Referrals application and can be used in the SCIM Microsoft Entra provisioning API.

The supported custom attributes for the SCIM Microsoft Entra provisioning API are as follows: 

| SCIM Custom Attribute                                                                  | Radancy Referrals Attribute | Required |
| -------------------------------------------------------------------------------------- | --------------------------- | -------- |
| urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User:locationName | user location name          | no       |
| urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User:role         | user role                   | no       |
| urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber              | user employee id            | no       |
| urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department                  | user department name        | no       |

## Service Provider Configuration

Returns Radancy Referrals SCIM service provider configuration, including supported features and capabilities.

### HTTP Request

`GET https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/ServiceProviderConfig`

## Schemas

Radancy Referrals supports schemas for Users. Querying the schemas endpoint returns the SCIM attributes.

## Resource Types

Returns the resource types supported by Radancy Referrals SCIM provisioning API.

## Get a User

To get a user using the SCIM Referrals provisioning API, you can use the following request:

### HTTP Request
`GET https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{id}`


### Example Request

`GET https://customer.services.1brd.com/api/customers/00000000-0000-0000-0000-000000000000/scim/v2/Users/00000000-0000-0000-0000-000000000001`


> This request returns JSON structured like this:

```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
    ],
    "id": "00000000-0000-0000-0000-000000000001",
    "externalId": "max.mustermann",
    "userName": "max.mustermann@example.com",
    "name": {
        "givenName": "Max",
        "familyName": "Mustermann",
    },
    "active": true,
    "emails": [
        {
            "value": "max.mustermann@example.com",
            "primary": true
        }
    ],
    "groups": [],
    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
        "department": "Product Development",
        "employeeNumber": "123456"
    },
    "urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User": {
        "locationName": "Austria",
        "role": "ROLE_RECRUITER"
    },
    "meta": {
        "resourceType": "User"
    }
}
```

## Create a User

In Radancy Referrals, the `userName` field must match the email address of the user.
To create a user using the SCIM Radancy Referrals provisioning API, you can use the following request:

### HTTP Request
`POST https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users`

### Example Request

`POST https://customer.services.1brd.com/api/customers/00000000-0000-0000-0000-000000000000/scim/v2/Users`

> This is an example request body

```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
    ],
    "externalId": "max.mustermann",
    "userName": "max.mustermann@example.com",
    "name": {
        "familyName": "Max",
        "givenName": "Mustermann"
    },
    "timezone": "America/Los_Angeles",
    "active": true,
    "emails": [
        {
            "value": "max.mustermann@example.com",
            "type": "work",
            "primary": true
        }
    ],
    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
        "employeeNumber": "123456",
        "department": "Product Development"
    },
    "urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User": {
        "locationName": "Los Angeles",
        "role": "ROLE_RECRUITER"
    }
}
```

The accepted values for the field `urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User:role` are:

* `ROLE_TALENT_SCOUT`
* `ROLE_RECRUITER`
* `ROLE_COMPANY_ADMIN`

> This is an example response body:

```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
    ],
    "id": "00000000-0000-0000-0000-000000000001",
    "externalId": "max.mustermann",
    "userName": "max.mustermann@example.com",
    "name": {
        "familyName": "Max",
        "givenName": "Mustermann"
    },
    "timezone": "America/Los_Angeles",
    "active": true,
    "emails": [
        {
            "value": "max.mustermann@example.com",
            "type": "work",
            "primary": true
        }
    ],
    "groups": [],
    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
        "employeeNumber": "123456",
        "department": "Product Development"
    },
    "urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User": {
        "locationName": "Los Angeles",
        "role": "ROLE_RECRUITER"
    },
    "meta": {
        "resourceType": "User"
    }
}
```

## Update a User

In Radancy Referrals, the `userName` field must match the email address of the user.
To update a user using the SCIM Radancy Referrals provisioning API, you can use the following request:

### HTTP Request
`PUT https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{id}`

### Example Request
`PUT https://customer.services.1brd.com/api/customers/00000000-0000-0000-0000-000000000001/scim/v2/Users/00000000-0000-0000-0000-000000000001`

> This is an example request body

```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
    ],
    "externalId": "max.mustermann",
    "userName": "max.mustermann@example.com",
    "name": {
        "familyName": "Max",
        "givenName": "Mustermann"
    },
    "timezone": "Europe/Vienna",
    "active": true,
    "emails": [
        {
            "value": "max.mustermann@example.com",
            "type": "work",
            "primary": true
        }
    ],
    "groups": [],
    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
        "employeeNumber": "654321",
        "department": "Product Development"
    },
    "urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User": {
        "locationName": "Vienna",
        "role": "ROLE_RECRUITER"
    }
}
```

> This is an example response body:

```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
    ],
    "id": "00000000-0000-0000-0000-000000000001",
    "externalId": "max.mustermann",
    "userName": "max.mustermann@example.com",
    "name": {
        "familyName": "Max",
        "givenName": "Mustermann"
    },
    "timezone": "Europe/Vienna",
    "active": true,
    "emails": [
        {
            "value": "max.mustermann@example.com",
            "type": "work",
            "primary": true
        }
    ],
    "groups": [],
    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
        "employeeNumber": "654321",
        "department": "Product Development"
    },
    "urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User": {
        "locationName": "Vienna",
        "role": "ROLE_RECRUITER"
    },
    "meta": {
        "resourceType": "User"
    }
}
```

## Patch a User

To patch a user using the SCIM Radancy Referrals provisioning API, you can use the following request:

### HTTP Request

`PATCH https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{id}`

### Example Request

`PATCH https://customer.services.1brd.com/api/customers/00000000-0000-0000-0000-000000000001/scim/v2/Users/00000000-0000-0000-0000-000000000001`

>This is an example request body:

```json
{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"
    ],
    "Operations": [
        {
            "op": "Replace",
            "path": "userName",
            "value": "max.updated@test.com"
        },
        {
            "op": "Replace",
            "path": "emails[type eq \"work\"].value",
            "value": "max.updated@test.com"
        },
        {
            "op": "Add",
            "path": "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department",
            "value": "Software Engineer"
        },
        {
            "op": "Remove",
            "path": "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber"
        }
    ]
}
```

>This is an example response body:

```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
    ],
    "id": "00000000-0000-0000-0000-000000000001",
    "externalId": "max.mustermann",
    "userName": "max.updated@test.com",
    "name": {
        "familyName": "Max",
        "givenName": "Mustermann"
    },
    "timezone": "Europe/Vienna",
    "active": true,
    "emails": [
        {
            "value": "max.updated@test.com",
            "type": "work",
            "primary": true
        }
    ],
    "groups": [],
    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
        "department": "Software Engineer"
    },
    "urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User": {
        "locationName": "Vienna",
        "role": "ROLE_RECRUITER"
    },
    "meta": {
        "resourceType": "User"
    }
}
```

## Get a List of Users

To get a list of users using the SCIM Radancy Referrals provisioning API, you can use the following request:

### HTTP Request

`GET https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users`

### Example Request
`GET https://customer.services.1brd.com/api/customers/00000000-0000-0000-0000-000000000001/scim/v2/Users`

> This request returns JSON structured like this:

```json
{
    "totalResults": 1,
    "itemsPerPage": 50,
    "startIndex": 1,
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:ListResponse"
    ],
    "Resources": [
        {
            "schemas": [
                "urn:ietf:params:scim:schemas:core:2.0:User",
                "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
            ],
            "id": "00000000-0000-0000-0000-000000000001",
            "externalId": "max.mustermann",
            "userName": "max.updated@test.com",
            "name": {
                "familyName": "Max",
                "givenName": "Mustermann"
            },
            "timezone": "Europe/Vienna",
            "active": true,
            "emails": [
                {
                    "value": "max.updated@test.com",
                    "type": "work",
                    "primary": true
                }
            ],
            "groups": [],
            "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User": {
                "department": "Software Engineer"
            },
            "urn:ietf:params:scim:schemas:extension:RadancyReferralsExtension:2.0:User": {
                "locationName": "Vienna",
                "role": "ROLE_RECRUITER"
            },
            "meta": {
                "resourceType": "User"
            }
        }
    ]
}
```

### Filtering Users

You can filter users by using the `filter` query parameter. The filter syntax is based on the SCIM 2.0 specification.

The fields that are supported for filtering are:

| SCIM Attribute |
|----------------|
| employeenumber |
| externalId     |
| userName       |
| email          |

The following operators are supported:

| Operator | Description |
|----------|-------------|
| eq       | equal       |
| ne       | not equal   |

Example filter queries:

`GET https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users?filter=userName eq \"max.mustermann@example.com\"`

## Delete a User

To delete a user using the SCIM Radancy Referrals provisioning API, you can use the following request:

### HTTP Request

`DELETE https://customer.services.1brd.com/api/customers/{COMPANY ID}/scim/v2/Users/{id}`

### Example Request

`DELETE https://customer.services.1brd.com/api/customers/00000000-0000-0000-0000-000000000001/scim/v2/Users/00000000-0000-0000-0000-000000000001`
