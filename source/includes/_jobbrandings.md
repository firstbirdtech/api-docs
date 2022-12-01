# Job Brandings

Job Brandings allow you to customize your jobs to make them stand out on social networks.

## Get All Job Brandings

This endpoint retrieves all Job Brandings that are configured for your company.

### HTTP Request

> This request returns JSON structured like this:

```json
[
  {
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/job_brandings/00000000-0000-0000-0000-000000000001",
    "id": "00000000-0000-0000-0000-000000000001",
    "company": {
      "id": "00000000-0000-0000-0000-000000000000",
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
    },
    "name": "Branding One",
    "isDefault": false,
    "shareLogo": {
      "id": "00000000-0000-0000-0000-0000000000002",
      "href": "https://localhost/share-logo-image.jpeg"
    },
    "shareLogoWide": {
      "id": "00000000-0000-0000-0000-0000000000003",
      "href": "https://localhost/share-logo-image-wide.jpeg"
    },
    "linkedInShareLogo": {
      "id": "00000000-0000-0000-0000-000000000004",
      "href": "https://localhost/linkedin-share-logo-image.jpeg"
    },
    "jobHeader": {
      "id": "00000000-0000-0000-0000-000000000005",
      "href": "https://localhost/job-header-image.jpeg"
    },
    "shareDescription": "This is my share description.",
    "createdAt": "2018-10-09T10:03:39Z",
    "updatedAt": "2018-10-09T10:04:38Z",
    "sharingTexts": {
      "email": {
        "en_US": "EmailSharingText"
      },
      "whatsapp": {
        "en_US": "WhatsAppSharingText"
      },
      "wechat": {
        "en_US": "WeChatSharingText"
      }
    },
    "jobHeaderColor": "#ffffff",
    "jobBackgroundColor": "#000000"
  }
]
```

`GET /v1/companies/{companyId}/job_brandings`

### Response Fields

| Property              | Required | Description                                                                                           |
|:----------------------|:---------|:------------------------------------------------------------------------------------------------------|
| href                  | Yes      | The link to this job branding.
| id                    | Yes      | The id of this job branding.
| company               | Yes      | The company this job branding is associated with.
| name                  | No       | The name of this job branding. Absent, if this is the default branding.
| isDefault             | Yes      | Whether this job branding is the default one or not.
| shareLogo             | Yes      | The share logo that will be used for this job branding.
| shareLogoWide         | No       | The wide share logo that will be used for this job branding by certain share channels.
| linkedInShareLogo     | Yes      | The share logo that will be used for this job branding on LinkedIn.
| jobHeader             | Yes      | The job header image that will be used for this job branding.
| shareDescription      | No       | The share description that will be used for this job branding.
| createdAt             | Yes      | The date time when this job branding got created. Absent, if this is the default branding.
| updatedAt             | No       | The date time when this job branding got updated. Absent, if this job branding has never been updated.
| sharingTexts          | Yes      | Text suggestions for when Talent Scouts share a job.
| jobHeaderColor        | No       | The page heading color for the companies job page.
| jobBackgroundColor    | No       | The page backgroud color for the companies job page.


**Note:** There will always be a default branding, if no job branding has been created.

