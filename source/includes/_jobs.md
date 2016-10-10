# Jobs

Jobs are one of the main pillars of Firstbird

Jobs can have different statuses:

| Status           | Description                                                                                                                                    |
|:-----------------|:-----------------------------------------------------------------------------------------------------------------------------------------------|
| DRAFT            | Those Jobs are only visible to Company Administrators and Recruiters before they get published to all Talent Scouts                            |
| ACTIVE_PUBLISHED | Those Jobs are visible to all Talent Scouts and can be shared and candidates can be referred for those Jobs                                    |
| ACTIVE_CLOSED    | Those Jobs are only visible to Recruiters and Company Administrators, candidates who got a shared link to that job before can’t apply anymore. |
| ARCHIVED         | Candidates can’t apply to those Jobs anymore                                                                                                   |
| DELETED          | Those jobs aren’t visible anymore                                                                                                              |
Jobs can also be flagged as **Hot** which means they are hard to achieve. Most of the time this flag is used for visual indication on the UI.

## Get All Jobs

To get a list of all your Jobs you have to issue following request:

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=0&limit=2147483647",
  "total": 1,
  "offset": 0,
  "limit": 2147483647,
  "first": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=0&limit=2147483647"
  },
  "last": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs?status=active_closed,active_published,archived,deleted,draft&offset=0&limit=2147483647"
  },
  "items": [
    {
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
      "id": "0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
      "company": {
        "id": "00000000-0000-0000-0000-000000000000",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
      },
      "location": {
        "id": "50c7be5d-3e2d-4e57-9394-87d5ffc7f50f",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/location/50c7be5d-3e2d-4e57-9394-87d5ffc7f50f"
      },
      "creationDate": "2016-03-22T09:57:21Z",
      "title": "Nr. 1 System Engineer/Administrator (m/w)",
      "referenceNumber": "123456",
      "department": {
        "id": "50018463-d804-46ae-90a7-8187a12e6540",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/departments/50018463-d804-46ae-90a7-8187a12e6540"
      },
      "contactPerson": {
        "id": "a9709b55-69b9-4400-a5a9-6101790ea6d6",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/a9709b55-69b9-4400-a5a9-6101790ea6d6"
      },
      "reward": {
        "id": "00000000-0000-0000-0000-000000000000",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewards/00000000-0000-0000-0000-000000000000"
      },
      "responsiblePersons": [
        {
          "id": "a9709b55-69b9-4400-a5a9-6101790ea6d6",
          "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/a9709b55-69b9-4400-a5a9-6101790ea6d6"
        }
      ],
      "description": "<h1>This is a description</h1>",
      "status": "ACTIVE_PUBLISHED",
      "hot": false,
      "image": {},
      "statistics": {
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a/statistics"
      },
      "shareLink": {
        "href": "http://1bird.1brd.lvh.me/job/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a?referrer=dddddddd-dddd-dddd-dddd-dddddddddddd"
      }
    }
  ]
}
```

`GET /v1/companies/{companyId}/jobs`

### Query Parameters

| Query Parameter | Description                                                                |
|:----------------|:---------------------------------------------------------------------------|
| status          | Comma separated list of statuses which should be included in the response. |
| endDateBefore   | Jobs where the endDate is before the given date. (e.g. 2017-01-05)         |
| department      | Comma separated list of Department Ids to filter after                     |
| location        | Comma separated list of Location Ids to filter after                       |
| contact         | Comma separated list of User Ids to filter the Job’s Contact Person after  |
| isHot           | Show Hot Jobs only                                                         |
| fields          | See [Fields](#customizing-response-fields) documentation                   |
| limit           | See [Pagination](#pagination) documentation                                |
| offset          | See [Pagination](#pagination) documentation                                |
| sort            | See [Sorting](#sorting) documentation                                      |

## Get a Single Job

To get a single Job by Id you have to use following request:

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
  "id": "0a3f98fa-ef4f-457f-abb9-0a052d6ced5a",
  "title": "Nr. 1 System Engineer/Administrator (m/w)"
}
```

`GET /v1/companies/{companyId}/jobs/{jobId}`

