# Reward Plans

Reward Plans allow you to customize rewards defined by your company. Currently, there can be rewards for job application hires only.

## Get All Reward Plans

This endpoint retrieves all Reward Plans that are configured for your company.

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewarding/plans?offset=0&limit=2147483647",
  "total": 1,
  "offset": 0,
  "limit": 2147483647,
  "first": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewarding/plans?offset=0&limit=2147483647"
  },
  "last": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewarding/plans?offset=0&limit=2147483647"
  },
  "items": [
    {
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewarding/plans/00000000-0000-0000-0000-000000000005",
      "id": "00000000-0000-0000-0000-000000000005",
      "type": "hire",
      "name": "Just a Plan",
      "currency": "EUR",
      "external": false,
      "details": {
        "items": [
           {
              "description":"250€ Amazon Gift Card",
              "value":250,
              "paymentDate":"CANDIDATE_IS_HIRED"
           },
           {
              "description":"400€ Amazon Gift Card",
              "value":400,
              "paymentDate":"4_MONTHS_AFTER_EMPLOYMENT"
           }
        ]
      }
    }
  ]
}
```

`GET /v1/companies/{companyId}/rewarding/plans`

### Query Parameters

| Query Parameter | Required | Description                                                                                            |
|:----------------|:---------|:-------------------------------------------------------------------------------------------------------|
| status          | No       | Comma separated list of statuses which should be included in the response. Allowed: ACTIVE or INACTIVE |
| limit           | No       | See [Pagination](#pagination) documentation.                                                           |
| offset          | No       | See [Pagination](#pagination) documentation.                                                           |

### Response Fields

| Property                     | Required | Description                                                                                           |
|:-----------------------------|:---------|:------------------------------------------------------------------------------------------------------|
| href                         | Yes      | The link to this reward plan.
| id                           | Yes      | The id of this reward plan.
| type                         | Yes      | The type of reward plan. Supported types: *hire*
| name                         | Yes      | The name of this reward plan.
| currency                     | Yes      | The currency for this reward plan.
| external                     | Yes      | Whether this is an external reward or not.
| details.items                | Yes      | The rewards for this reward plan.
| details.items[i].description | Yes      | The description of this reward.
| details.items[i].value       | Yes      | The value of this reward.
| details.items[i].paymentDate | Yes      | The payment date of this reward.