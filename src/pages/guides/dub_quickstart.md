---
title: Dub API Quickstart
description: This page is a quickstart guide for the ADLS Dub API.
---
# Dub API

Quickstart commands to dub audio or video with a target language or edited transcript.

## Before you start

- You'll need a valid access token and client ID. See the [Authentication Guide](../getting_started/index.md) for details.
- Upload your media files (audio or video) to [your storage location and generate a pre-signed URL](../getting_started/storage_solutions/index.md).

## Quickstart commands

In the commands below, be sure to:

- Update the `Authorization` with the bearer access token.
- Update `x-api-key` with the client ID.
- Update `url` with the generated pre-signed url for your input file.

You can try these curl requests directly in your terminal. Or you can use an HTTP client like [Postman](https://www.postman.com/).

### Automated dubbing

You'll need to pass `targetLocaleCodes` in these commands.

#### Automated dubbing for video

```bash
curl --location 'https://audio-video-api.adobe.io/beta/dub' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "video": {
    "source": {
        "url": "<<Replace with the presigned URL of the input video file>>"
    },
    "mediaType": "video/mp4"
  },
  "targetLocaleCodes": [
    "<<Replace with the command separated values of locale code>>"
  ],
  "lipSync": "false"
}'
 ```

#### Automated dubbing for audio

```bash
curl --location 'https://audio-video-api.adobe.io/beta/dub' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "audio": {
    "source": {
        "url": "<<Replace with the presigned URL of the input video file>>"
      },
      "mediaType": "audio/mp3"
    },
    "targetLocaleCodes": [  "<<Replace with the command separated values of locale code>>"   ],
    "lipSync": "false"
}'
```

### Dubbing with edited transcript

You'll need to pass the `targetLocaleCodes` and `edited transcripts` in these commands. The `transcripts` should contain **only one value** with the URL for the edited transcript.

#### Dubbing with edited translations for video

```bash
curl --location 'https://audio-video-api.adobe.io/beta/dub' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "video": {
    "source": {
      "url": "<<Replace with the presigned URL of the input video file>>"
    },
    "mediaType": "video/mp4"
  },
  "transcripts": [
    {
      "source": {
        "url": "<<Replace with the presigned URL of the input transcript file>>"
      }
    }
  ],
  "targetLocaleCodes": [
    "<<Replace with the comma-separated values of locale code>>"
  ],
  "lipSync": "false"
}'
```

#### Dubbing with edited translations for audio

```bash
curl --location 'https://audio-video-api.adobe.io/beta/dub' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "audio": {
    "source": {
      "url": "<<Replace with the presigned URL of the input video file>>"
    },
    "mediaType": "audio/mp3"
  },
  "transcripts": [
    {
      "source": {
        "url": "<<Replace with the presigned URL of the input translated transcript file in de-DE>>"
      },
      "localeCode": "de-DE"
    },
    {
      "source": {
        "url": "<<Replace with the presigned URL of the input translated transcript file in en-US>>"
      },
      "localeCode": "en-US"
    }
  ],
  "lipSync": "false"
}'
```

### Dubbing with pre-existing translations

You need to pass `transcripts` along with `localeCode` in this case. Each value of `transcripts` contains the URL to download the transcript AND the locale code for the same.

#### Dubbing with pre-existing translations for video

```bash
curl --location 'https://audio-video-api.adobe.io/beta/dub' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "video": {
    "source": {
        "url": "<<Replace with the presigned URL of the input video file>>"
    },
    "mediaType": "video/mp4"
  },
  "transcripts": [{
        "source": {
            "url": "<<Replace with the presigned URL of the input translated transcript file in de-DE>>"
        },
        "localeCode": "de-DE"
    },{
        "source": {
            "url": "<<Replace with the presigned URL of the input translated transcript file in en-US>>"
        },
        "localeCode": "en-US"
    }
  ],
  "lipSync": "false"
}'
```

#### Dubbing with pre-existing translations for audio

```bash
curl --location 'https://audio-video-api.adobe.io/beta/dub' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "audio": {
    "source": {
      "url": "<<Replace with the presigned URL of the input video file>>"
    },
    "mediaType": "audio/mp3"
  },
  "transcripts": [
    {
      "source": {
        "url": "<<Replace with the presigned URL of the input translated transcript file in de-DE>>"
      },
      "localeCode": "de-DE"
    },
    {
      "source": {
        "url": "<<Replace with the presigned URL of the input translated transcript file in en-US>>"
      },
      "localeCode": "en-US"
    }
  ],
  "lipSync": "false"
}'
```

## Check the result

Note the job ID in the response and use the [Get Result API](get_result_quickstart.md) to see the final result.

**Sample response**

```bash
{
    "jobId": "986fc222-1118-4242-b326-eb9873e3982f",
    "statusUrl": "https://audio-video-api.adobe.io/beta/status/<<Replace with the job id>>"
}
```
