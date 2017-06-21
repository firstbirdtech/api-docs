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
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005",
      "id": "00000000-0000-0000-0000-000000000005",
      "company": {
        "id": "00000000-0000-0000-0000-000000000000",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
      },
      "location": {
        "id": "00000000-0000-0000-0000-000000000001",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/location/00000000-0000-0000-0000-000000000001"
      },
      "creationDate": "2016-03-22T09:57:21Z",
      "title": "Nr. 1 System Engineer/Administrator (m/w)",
      "referenceNumber": "123456",
      "department": {
        "id": "00000000-0000-0000-0000-000000000002",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/departments/00000000-0000-0000-0000-000000000002"
      },
      "contactPerson": {
        "id": "00000000-0000-0000-0000-000000000003",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000003"
      },
      "reward": {
        "id": "00000000-0000-0000-0000-000000000004",
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewards/00000000-0000-0000-0000-000000000004"
      },
      "responsiblePersons": [
        {
          "id": "00000000-0000-0000-0000-000000000005",
          "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000006"
        }
      ],
      "description": "<h1>This is a description</h1>",
      "status": "ACTIVE_PUBLISHED",
      "hot": false,
      "image": {
        "href": "https://aws.com/eu-central-1/job-headers/2160x705/00000000-0000-0000-0000-000000000007.jpeg"
      },
      "statistics": {
        "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005/statistics"
      },
      "shareLink": {
        "href": "https://api.1brd.com/job/00000000-0000-0000-0000-000000000005?referrer=dddddddd-dddd-dddd-dddd-dddddddddddd"
      },
      "jobBranding": {
          "id": "00000000-0000-0000-0000-000000000007",
          "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/job_brandings/00000000-0000-0000-0000-000000000008"
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
| hot             | Show Hot Jobs only                                                         |
| referenceNumber | Filter by reference number                                                 |
| query           | Filter by job title                                                        |
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
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005",
  "id": "00000000-0000-0000-0000-000000000005",
  "company": {
    "id": "00000000-0000-0000-0000-000000000000",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
  },
  "location": {
    "id": "00000000-0000-0000-0000-000000000001",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/location/00000000-0000-0000-0000-000000000001"
  },
  "creationDate": "2016-03-22T09:57:21Z",
  "title": "Nr. 1 System Engineer/Administrator (m/w)",
  "referenceNumber": "123456",
  "department": {
    "id": "00000000-0000-0000-0000-000000000002",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/departments/00000000-0000-0000-0000-000000000002"
  },
  "contactPerson": {
    "id": "00000000-0000-0000-0000-000000000003",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000003"
  },
  "reward": {
    "id": "00000000-0000-0000-0000-000000000004",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/rewards/00000000-0000-0000-0000-000000000004"
  },
  "responsiblePersons": [
    {
      "id": "00000000-0000-0000-0000-000000000005",
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000006"
    }
  ],
  "description": "<h1>This is a description</h1>",
  "status": "ACTIVE_PUBLISHED",
  "hot": false,
  "image": {
    "href": "https://aws.com/eu-central-1/job-headers/2160x705/00000000-0000-0000-0000-000000000007.jpeg"
  },
  "statistics": {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/jobs/00000000-0000-0000-0000-000000000005/statistics"
  },
  "shareLink": {
    "href": "https://api.1brd.com/job/00000000-0000-0000-0000-000000000005?referrer=dddddddd-dddd-dddd-dddd-dddddddddddd"
  },
  "jobBranding": {
      "id": "00000000-0000-0000-0000-000000000007",
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/job_brandings/00000000-0000-0000-0000-000000000008"
  }
}
```

`GET /v1/companies/{companyId}/jobs/{jobId}`

### Query Parameters

| Query Parameter | Description                                                                                                                            |
|:----------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| fields          | See [Fields](#customizing-response-fields) documentation.                                                                              |
| expand          | See [Resource Expansion](#links-and-resource-expansion) documentation. Available are: `company`, `location`, `department` and `reward` |

### Response fields

| Field name         | Required | Description                                                                                        |
|:-------------------|:---------|----------------------------------------------------------------------------------------------------|
| href               | Yes      | The link to this job.                                                                              |
| id                 | Yes      | The id of this job.                                                                                |
| company            | Yes      | The company this job belongs to.                                                                   |
| location           | Yes      | The location that has been assigned.                                                               |
| creationDate       | Yes      | The creation date.                                                                                 |
| title              | Yes      | The job title.                                                                                     |
| referenceNumber    | No       | The reference number. (Not present, if no reference number entered)                                |
| department         | Yes      | The department that has been assigned.                                                             |
| contactPerson      | Yes      | The contact person.                                                                                |
| reward             | Yes      | The reward that has been assigned.                                                                 |
| responsiblePersons | No       | The responsible persons that have been assigned. (Not present, if no responsible persons assigned) |
| description        | Yes      | The job description.                                                                               |
| status             | Yes      | The status of the job.                                                                             |
| hot                | Yes      | Whether the job is a hot job or not.                                                               |
| image              | Yes      | The job header image.                                                                              |
| statistics         | Yes      | The statistics of this job.                                                                        |
| shareLink          | Yes      | The sharing link of this job.                                                                      |
| jobBranding        | No       | The branding that has been assigned. (Not present, if no branding assigned)                        |

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

| Property           | Description                                                                                                                 |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------|
| department         | The Id of the Department this Job is associated with                                                                        |
| contactPerson      | The Id of the Recruiter who is responsible for this Job                                                                     |
| description        | HTMl describing the Job. Please consider the //TODO HTML documentation to know about allowed HTML tags etc.                 |
| endDate            | The date when the job will be automatically closed once it is in status ACTIVE_PUBLISHED. Can be null to avoid autoclosing. |
| hot                | The Hot flag                                                                                                                |
| location           | The Location of your Company the Job is associated with                                                                     |
| referenceNumber    | This field allows to enter reference numbers of external systems                                                            |
| reward             | The Reward that will be payed as soon as an Applicant gets hired for that Job                                               |
| title              | The title of the Job. This field is limited to 255 characters                                                               |
| responsiblePersons | An array of objects containing the User Ids of Recruiters being responsible for this Job as well                            |

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