## Get a Single Job Branding
To get a single Job Branding by it’s Id you have to use following request:

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000/job_brandings/00000000-0000-0000-0000-000000000001",
  "id": "00000000-0000-0000-0000-000000000001",
  "company": {
    "id": "00000000-0000-0000-0000-000000000000",
    "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000000"
  },
  "name": "Branding One",
  "isDefault": false,
  "shareLogo": {
    "id": "00000000-0000-0000-0000-0000000000002",
    "href": "https://localhost/share-logo-image.jpeg"
  },
  "shareLogoWide": {
    "id": "00000000-0000-0000-0000-0000000000003",
    "href": "https://localhost/share-logo-image-wide.jpeg"
  },
  "linkedInShareLogo": {
    "id": "00000000-0000-0000-0000-000000000004",
    "href": "https://localhost/linkedin-share-logo-image.jpeg"
  },
  "jobHeader": {
    "id": "00000000-0000-0000-0000-000000000005",
    "href": "https://localhost/job-header-image.jpeg"
  },
  "shareDescription": "This is my share description.",
  "createdAt": "2018-10-09T10:03:39Z",
  "updatedAt": "2018-10-09T10:04:38Z",
  "sharingTexts": {
    "email": {
      "en_US": "EmailSharingText"
    },
    "whatsapp": {
      "en_US": "WhatsAppSharingText"
    },
    "wechat": {
      "en_US": "WeChatSharingText"
    }
  },
  "jobHeaderColor": "#ffffff",
  "jobBackgroundColor": "#000000"
}
```

`GET /v1/companies/{companyId}/job_brandings/{jobBrandingId}`

### Response Fields

| Property              | Required | Description                                                                                           |
|:----------------------|:---------|:------------------------------------------------------------------------------------------------------|
| href                  | Yes      | The link to this job branding.
| id                    | Yes      | The id of this job branding.
| company               | Yes      | The company this job branding is associated with.
| name                  | No       | The name of this job branding. Absent, if this is the default branding.
| isDefault             | Yes      | Whether this job branding is the default one or not.
| shareLogo             | Yes      | The share logo that will be used for this job branding.
| shareLogoWide         | No       | The wide share logo that will be used for this job branding by certain share channels.
| linkedInShareLogo     | Yes      | The share logo that will be used for this job branding on LinkedIn.
| jobHeader             | Yes      | The job header image that will be used for this job branding.
| shareDescription      | No       | The share description that will be used for this job branding.
| createdAt             | Yes      | The date time when this job branding got created. Absent, if this is the default branding.
| updatedAt             | No       | The date time when this job branding got updated. Absent, if this job branding has never been updated.
| sharingTexts          | Yes      | Text suggestions for when Talent Scouts share a job.
| jobHeaderColor        | No       | The page heading color for the companies job page.
| jobBackgroundColor    | No       | The page backgroud color for the companies job page.

## Create a Job Branding

To create a new Job Branding for your company use following request:

### HTTP Request

> This is an example request body

```json
{
  "name": "Branding One",
  "jobHeader": {
    "id": "00000000-0000-0000-0000-000000000001"
  },
  "shareLogo": {
    "id": "00000000-0000-0000-0000-000000000002"
  },
  "shareLogoWide": {
    "id": "00000000-0000-0000-0000-000000000003"
  },
  "shareDescription": "This is my share description.",
  "sharingTexts": {
    "email": {
        "en_US": "EmailSharingText"
    },
    "whatsapp": {
        "en_US": "WhatsAppSharingText"
    },
    "wechat": {
        "en_US": "WeChatSharingText"
    }
  },
  "jobHeaderColor": "#ffffff",
  "jobBackgroundColor": "#000000"
}
```

> This request returns JSON structured like this:

```json
{
    "id": "00000000-0000-0000-0000-000000000010",
    "company": {
      "id": "00000000-0000-0000-0000-000000000011",
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000011"
    },
    "name": "Branding One",
    "isDefault": false,
    "jobHeader": {
      "id": "00000000-0000-0000-0000-000000000001",
      "href": "https://localhost/job-header-image.jpeg"
    },
    "shareLogo": {
      "id": "00000000-0000-0000-0000-000000000002",
      "href": "https://localhost/share-logo-image.jpeg"
    },
    "shareLogoWide": {
      "id": "00000000-0000-0000-0000-000000000003",
      "href": "https://localhost/share-logo-image-wide.jpeg"
    },
    "linkedInShareLogo": {
      "id": "00000000-0000-0000-0000-000000000111",
      "href": "https://localhost/linkedin-share-logo-image.jpeg"
    },
    "shareDescription": "This is my share description.",
    "createdAt": "2022-12-01T16:02:39.115Z",
    "sharingTexts": {
      "email": {
        "en_US": "EmailSharingText"
      },
      "wechat": {
        "en_US": "WeChatSharingText"
      },
      "whatsapp": {
        "en_US": "WhatsAppSharingText"
      }
    },
    "jobHeaderColor": "#ffffff",
    "jobBackgroundColor": "#000000"
}
```

`POST /v1/companies/{companyId}/job_brandings`

### Parameters

| Property           | Required | Description                                                        |
|:-------------------|:---------|:-------------------------------------------------------------------|
| name               | Yes      | The name of the new job branding.
| jobHeader          | Yes      | The job header image that will be used for the new job branding. [See here](#files)
| shareLogo          | Yes      | The share logo that will be used for the new job branding. [See here](#files)
| shareLogoWide      | No       | The wide share logo that will be used for this job branding by certain share channels. [See here](#files)
| shareDescription   | Yes      | The share description that will be used for the new job branding.
| sharingTexts       | Yes      | Text suggestions for when Talent Scouts share a job.
| jobHeaderColor     | No       | The page heading color for the companies job page.
| jobBackgroundColor | No       | The page backgroud color for the companies job page.

## Updating a Job Branding

To update an existing Job Branding for your company use following request:

### HTTP Request

> This is an example request body

```json
{
  "name": "company-default-branding",
  "jobHeader": {
      "id": "00000000-0000-0000-0000-000000000001"
  },
  "shareLogo": {
      "id": "00000000-0000-0000-0000-000000000002"
  },
  "shareLogoWide": {
      "id": "00000000-0000-0000-0000-000000000003"
  },
  "shareDescription": "my company",
  "sharingTexts": {
      "email": {
          "en_US": "EmailSharingText"
      },
      "whatsapp": {
          "en_US": "WhatsAppSharingText"
      },
      "wechat": {
          "en_US": "WeChatSharingText"
      }
  },
  "jobBackgroundColor": "#000000",
  "jobHeaderColor": "#ffffff"
}
```

`PUT /v1/companies/{companyId}/job_brandings/{jobBrandingId}`

### Parameters

| Property           | Required | Description                                                        |
|:-------------------|:---------|:-------------------------------------------------------------------|
| name               | Yes      | The name of the new job branding.
| jobHeader          | Yes      | The job header image that will be used for the new job branding. [See here](#files)
| shareLogo          | Yes      | The share logo that will be used for the new job branding. [See here](#files)
| shareLogoWide      | No       | The wide share logo that will be used for this job branding by certain share channels. [See here](#files)
| shareDescription   | Yes      | The share description that will be used for the new job branding.
| sharingTexts       | Yes      | Text suggestions for when Talent Scouts share a job.
| jobHeaderColor     | No       | The page heading color for the companies job page.
| jobBackgroundColor | No       | The page backgroud color for the companies job page.

> This request returns JSON structured like this:

```json
{
    "id": "00000000-0000-0000-0000-000000000010",
    "company": {
      "id": "00000000-0000-0000-0000-000000000011",
      "href": "https://api.1brd.com/v1/companies/00000000-0000-0000-0000-000000000011"
    },
    "name": "Branding One",
    "isDefault": false,
    "jobHeader": {
      "id": "00000000-0000-0000-0000-000000000001",
      "href": "https://localhost/job-header-image.jpeg"
    },
    "shareLogo": {
      "id": "00000000-0000-0000-0000-000000000002",
      "href": "https://localhost/share-logo-image.jpeg"
    },
    "shareLogoWide": {
      "id": "00000000-0000-0000-0000-000000000003",
      "href": "https://localhost/share-logo-image-wide.jpeg"
    },
    "linkedInShareLogo": {
      "id": "00000000-0000-0000-0000-000000000111",
      "href": "https://localhost/linkedin-share-logo-image.jpeg"
    },
    "shareDescription": "This is my share description.",
    "createdAt": "2022-12-01T16:02:39.115Z",
    "sharingTexts": {
      "email": {
        "en_US": "EmailSharingText"
      },
      "wechat": {
        "en_US": "WeChatSharingText"
      },
      "whatsapp": {
        "en_US": "WhatsAppSharingText"
      }
    },
    "jobBackgroundColor": "#000000",
    "jobHeaderColor": "#ffffff"
}
```

## Deleting a Job Branding

To delete an existing Job Branding for your company use following request:

### HTTP Request
`DELETE /v1/companies/{companyId}/job_brandings/{jobBrandingId}`
