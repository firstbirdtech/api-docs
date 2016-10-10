# Job Applications

Job Applications are the other main pillar of your Account at Firstbird.

Job Applications can have following statuses:

| Status      | Description                                                                           |
|:------------|:--------------------------------------------------------------------------------------|
| IN_PROGRESS | This Job Application is currently in progress and waits for your Recruiters decisions |
| HIRED       | The candidate of this Job Application got hired                                       |
| CLOSED      | The Job Application has been withdrawn by your Recruiters                             |

Your recruiters can give a Job Application different ratings:

| Rating | Description                                                             |
|:-------|:------------------------------------------------------------------------|
| A      | The A rating corresponds to the 3-star rating from the web applications |
| B      | The B rating corresponds to the 2-star rating from the web applications |
| C      | The C rating corresponds to the 1-star rating from the web applications |

## Get All Job Applications

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications?offset=0&limit=2147483647",
  "total": 2,
  "offset": 0,
  "limit": 2147483647,
  "first": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications?offset=0&limit=2147483647"
  },
  "last": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications?offset=1&limit=2147483647"
  },
  "items": [
    {
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e",
      "id": "d648096f-c3f4-4121-af9a-5377753e467e",
      "status": "IN_PROGRESS",
      "applicationDate": "2016-03-23T08:37:15Z",
      "company": {
        "id": "00000000-0000-0000-0000-000000000000",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
      },
      "applicant": {
        "id": "1d029da5-0a39-45d2-a26a-eb14a5d05d36",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applicants/1d029da5-0a39-45d2-a26a-eb14a5d05d36"
      },
      "referrer": {
        "id": "dddddddd-dddd-dddd-dddd-dddddddddddd",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/dddddddd-dddd-dddd-dddd-dddddddddddd"
      },
      "share": {
        "id": "4d61dae4-8444-4e7d-a73b-20aa6aa02093",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a/shares/4d61dae4-8444-4e7d-a73b-20aa6aa02093"
      },
      "job": {
        "id": "0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a"
      },
      "referrals": {
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/referrals"
      },
      "files": [
        {
          "id": "a3beb15a-84ac-4646-a20b-7aa5faf982a7",
          "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/files/a3beb15a-84ac-4646-a20b-7aa5faf982a7"
        }
      ],
      "applicantImage": {
        "href": "https://s3.eu-central-1.amazonaws.com/hummingbird-development/applicantimg/150x150/b642441c-2dc4-4cd1-8873-c5d7e2e725f2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20160323T083722Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Credential=AKIAJX7FDXXZDKC4NZVA%2F20160323%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Signature=06981e7b0b46d4d43cd407bd2848391a01195714f6ce0df2a8cb67358efaa598"
      },
      "rewardPaid": false
    }
  ]
}
```

To get a list of all your Job Applications user following request:

### HTTP Request

`GET /v1/companies/{companyId}/applications`

### Query Parameters

| Query Parameter | Description                                                                                                                       |
|:----------------|:----------------------------------------------------------------------------------------------------------------------------------|
| status          | A comma separated list of statuses. Possible values are IN_PROGRESS, HIRED and CLOSED                                             |
| rating          | A comma separated list of ratings. Possible values are A, B and C                                                                 |
| rated           | A boolean value filtering for Job Applications that are whether rated or not. Possible values are true and false                  |
| fields          | See [Fields](#customizing-response-fields) documentation                                                                          |
| expand          | See [Resource Expansion](#links-and-resource-expansion) documentation. Expandable fields are: applicant, referrer, job, referrals |
| offset          | See [Pagination](#pagination) documentation                                                                                       |
| limit           | See [Pagination](#pagination) documentation                                                                                       |
| sort            | See Sorting documentation                                                                                                         |

## Get a Single Job Application

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e",
  "id": "d648096f-c3f4-4121-af9a-5377753e467e",
  "status": "IN_PROGRESS",
  "applicationDate": "2016-03-23T08:37:15Z",
  "company": {
    "id": "00000000-0000-0000-0000-000000000000",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
  },
  "applicant": {
    "id": "1d029da5-0a39-45d2-a26a-eb14a5d05d36",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applicants/1d029da5-0a39-45d2-a26a-eb14a5d05d36"
  },
  "referrer": {
    "id": "dddddddd-dddd-dddd-dddd-dddddddddddd",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/dddddddd-dddd-dddd-dddd-dddddddddddd"
  },
  "share": {
    "id": "4d61dae4-8444-4e7d-a73b-20aa6aa02093",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a/shares/4d61dae4-8444-4e7d-a73b-20aa6aa02093"
  },
  "job": {
    "id": "0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a"
  },
  "referrals": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/referrals"
  },
  "files": [
    {
      "id": "a3beb15a-84ac-4646-a20b-7aa5faf982a7",
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/files/a3beb15a-84ac-4646-a20b-7aa5faf982a7"
    }
  ],
  "applicantImage": {
    "href": "https://s3.eu-central-1.amazonaws.com/hummingbird-development/applicantimg/150x150/b642441c-2dc4-4cd1-8873-c5d7e2e725f2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20160323T083722Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Credential=AKIAJX7FDXXZDKC4NZVA%2F20160323%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Signature=06981e7b0b46d4d43cd407bd2848391a01195714f6ce0df2a8cb67358efaa598"
  },
  "read": false,
  "rewardPaid": false
}
```

To get a single Job Application you have to use following request:

### HTTP Request

`GET /v1/companies/{companyId}/applications/{jobApplicationId}`

### Query Parameters

| Query Parameter | Description                                                                                                                       |
|:----------------|:----------------------------------------------------------------------------------------------------------------------------------|
| fields          | See [Fields](#customizing-response-fields) documentation.                                                                         |
| expand          | See [Resource Expansion](#links-and-resource-expansion) documentation. Expandable fields are: applicant, referrer, job, referrals |

## Get Feedback of a Job Application

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/referrals",
  "items": [
    {
      "id": "b93bb536-c964-4e11-9d30-11da0c362e09",
      "user": {
        "id": "dddddddd-dddd-dddd-dddd-dddddddddddd",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/dddddddd-dddd-dddd-dddd-dddddddddddd"
      },
      "referralType": "REFERRAL",
      "connection": "John Does is a former coworker",
      "reason": "I highly recommend this candidate"
    }
  ]
}
```

This is the feedback of the Talent Scout who shared/referred this candidate. Feedback can have different types whether the Talent Scout wants to support the applicant or not:

| Type     | Description                                                                           |
|:---------|:--------------------------------------------------------------------------------------|
| REFERRAL | The Talent Scout supports the Applicant and refers him for the position he applied on |
| NEUTRAL  | The Talent Scout doesn’t want to give either negative or positive feedback            |
| NEGATIVE | The Talent Scout doesn’t think that the candidate is a good fit for the postition     |

### HTTP Request
`GET /v1/companies/{companyId}/applications/{jobApplicationId}/referrals`
