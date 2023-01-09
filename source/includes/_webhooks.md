# Webhooks
Use webhooks to be notified about events that happen in the Employee Referrals system.


##Webhook terminology
An event is an account occurrence, such as a new job application being received, a referral added, or an applicant being hired. Each occurrence has a corresponding event object.
Webhook endpoints are URLs defined by users to which the Employee Referrals system sends events. A single event may be sent to many webhook endpoints.
Webhooks refers to the overall concept of sending notifications to webhook endpoints.

--

##Why using webhooks
Interacting with a third-party API like Employee Referrals' can introduce two problems:

* Services not directly responsible for making an API request may still need to know the response of that request
* Some events, like job application received and referral added events, are not the result of a direct API request

Webhooks solve these problems by letting you register a URL that we will notify anytime an event happens in your account.
When the event occurs—for example, when a job application was received, the Employee Referrals system creates an event object. This object contains all the relevant information about what just happened, including the type of event and the data associated with that event. The Employee Referrals system then sends the event object to any URLs in your account's webhooks settings via an HTTP(s) POST request.

You might use webhooks as the basis to:

* Send new e-mails to applicants on specific events
* Forward the job application to your ATS
* Integrate your whole hiring process with Radancy's Employee Referrals

##Configuring Webhooks
Webhooks can be configured as a Company Administrator within the Integration tab of the `Account Preferences`. For a single webhook destination you have to configure your callback URL, which can be either HTTP or HTTPS.
You can decide yourself which of the available events should be sent to which webhook destination.

![webhooks settings](images/webhooks_screenshot.png)

## Webhooks Structure

```json
[
  {
    "event_name": "entity.event_name",
    "event": {

    }
  }
]
```

Our webhooks are sent as `JSON` data with `POST` requests to your configured URL. To allow batching of webhooks we send them as arrays which can
contain multiple event envelopes, containing the type of the event and the payload.

## Acknowledge webhooks
Following HTTP response status values are considered as success: `2XX`, `3XX`. If your configured URL returns any of this status values, the Employee Referrals system considers this webhook as successfully delivered.

If the request to your configured URL returns with a status of `4XX` or `5XX` we will consider that as a failure (e.g. your receiving server has been unavailable) and
are going to retry the delivery for 24 hours which exponential increasing intervals between the retries.

## Security Considerations
As our webhooks don't provide authentication mechanisms, you shouldn't take the values contained in the requests as granted. It is considered a good practice to request the contained values by their reference id (e.g. job_application.received contains the job application id which allows you to request the referenced job application via our REST API)

You can restrict the webhooks to only accept them from our IPs: 52.57.76.133, 52.57.83.207.

## Available Events

> job_application.received by link or referral

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A, B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED",
      "applicant_image": "http://example.com/applicant_image.png",
      "attachments": [
          "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/files/a3beb15a-84ac-4646-a20b-7aa5faf982a7"
      ]
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "applicant": {
      "id": "00000000-0000-0000-0000-000000000000",
      "first_name": "Test",
      "last_name": "User",
      "email": "test.user@radancy.com",
      "phone_number": "123456789"
  },
  "referrer": {
      "id": "00000000-0000-0000-0000-000000000000",
      "company_id": "00000000-0000-0000-0000-000000000000",
      "first_name": "Test",
      "last_name": "User",
      "email": "test.user@radancy.com",
      "locale": "en_US",
      "main_role": "ROLE_TALENT_SCOUT",
      "location_id": "00000000-0000-0000-0000-000000000000",
      "department_id": "00000000-0000-0000-0000-000000000000",
      "status": "ACTIVE or INACTIVE",
      "incognito": false,
      "time_zone": "Europe/Vienna"
  },
  "job": {
      "id": "00000000-0000-0000-0000-000000000000",
      "company_id": "00000000-0000-0000-0000-000000000000",
      "location_id": "00000000-0000-0000-0000-000000000000",
      "contact_person_id": "00000000-0000-0000-0000-000000000000",
      "reward_id": "00000000-0000-0000-0000-000000000000",
      "department_id": "00000000-0000-0000-0000-000000000000",
      "reference_number": "ref-no",
      "title": "Developer",
      "description": "Java Backend Dev",
      "end_date": "1970-01-01 12:00:00.000Z",
      "status": "DRAFT, ACTIVE_PUBLISHED, ACTIVE_CLOSED, ARCHIVED or DELETED",
      "hot": true,
      "responsible_persons": [
          "00000000-0000-0000-0000-000000000000",
          "00000000-0000-0000-0000-000000000000"
      ],
      "creation_date": "1970-01-01 12:00:00.000Z"
  },
  "date_time": "1970-01-01 12:00:00.000Z",
  "type": "link or referral"
}
```

> job_application.received by share

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A, B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED",
      "applicant_image": "http://example.com/applicant_image.png",
      "attachments": [
          "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/files/a3beb15a-84ac-4646-a20b-7aa5faf982a7"
      ]
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "applicant" : {
      "id": "00000000-0000-0000-0000-000000000000",
      "first_name": "Test",
      "last_name": "User",
      "email": "test.user@radancy.com",
      "phone_number": "123456789"
  },
  "referrer": {
      "id": "00000000-0000-0000-0000-000000000000",
      "company_id": "00000000-0000-0000-0000-000000000000",
      "first_name": "Test",
      "last_name": "User",
      "email": "test.user@radancy.com",
      "locale": "en_US",
      "main_role": "ROLE_TALENT_SCOUT",
      "location_id": "00000000-0000-0000-0000-000000000000",
      "department_id": "00000000-0000-0000-0000-000000000000",
      "status": "ACTIVE or INACTIVE",
      "incognito": false,
      "time_zone": "Europe/Vienna"
  },
  "share_id": "00000000-0000-0000-0000-000000000000",
  "job": {
      "id": "00000000-0000-0000-0000-000000000000",
      "company_id": "00000000-0000-0000-0000-000000000000",
      "location_id": "00000000-0000-0000-0000-000000000000",
      "contact_person_id": "00000000-0000-0000-0000-000000000000",
      "reward_id": "00000000-0000-0000-0000-000000000000",
      "department_id": "00000000-0000-0000-0000-000000000000",
      "reference_number": "ref-no",
      "title": "Developer",
      "description": "Java Backend Dev",
      "end_date": "1970-01-01 12:00:00.000Z",
      "status": "DRAFT, ACTIVE_PUBLISHED, ACTIVE_CLOSED, ARCHIVED or DELETED",
      "hot": true,
      "responsible_persons": [
          "00000000-0000-0000-0000-000000000000",
          "00000000-0000-0000-0000-000000000000"
      ],
      "creation_date": "1970-01-01 12:00:00.000Z"
  },
  "date_time" : "1970-01-01 12:00:00.000Z",
  "type" : "share"
}
```

