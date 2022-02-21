# Candidate Experience Package

### Intro

With the introduction of our [Candidate Experience Package](https://www.firstbird.com/en/magazine/candidate-experience-package/) 
we have revised our referral form for candidates. It is now split into two steps. 
On the first step the candidate accepts the referral which only needs basic information. 
On the second step the candidate can now be forwarded to an external URL to complete the job application directly in the ATS.

### Requirement

The Candidate Experience Package has to be unlocked explicitly per Company Account on Firstbird side. The CEP is an add-on package.

## Job-Import with external URL

The endpoint of creating a job has an additional field **jobPostingUrl** to add the target URL

`POST /v1/companies/{companyId}/jobs`

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
      "jobBranding": {
               "id": "00000000-0000-0000-0000-000000000001"
      },
      "title": "Developer",
      "responsiblePersons": [{
              "id": "a9709b55-69b9-4400-a5a9-6101790ea6d6"
      }],
      "jobPostingUrl": "https://jobs.someurl.com/abc?source=Firstbird"
}
```

## Request basic referral information

Once a candidate has completed the first step the user is forwarded to the `jobPostingUrl`. 
A query parameter **referralId** is added to this URL which references the referral in Firstbird.
Note that the referralId is different from the applicationId.
This referralId can be used to request basic information the candidate has added to Firstbird. 

`GET /v1/companies/{companyId}/applications?sourceId={referralId}&expand=applicant`

### Move Accepted Referral to in Progress

In the background we besides a referral also create a job application. 
To update a status of a referral you actually need to accept the Terms and then  update the status of the job application. 
That means to move a Job Application from “Accepted Referral” to “In Progress” you need to

* get the jobApplicationId
* accept the legal terms via API
* update the Status of the job application

#### Endpoint to get the Job Application Id

`GET /v1/companies/{companyId}/applications?sourceId={referralId}&expand=applicant`

#### Endpoint to accept the legal terms

`PUT /v1/companies/{companyId}/applications/{applicationId}`

> This is an example request body

```json
{
  "firstName": "Maria",
  "lastName": "Finch",
  "email": "maria.finch1983@gmail.com",
  "acceptTerms": true
}
```

**Important to know**

All fields are mandatory. Changing a field will update the Job Application information on Firstbird side!

#### Endpoint to move the job application to "In Progress"

`PUT /v1/companies/{companyId}/applications/{applicationId}/status`

> This is an example request body

```json
{
  "value": "FINISHED"
}
```

The value finished means that the job application has been finished and therefore is moved to “In Progress”.

**Important to know**

Customers may have set the attachments to mandatory, which block the job application to be finished as it will complain about missing files. 
First disable the mandatory files in the Company Account Preferences!