### Query Parameters

| Query Parameter | Description                                                                                                                            |
|:----------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| fields          | See [Fields](#customizing-response-fields) documentation.                                                                              |
| expand          | See [Resource Expansion](#links-and-resource-expansion) documentation. Available are: `company`, `location`, `department` and `reward` |

## Create a Job

> This is an example request body

```json
{
      "department": {
              "id": "50018463-d804-46ae-90a7-8187a12e6540"
      },
      "contactPerson": {
              "id": "a9709b55-69b9-4400-a5a9-6101790ea6d6"
      },
      "description": "<h1>This is HTML Description of a Job</h1><p></p>",
      "endDate": "2016-03-23",
      "hot": true,
      "location": {
              "id": "50c7be5d-3e2d-4e57-9394-87d5ffc7f50f"
      },
      "referenceNumber": "123456",
      "reward": {
              "id": "00000000-0000-0000-0000-000000000000"
      },
      "title": "Developer",
      "responsiblePersons": [{
              "id": "a9709b55-69b9-4400-a5a9-6101790ea6d6"
      }]
}
```

> This request returns JSON structured like this:

```json
{
  "id": "54d49fa7-97cb-4502-bb55-4217cb281b3f"
}
```

To create a new Job for your Company use following request

### HTTP Request

`POST /v1/companies/{companyId}/jobs`

### Parameters

| Property           | Description                                                                                                 |
|:-------------------|:------------------------------------------------------------------------------------------------------------|
| department         | The Id of the Department this Job is associated with                                                        |
| contactPerson      | The Id of the Recruiter who is responsible for this Job                                                     |
| description        | HTMl describing the Job. Please consider the //TODO HTML documentation to know about allowed HTML tags etc. |
| endDate            | The date when the job will be automatically closed once it is in status ACTIVE_PUBLISHED                    |
| hot                | The Hot flag                                                                                                |
| location           | The Location of your Company the Job is associated with                                                     |
| referenceNumber    | This field allows to enter reference numbers of external systems                                            |
| reward             | The Reward that will be payed as soon as an Applicant gets hired for that Job                               |
| title              | The title of the Job. This field is limited to 255 characters                                               |
| responsiblePersons | An array of objects containing the User Ids of Recruiters being responsible for this Job as well            |

## Update a Job

> This is an example request body

```json
{
      "department": {
              "id": "50018463-d804-46ae-90a7-8187a12e6540"
      },
      "contactPerson": {
              "id": "a9709b55-69b9-4400-a5a9-6101790ea6d6"
      },
      "description": "<h1>This is HTML Description of a Job</h1><p></p>",
      "endDate": "2016-03-23",
      "hot": true,
      "location": {
              "id": "50c7be5d-3e2d-4e57-9394-87d5ffc7f50f"
      },
      "referenceNumber": "123456",
      "reward": {
              "id": "00000000-0000-0000-0000-000000000000"
      },
      "title": "Developer",
      "responsiblePersons": [{
              "id": "a9709b55-69b9-4400-a5a9-6101790ea6d6"
      }]
}
```

After creating a Job you maybe want to change some fields. All fields used during Job creation can be updated with following request

### HTTP Request

`PUT /v1/companies/{companyId}/jobs/{jobId}`

## Update a Jobs Status

> This is an example request body

```json
{
  "value":"ACTIVE_PUBLISHED"
}
```

To change the status of a Job you need following request. Please keep in mind that not all status transitions are allowed.

![status transitions](images/fsm_job_life_cycle.png)

### HTTP Request

`PUT /v1/companies/{companyId}/jobs/{jobId}/status`

### Parameters

| Property | Description                                                                                                                        |
|:---------|:-----------------------------------------------------------------------------------------------------------------------------------|
| status   | New status of a the Job. Possible values are: ACTIVE_PUBLISHED, ACTIVE_CLOSED, ARCHIVED (you can’t set DRAFT and DELETED directly) |

## Delete a Job

After a while you may want to delete a Job because it is outdated to do so use following request:

### HTTP Request

`DELETE /v1/companies/{companyId}/jobs/{jobId}`
