# Job Applications

Job Applications are the other main pillar of your Account at Firstbird.

Job Applications can have following statuses:

| Status      | Description                                                                           |
|:------------|:--------------------------------------------------------------------------------------|
| IN_PROGRESS | This Job Application is currently in progress and waits for your Recruiters decisions |
| HIRED       | The candidate of this Job Application got hired                                       |
| CLOSED      | The Job Application has been withdrawn by your Recruiters                             |

Your Recruiters can give a Job Application different ratings:

| Rating | Description                                                             |
|:-------|:------------------------------------------------------------------------|
| A      | The A rating corresponds to the 3-star rating from the web applications |
| B      | The B rating corresponds to the 2-star rating from the web applications |
| C      | The C rating corresponds to the 1-star rating from the web applications |

In case of a closed Job Application, one of the following reasons must be provided:

| Reason              | Description                                                                       |
|:--------------------|:----------------------------------------------------------------------------------|
| CANDIDATE_KNOWN     | This Applicant was already being considered by the company prior to this referral |
| CANDIDATE_REJECTED  | This Applicant was reject for this position                                       |
| CANDIDATE_WITHDRAWN | This Applicant withdrew is application                                            |
| CANDIDATE_EVIDENCE  | This Applicant was not selected, but might be a good in the future                |
| APPLICATION_INVALID | The application is not valid                                                      |

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
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/00000000-0000-0000-0000-000000000001",
      "id": "00000000-0000-0000-0000-000000000001",
      "status": "IN_PROGRESS",
      "applicationDate": "2016-03-23T08:37:15Z",
      "company": {
        "id": "00000000-0000-0000-0000-000000000000",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
      },
      "applicant": {
        "id": "1d029da5-0a39-45d2-a26a-eb14a5d05d36",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applicants/00000000-0000-0000-0000-000000000002"
      },
      "referrer": {
        "id": "dddddddd-dddd-dddd-dddd-dddddddddddd",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/dddddddd-dddd-dddd-dddd-dddddddddddd"
      },
      "share": {
        "id": "00000000-0000-0000-0000-000000000004",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000003/shares/00000000-0000-0000-0000-000000000004"
      },
      "job": {
        "id": "00000000-0000-0000-0000-000000000003",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000003"
      },
      "referrals": {
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/00000000-0000-0000-0000-000000000001/referrals"
      },
      "files": [
        {
          "id": "00000000-0000-0000-0000-000000000006",
          "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/00000000-0000-0000-0000-000000000005/files/00000000-0000-0000-0000-000000000006"
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
| sort            | See [Sorting](#sorting) documentation                                                                                             |

## Get a Single Job Application

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/00000000-0000-0000-0000-000000000001",
  "id": "00000000-0000-0000-0000-000000000001",
  "status": "IN_PROGRESS",
  "applicationDate": "2016-03-23T08:37:15Z",
  "company": {
    "id": "00000000-0000-0000-0000-000000000000",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
  },
  "applicant": {
    "id": "1d029da5-0a39-45d2-a26a-eb14a5d05d36",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applicants/00000000-0000-0000-0000-000000000002"
  },
  "referrer": {
    "id": "dddddddd-dddd-dddd-dddd-dddddddddddd",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/dddddddd-dddd-dddd-dddd-dddddddddddd"
  },
  "share": {
    "id": "00000000-0000-0000-0000-000000000004",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000003/shares/00000000-0000-0000-0000-000000000004"
  },
  "job": {
    "id": "00000000-0000-0000-0000-000000000003",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000003"
  },
  "referrals": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/00000000-0000-0000-0000-000000000001/referrals"
  },
  "files": [
    {
      "id": "00000000-0000-0000-0000-000000000006",
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/00000000-0000-0000-0000-000000000005/files/00000000-0000-0000-0000-000000000006"
    }
  ],
  "applicantImage": {
    "href": "https://s3.eu-central-1.amazonaws.com/hummingbird-development/applicantimg/150x150/b642441c-2dc4-4cd1-8873-c5d7e2e725f2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20160323T083722Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Credential=AKIAJX7FDXXZDKC4NZVA%2F20160323%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Signature=06981e7b0b46d4d43cd407bd2848391a01195714f6ce0df2a8cb67358efaa598"
  },
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

### Response Fields

| Field name      | Required | Description                                                                                              |
|:----------------|:---------|:---------------------------------------------------------------------------------------------------------|
| href            | Yes      | The link to this job application.                                                                        |
| id              | Yes      | The id to this job application.                                                                          |
| status          | Yes      | The status.                                                                                              |
| applicationDate | Yes      | The date of the application.                                                                             |
| company         | Yes      | The company this job application belongs to.                                                             |
| applicant       | Yes      | The applicant.                                                                                           |
| referrer        | Yes      | The referrer.                                                                                            |
| share           | No       | The related share of this job application. (Not present, if the application didn't come through a share) |
| job             | Yes      | The job this job application belongs to.                                                                 |
| referrals       | Yes      | The referrals of this job application.                                                                   |
| files           | No       | The attached files. (Not present, if no files provided by the applicant).                                |
| applicantImage  | No       | The applicant's image. (Not present, if no applicant image provided by the applicant).                   |
| rewardPaid      | Yes      | Whether a reward has been paid or not.                                                                   |

## Get Attachment file of a Job Application

> The file information request returns JSON structured like this:

```json
{
  "id": "a3beb15a-84ac-4646-a20b-7aa5faf982a7",
  "name": "my_application.pdf",
  "contentType": "application/pdf",
  "size": "100000",
  "url": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/files/a3beb15a-84ac-4646-a20b-7aa5faf982a7/url"
}
```

> The file URL request returns JSON structured like this:

```json
{
  "url": "https://s3-eu-central-1.amazonaws.com/hummingbird-development/files/775845ca-5837-4f65-9a4f-658d22f12622?response-content-disposition=inline%3B%20filename%3Dtest.pdf&response-content-type=application%2Fpdf&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20170327T124130Z&X-Amz-SignedHeaders=host&X-Amz-Expires=15&X-Amz-Credential=AKIAJRDHPR2ZNVGR6XRQ%2F20170327%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Signature=6e3bdd82aa17d13af791c73314ab1accba5dc00644bbdd5670aacc66bbc88309"
}
```

First, you have to get basic information of job application file by issuing a [File Information](#file-information) request.

The response contains a `url` property where you can request the actual file URL. You can do this by issuing a [File URL](#file-url) request.
This will return the URL to the actual file. Be aware, that the URL is valid for 15 seconds only.

### HTTP Requests

#### File Information
`GET /v1/companies/{companyId}/applications/{jobApplicationId}/files/{fileId}`

#### File URL
`GET /v1/companies/{companyId}/applications/{jobApplicationId}/files/{fileId}/url`


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


## Rate a Job Application

> This is an example request body

```json
{
  "value": "A",
  "message": "Test"
}
```

In order to rate a Job Application you have to use the following request

### HTTP Request

`PUT /v1/companies/{companyId}/applications/{jobApplicationId}/rating`

### Parameters

| Property | Description                                                                                                       |
|:---------|:------------------------------------------------------------------------------------------------------------------|
| value    | Rating value as described in the [Job Application's rating table](#job-applications)                              |
| message  | Optional field, containing a message that the Recruiter may wish to send to the Referrer regarding this Applicant |


## Hire a Job Application

> This is an example request body

```json
{
  "firstDayOfWork": "2017-01-01",
  "message": "This was a very good referral. The candidate is a great fit.",
  "payReward": true,
  "value": "HIRED"
}
```

In order to hire a Job Application you must change its status to HIRED using the following request

### HTTP Request

`PUT /v1/companies/{companyId}/applications/{jobApplicationId}/status`

### Parameters

| Property       | Description                                                                                                       |
|:---------------|:------------------------------------------------------------------------------------------------------------------|
| firstDayOfWork | First day of work for the Applicant. Date format: "yyyy-MM-dd"                                                    |
| message        | Optional field, containing a message that the Recruiter may wish to send to the Referrer regarding this Applicant |
| payReward      | Whether or not the reward should be given to the Referrer                                                         |
| value          | New Job Application status. In this case, 'HIRED'. [Check Job Application's Status table](#job-applications)      |


## Close a Job Application

> This is an example request body

```json
{
  "closeReason": "CANDIDATE_WITHDRAWN",
  "message": "test",
  "value": "CLOSED"
}
```

In order to close a Job Application you must change its status to CLOSED using the following request


### HTTP Request

`PUT /v1/companies/{companyId}/applications/{jobApplicationId}/status`

### Parameters

| Property    | Description                                                                                                       |
|:------------|:------------------------------------------------------------------------------------------------------------------|
| closeReason | Reason why this Job Application is being rejected. Check [Job Application's close reasons](#job-applications)     |
| message     | Optional field, containing a message that the Recruiter may wish to send to the Referrer regarding this Applicant |
| value       | New Job Application status. In this case, 'CLOSED'. [Check Job Application's Status table](#job-applications)     |


## Re-open a Job Application

> This is an example request body

```json
{
  "value": "IN_PROGRESS"
}
```

In order to re-open a closed Job Application you must change its status to IN_PROGRESS using the following request


### HTTP Request

`PUT /v1/companies/{companyId}/applications/{jobApplicationId}/status`

### Parameters

| Property | Description                                                                                                        |
|:---------|:-------------------------------------------------------------------------------------------------------------------|
| value    | New Job Application status. In this case, 'IN_PROGRESS'. [Check Job Application's Status table](#job-applications) |

## Delete a closed Job Applcation

In order to delete a closed or hired Job Application you must use the following request


### HTTP Request

`DELETE /v1/companies/{companyId}/applications/{jobApplicationId}`

If the request succeeds, the api will return a 200 response with no body.
