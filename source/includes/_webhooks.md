# Webhooks
Use webhooks to be notified about events that happen in a Firstbird account.


## Webhook terminology
An event is an account occurrence, such as a new job application being received, a referral added, or an applicant being hired. Each occurrence has a corresponding event object.
Webhook endpoints are URLs defined by users to which Firstbird sends events. A single event may be sent to many webhook endpoints.
Webhooks refers to the overall concept of sending notifications to webhook endpoints.

--

##Why using webhooks
Interacting with a third-party API like Firstbird's can introduce two problems:
* Services not directly responsible for making an API request may still need to know the response of that request
* Some events, like job application received and referral added events, are not the result of a direct API request

Webhooks solve these problems by letting you register a URL that we will notify anytime an event happens in your account. 
When the event occurs—for example, when a job application was received, Firstbird creates an event object. This object contains all the relevant information about what just happened, including the type of event and the data associated with that event. Firstbird then sends the event object to any URLs in your account's webhooks settings via an HTTP(s) POST request. 

You might use webhooks as the basis to:
* Send new e-emails to applicants on specific events
* Forward the job application to your ATS
* Integrate your hole hiring process with Firstbird

## Configuring Webhooks
Webhooks can be configured as a Company Administrator within the Integration tab of the `Account Preferences`. For a single webhook destination you have to configure your callback URL, which can be either HTTP or HTTPS.
You can decide fo yourself which of the available events should be sent to which webhook destination.

![webhooks settings](images/webhooks_screenshot.png)

## Webhooks Structure

```json
[
  {
    "type" : "entity.event_name",
    "event" : {

    }
  }
]
```

Our webhooks are sent as `JSON` data with `POST` requests to your configured URL. To allow batching of webhooks we send them as arrays which can
contain multiple event envelopes, containing the type of the event and the payload.

## Acknowledge webhooks
Following HTTP response status values are considered as success: `2XX`, `3XX`. If your configured URL returns any of this status values, Firstbird considers this
webhook as successfully delivered.

If the request to your configured URL returns with a status of `4XX` or `5XX` we will consider that as a failure (e.g. your receiving server has been unavailable) and
are going to retry the delivery for 24 hours which exponential increasing intervals between the retries.

## Security Considerations
As our webhooks don't provide authentication mechanisms, you shouldn't take the values contained in the requests as granted. It is
considered a good practice to request the contained values by their reference id (e.g. job_application.received contains the job application id
which allows you to request the referenced job application via our REST API)

## Available Events

> job_application.received by link or referral

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "applicant_id" : "00000000-0000-0000-0000-000000000000",
  "referrer_id" : "00000000-0000-0000-0000-000000000000",
  "job_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "type" : "link or referral"
}
```

> job_application.received by share

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "applicant_id" : "00000000-0000-0000-0000-000000000000",
  "referrer_id" : "00000000-0000-0000-0000-000000000000",
  "share_id" : "00000000-0000-0000-0000-000000000000",
  "job_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "type" : "share"
}
```

> job_application.received from user

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "applicant_id" : "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "share_id" : "00000000-0000-0000-0000-000000000000",
  "job_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "type" : "user"
}
```

> job_application.deleted from user

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z"
}
```

> job_application.rated from user

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "initial" : "true",
  "rating" : "A, B or C"
}
```

> job_application.closed from user

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "close_reason" : "CANDIDATE_KNOWN"
}
```

> job_application.hired from user

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "pay_reward" : "true",
  "first_day_of_work" : "2020-01-01"
}
```

> job_application.referral_added from user

```json
{
  "job_application_id": "00000000-0000-0000-0000-000000000000",
  "company_id": "00000000-0000-0000-0000-000000000000",
  "user_id" : "00000000-0000-0000-0000-000000000000",
  "date_time" : "1970-01-01 12:00:00.000Z",
  "referral_id" : "00000000-0000-0000-0000-000000000000",
  "connection" : "Former coworker!",
  "reason" : "Great employee!",
  "referral_type" : "NEUTRAL, POSITIVE or NEGATIVE"
}
```

| type                           | Description                                                                                             |
|:-------------------------------|:--------------------------------------------------------------------------------------------------------|
| job_application.received       | A job application has been created inside Firstbird. The type fields indicates how it has been created. |
| job_application.edited         | One of your recruiters edited a job application                                                         |
| job_application.deleted        | One of your recruiters deleted a job application                                                        |
| job_application.rated          | One of your recruiters rated a job application                                                          |
| job_application.closed         | One of your recruiters closed a job application                                                         |
| job_application.hired          | One of your recruiters hired the applicant                                                              |
| job_application.referral_added | The talent scout via whom the job application has been received provided feedback.                      |
