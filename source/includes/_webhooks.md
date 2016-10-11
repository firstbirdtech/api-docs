# Webhooks

We at firstbird think that the internet should be event driven, and so should be your employee referral program.
Webhooks provide an easy way to react to things that happened within your firstbird account.

Whether a new job application has been received or a talent scout provided feedback for a candidate, you may want to
connect other systems to your firstbird data without the annoying polling of REST resources. Webhooks provide a convenient way to register
any public available URL as a callback within firstbird.

## Configuring Webhooks
Webhooks can be configured as a company admin within the account settings. For a single webhook destination you have to configure your callback URL, which can be either HTTP or HTTPS.
You can decide yourself which of the available events should be sent to which webhook destination.

![webhooks settings](images/webhooks_screenshot.png)

## Webhooks Structure
Our webhooks are sent as JSON data with POST requests to your configured URL. To allow batching of webhooks we send them as arrays which can
contain multiple event envelopes, containing the type of the event and the payload.

```json
[
  {
    "type" : "entity.event_name",
    "event" : {

    }
  }
]
```

## Acknowledge webhooks

Following HTTP response status values are considered as success: `2XX`, `3XX`. If your configured URL returns any of this status values, firstbird considers this
webhooks as successfully delivered.

If the request to your configured URL returns with a status of `4XX` or `5XX` we will consider that as a failure (e.g. your receiving server has been unavailable) and
are going to retry the delivery for 24 hours which exponential increasing intervals between the retries.

## Security Considerations
As our webhooks don't provide authentication mechanisms, you shouldn't take the values contained in the requests as granted. It is
considered a good practice to request the contained values by their reference id (e.g. job_application.received contains the job application id
which allows you to request the referenced job application via our REST API)
