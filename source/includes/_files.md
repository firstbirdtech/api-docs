# Files

Files are managed via the endpoints described below and are used in various places in Firstbird (e.g. Job Brandings). Wherever you need to specify a file, you always reference them by their Id.

## Upload a File: Binary

To upload a file using in binary use the following request:

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "name": "my_filename.jpeg",
  "contentType": "image/jpeg",
  "size": 100000,
  "createdAt": "2018-10-09T10:04:38Z"
}
```

`POST https://services.1brd.com/files/v1/binary`

### Headers

| Property          | Required | Description                                                        |
|:------------------|:---------|:-------------------------------------------------------------------|
| X-Filename        | Yes      | The name of the file.
| Content-Type      | Yes      | The content type of the file. Must be one of: application/msword, application/vnd.openxmlformats-officedocument.wordprocessingml.document, application/pdf, application/zip, image/jpeg, image/png or image/bmp.

### Request Body

The binary file that you want to upload.

## Upload a File: Multipart

To upload a file using multipart use the following request:

### HTTP Request

> This request returns JSON structured like this:

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "name": "my_filename.jpeg",
  "contentType": "image/jpeg",
  "size": 100000,
  "createdAt": "2018-10-09T10:04:38Z"
}
```

`POST https://services.1brd.com/files/v1/multipart`

### Request Body

In your multipart form, set a key called **file** where you put in the binary file.

## Upload a File: Base64

To upload a file using Base64 use the following request:

### HTTP Request

> This is an example request body

```json
{
  "name": "my_filename.jpeg",
  "contentType": "image/jpeg",
  "contentBase64": "base64-image"
}
```

> This request returns JSON structured like this:

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "name": "my_filename.jpeg",
  "contentType": "image/jpeg",
  "size": 100000,
  "createdAt": "2018-10-09T10:04:38Z"
}
```

`POST https://services.1brd.com/files/v1/base64`

### Parameters

| Property          | Required | Description                                                        |
|:------------------|:---------|:-------------------------------------------------------------------|
| name              | Yes      | The name of the file.
| contentType       | Yes      | The content type of the file. Must be one of: application/msword, application/vnd.openxmlformats-officedocument.wordprocessingml.document, application/pdf, application/zip, image/jpeg, image/png or image/bmp.
| contentBase64     | Yes      | The binary file base64 encoded.