> job_application.received from user

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A, B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED",
      "applicant_image": "http://example.com/applicant_image.png",
      "attachments": [
          "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/applications/d648096f-c3f4-4121-af9a-5377753e467e/files/a3beb15a-84ac-4646-a20b-7aa5faf982a7"
      ]
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "applicant": {
      "id": "00000000-0000-0000-0000-000000000000",
      "first_name": "Test",
      "last_name": "User",
      "email": "test.user@radancy.com",
      "phone_number": "123456789"
  },
  "user": {
      "id": "00000000-0000-0000-0000-000000000000",
      "company_id": "00000000-0000-0000-0000-000000000000",
      "first_name": "Test",
      "last_name": "User",
      "email": "test.user@radancy.com",
      "locale": "en_US",
      "main_role": "ROLE_TALENT_SCOUT",
      "location_id": "00000000-0000-0000-0000-000000000000",
      "department_id": "00000000-0000-0000-0000-000000000000",
      "status": "ACTIVE or INACTIVE",
      "incognito": false,
      "time_zone": "Europe/Vienna"
  },
  "share_id": "00000000-0000-0000-0000-000000000000",
  "job": {
      "id": "00000000-0000-0000-0000-000000000000",
      "company_id": "00000000-0000-0000-0000-000000000000",
      "location_id": "00000000-0000-0000-0000-000000000000",
      "contact_person_id": "00000000-0000-0000-0000-000000000000",
      "reward_id": "00000000-0000-0000-0000-000000000000",
      "department_id": "00000000-0000-0000-0000-000000000000",
      "reference_number": "ref-no",
      "title": "Developer",
      "description": "Java Backend Dev",
      "end_date": "1970-01-01 12:00:00.000Z",
      "status": "DRAFT, ACTIVE_PUBLISHED, ACTIVE_CLOSED, ARCHIVED or DELETED",
      "hot": true,
      "responsible_persons": [
          "00000000-0000-0000-0000-000000000000",
          "00000000-0000-0000-0000-000000000000"
      ],
      "creation_date": "1970-01-01 12:00:00.000Z"
  },
  "date_time": "1970-01-01 12:00:00.000Z",
  "type": "application"
}
```

> job_application.deleted from user

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A,B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED"
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id": "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z"
}
```

> job_application.rated from user

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A, B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED"
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id": "00000000-0000-0000-0000-000000000000",
  "date_time": "1970-01-01 12:00:00.000Z",
  "initial": true,
  "rating": "A, B or C"
}
```

> job_application.closed from user

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A, B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED"
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id": "00000000-0000-0000-0000-000000000000",
  "date_time": "1970-01-01 12:00:00.000Z",
  "close_reason": "CANDIDATE_KNOWN"
}
```

