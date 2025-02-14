---
title: Transcribe API Quickstart
description: This page is a quickstart guide for the ADLS Transcribe API.
---

# Transcribe API

Quickstart commands to create a transcription from audio or video files.

## Before you start

- You'll need a valid access token and client ID. See the [Authentication Guide](../getting_started/index.md) for details.
- Upload your media files (audio or video) to [your storage location and generate a pre-signed URL](../getting_started/storage_solutions/index.md).

## Quickstart commands

In the commands below, be sure to:

- Update the `Authorization` with the bearer access token.
- Update `x-api-key` with the client ID.
- Update `url` with the generated pre-signed url for your input file.

You can try these curl requests directly in your terminal. Or you can use an HTTP client like [Postman](https://www.postman.com/).

### Transcribe audio with source language output

```bash
curl --location 'https://audio-video-api.adobe.io/beta/transcribe' \
--header 'Authorization: Bearer {AccessToken}' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {ClientID}' \
--data '{
  "audio": {
    "source": {
         "url" : "{Presigned_URL}"
    },
    "mediaType": "audio/mp3"
  }
}'
```

### Transcribe audio with target language output

```bash
curl --location 'https://audio-video-api.adobe.io/beta/transcribe' \
--header 'Authorization: Bearer {AccessToken}' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {ClientID}' \
--data '{
  "audio": {
    "source": {
         "url" : "{Presigned_URL}"
    },
    "mediaType": "audio/mp3"
  },
    "targetLocaleCodes": [
        "en-US",
        "es-ES",
        "de-DE",
        "fr-FR",
        "it-IT",
        "pt-PT"
    ]
}'
```

### Transcribe video with source language output

```bash
curl --location 'https://audio-video-api.adobe.io/beta/transcribe' \
--header 'Authorization: Bearer {AccessToken}' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {ClientID}' \
--data '{
  "video": {
    "source": {
         "url" : "{Presigned_URL}"
    },
    "mediaType": "video/mp4"
  }
}'
```

### Transcribe video with target language output

```bash
curl --location 'https://audio-video-api.adobe.io/beta/transcribe' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "video": {
    "source": {
         "url" : "<<Replace with the presigned URL of the input video file>>"
    },
    "mediaType": "video/mp4"
  },
   "targetLocaleCodes": [
        "en-US",
        "es-ES",
        "de-DE",
        "fr-FR",
        "it-IT",
        "pt-PT"
    ]
}'
```

## Check the result

Note the job ID in the response and use the [Get Result API](get_result_quickstart.md) to see the final result.

**Sample response**

```json
{
    "jobId": "500de496-4961-4641-a273-1c760ee7e0b4",
    "status": "succeeded",
    "outputs": [
        {
            "destination": {
                "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/500de496-4961-4641-a273-1c760ee7e0b4/translation_de_DE.txt?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=Jfx%2F%2FL1GJqHjrWHVph0FcxoqpJs%3D&Expires=1725446894"
            },
            "localeCode": "de-DE"
        },
        {
            "destination": {
                "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/500de496-4961-4641-a273-1c760ee7e0b4/translation_es_sp.txt?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=FA5OF%2BXKZhnvmUcKHGAYkbhGpDs%3D&Expires=1725446894"
            },
            "localeCode": "es-ES"
        }
    ]
}
```
