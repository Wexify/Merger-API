## Merger File Upload API Documentation

This document describes the `/upload/:fileId` endpoint of the FFAPI for uploading files.

### Functionality

This endpoint provides a pre-signed URL for uploading a file and the URL where the uploaded file can be accessed after successful upload.

### Endpoint

- **Method:** GET

- **URL:** `/upload/:fileId`

**Parameter:**

- `:fileId` (string, required): The unique identifier for the file. It is best to use file hash.

### Response Format

The response is a JSON object with the following structure:

**Success Response:**

```json

{

  "success": true,

  "result": {

    "upload": "https://...", // Pre-signed upload URL

    "file": "http://..." // URL to access the uploaded file

  }

}

```

- `success`: Boolean indicating success (true) or failure (false).

- `result`: Object containing the upload and file URLs.

  - `upload`: String containing the pre-signed URL for uploading the file. This URL is temporary and will expire after a set time.

  - `file`: String containing the URL to access the uploaded file after successful upload.

**Error Response:**

```json

{

  "success": false,

  "error": {

    "message": "Error message"

  }

}

```

- `success`: Boolean indicating success (false) or failure (true).

- `error`: Object containing error details.

  - `message`: String describing the error that occurred.

### Example Usage

**Request:**

```

POST /upload/my-unique-file-id

```

**Successful Response:**

```json

{

  "success": true,

  "result": {

    "upload": "https://ffapi-user-file-uploads.1d5d990f0f0ecbbf192bfd882bc4e715.r2.cloudflarestorage.com/726f88c6-adba-445a-8db8-3e26247931a1_my-file-id?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=517d715629d54f2f8390e90c259fbcba%2F20241224%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20241224T104034Z&X-Amz-Expires=1800&X-Amz-Signature=472b4598ef93ec271ab3da4c4d8f8cc1dcd48039e095e4cb1912289091868de5&X-Amz-SignedHeaders=host&x-id=PutObject",

    "file": "http://localhost:8080/get/726f88c6-adba-445a-8db8-3e26247931a1_my-file-id"

  }

}

```

This response provides the pre-signed URL for uploading the file and the URL to access the uploaded file once complete.

**Error Response:**

```json

{

  "success": false,

  "error": {

    "message": "Please provide a file id"

  }

}

```