> job_application.hired from user

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A, B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED"
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "pay_reward" : true,
  "first_day_of_work" : "2020-01-01"
}
```

> job_application.referral_added from user

```json
{
  "job_application": {
      "id": "00000000-0000-0000-0000-000000000000",
      "job_id": "00000000-0000-0000-0000-000000000000",
      "rating": "A, B or C",
      "created_by_user_id": "00000000-0000-0000-0000-000000000000",
      "status": "IN_PROGRESS, HIRED or CLOSED"
  },
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "referral_id" : "00000000-0000-0000-0000-000000000000",
  "connection" : "Former coworker!",
  "reason" : "Great employee!",
  "referral_type" : "NEUTRAL, POSITIVE or NEGATIVE"
}
```

> reward.approved

```json
{
    "reward": {
        "name": "250€ Amazon Gift Card",
        "value": "250",
        "currency": "EUR",
        "due_date": "2021-02-10",
        "company_id": "00000000-0000-0000-0000-000000000000",
        "id": "00000000-0000-0000-0000-000000000000"
    },
    "company_id": "00000000-0000-0000-0000-000000000000",
    "recipient": {
        "id": "00000000-0000-0000-0000-000000000000",
        "first_name": "Name",
        "last_name": "Last",
        "email": "email@email.com",
        "location": "Location",
        "department": "Department",
        "employee_id": "123"
    },
    "job": {
        "id": "00000000-0000-0000-0000-000000000000",
        "company_id": "00000000-0000-0000-0000-000000000000",
        "title": "Title"
    },
    "application": {
        "id": "00000000-0000-0000-0000-000000000000",
        "company_id": "00000000-0000-0000-0000-000000000000",
        "first_name": "Name",
        "last_name": "Last"
    },
    "approvedBy": {
        "id": "00000000-0000-0000-0000-000000000000",
        "company_id": "00000000-0000-0000-0000-000000000000",
        "first_name": "Name",
        "last_name": "Last"
    },
    "type": "reward.approved",
    "company": {
        "domain": "domain",
        "company_name": "ATS Forward",
        "street": "street",
        "postal_code": "1234",
        "city": "city"
    }
}
```

> points.gained

```json
{
    "user": {
        "id": "00000000-0000-0001-0000-000000000000",
        "first_name": "Test",
        "last_name": "User",
        "email": "test.user@radancy.com",
        "location": "Wien",
        "department": "IT",
        "employee_id": "1234"
    },
    "count": 1,
    "cause": "JOB_VIEWS",
    "company": {
        "id": "00000000-0000-0000-0000-000000000000",
        "domain": "test",
        "company_name": "test"
    },
    "type": "points.gained",
    "date_time": "0001-01-01T01:01:00.000+0139"
}
```

> points.revoked

```json
{
    "user": {
        "id": "00000000-0000-0001-0000-000000000000",
        "first_name": "Test",
        "last_name": "User",
        "email": "test.user@radancy.com",
        "location": "Wien",
        "department": "IT",
        "employee_id": "1234"
    },
    "count": 1,
    "cause": "JOB_APPLICATION_INVALID",
    "company": {
        "id": "00000000-0000-0000-0000-000000000000",
        "domain": "test",
        "company_name": "test"
    },
    "type": "points.revoked",
    "date_time": "0001-01-01T01:01:00.000+0139"
}
```

| type                           | Description                                                                                             |
| :----------------------------- | :------------------------------------------------------------------------------------------------------ |
| job_application.received       | A job application has been created inside Employee Referrals. The type fields indicates how it has been created. |
| job_application.edited         | One of your recruiters edited a job application                                                         |
| job_application.deleted        | One of your recruiters deleted a job application                                                        |
| job_application.rated          | One of your recruiters rated a job application                                                          |
| job_application.closed         | One of your recruiters closed a job application                                                         |
| job_application.hired          | One of your recruiters hired the applicant                                                              |
| job_application.referral_added | The talent scout via whom the job application has been received provided feedback.                      |
| reward.approved                | The hiring reward that was approved by a recruiter which a talent scout should receive.                 |
| points.gained                  | A user gained points for actions within Employee Referrals.                                                      |
| points.revoked                 | A user got points revoked that were gained earlier within Employee Referrals.                                    |

**Note for job_application.received events:**

* If the referrer/user of the job application got deleted, the `referrer` / `user` key is not present.
* If the applicant did not provide a picture, the `applicant_image` key is not present.
* To get a file from the `attachments` array, follow
[this](#get-attachment-file-of-a-job-application) documentation.

**Note for reward.approved event:**

* If the applicant of the job application got deleted the `application` / `first_name` and `application` / `last_name` keys are not present
* The `recipient` / `employee_id` key is optional as a user is not obliged to provide one.
* The `reward` / `currency` follows the ISO 4217 currency standard.
* The `reward` / `currency` has an exception to the above rule where the currency can be the value `COINS`. If this is the case the `reward` / `name` key is empty.
* The `company` / `street`, `company` / `city` and `company` / `postal_code` keys are optional as a company is not obliged to provide them.