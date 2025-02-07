---
title: Video - Adobe Firefly API
description: This guide explains get started with video services.
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../../../styles/main.css";

# Getting Started with Video Services

## Overview

Transcribe, Dubbing & LipSync APIs address the need for automated video translation and lip-syncing at scale.  This document provides a guide to use these Async APIs  for:

- Generating transcripts for customer owned video/audio files
- Dubbing customer owned video/audio files in different languages with lip syncing capability
- Providing ability to customers to download and then edit the source transcripts (Only sentences edit is supported right now, please do not modify "timestamps". Speakers can be updated accordingly however dont remove speakers) before dubbing and dub using the edited transcripts in different target languages
- Providing ability to customers to dub using their own translated transcripts

## Prerequisites

### API credentials

The required credentials were provided as part of the public beta in the form of a `client_id` and `client_secret`. You will need them available to get started.

### Storage solution

You will need to be able to use some type of user owned storage (ie: Amazon S3 buckets) for the video/audio and edited transcripts to be able to generate a presigned URL to supply as the video/audio file input for the APIs.

Some ways to achieve this are described below.

#### Using Amazon S3 buckets

  1. Login to your AWS account.
  2. Go to s3.
  3. Create a new bucket with some name (ex: `adobeapitesting`).
  4. Drag and drop the video file/audio file/edited transcript file you want to test in the bucket.
  5. Once the upload completes, select the file and go to **Actions**.
  6. Select the **Share with presigned url** option and give the duration you want the presigned url to be valid.
  7. Copy the generated presigned url (it will also automatically be copied when you create it).

#### Using Frame.io account

  1. Login to your Frame.io account
  2. Create a project (ie: `AdobeApiTesting`)
  3. Open the inspect view of the browser. (In Chrome, press f12 and go to the "network" tab).
  4. Drag and drop the video file/audio file/edited transcript file you want to test in the bucket.
  5. Select the file and click on download.
  6. In the "network" tab, you will see a `GET` call using a presigned url to download the file.
  7. Copy that url to use in your API testing.

#### Use Google's direct link service

  1. You can use [Google's direct link service](https://sites.google.com/site/gdocs2direct/?authuser=1&pli=1) to generate downloadable public links for your files.
  2. Before generating, you'll need to make sure your file's visibility in your Google Drive is set to **Anyone with the link**.
  3. You can try the `curl` requests for the APIs directly from terminal.

Optionally, you can use an http client like [Postman](https://www.postman.com/) to try out the APIs.

## API Walkthrough

<InlineAlert slots="text" />

There is a limit of 5 RPM for transcribe and dub endpoints and x100 RPM for Get result API per user.

### Transcribe API

This endpoint enables transcription of audio or video input provided via a presigned URL. The API processes the input in supported languages and returns the transcription in the specified target language.

#### Step 1

Ensure you have reference to a valid access token. See the [Authentication Guide](../index.md) for details on how to obtain such a token.

#### Step 2

Upload the input audio file/video file to storage location and generate a presigned url to access the same (Refer to the [Prerequisites](#prerequisites) section for more details).

#### Step 3

In the curl command below, update the **Authorization** with the bearer token in step 1, **x-api-key** as per the prerequisite, **mediaType** as per input type and **url** with the generated presigned url and run the curl.

<InlineAlert variant="info" slots="text1" />

Please refer to the [usage notes](../usage/) for details about supported media types and locale codes.

**cURL Command for Audio with Source Language Output**

```bash
curl --location 'https://audio-video-api.adobe.io/beta/transcribe' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "audio": {
    "source": {
         "url" : "<<Replace with the presigned URL of the input audio file>>"
    },
    "mediaType": "audio/mp3"
  }
}'
```

**cURL Command for Audio with Target Language Output**

```bash
curl --location 'https://audio-video-api.adobe.io/beta/transcribe' \
--header 'Authorization: Bearer <<Token>>' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <<Client-ID>>' \
--data '{
  "audio": {
    "source": {
         "url" : "<<Replace with the presigned URL of the input audio file>>"
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

**cURL Command for Video with Source Language Output**

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
  }
}'
```

**cURL Command for Video with Target Language Output**

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

#### Step 4

Check the job id in the response and follow the steps in [GET Result API](#get-result-api) to get the final result.

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

### Dub API

The Dub API automates the generation of voices in specified target languages, offering high-quality dubbing output. It supports both audio and video inputs, ensuring voice translation with optional lip-syncing. The API handles various complexities such as background noise and music, delivering precise results regardless of input quality

#### Step 1

Ensure you have reference to a valid access token. See the [Authentication Guide](../index.md) for details on how to obtain such a token.

#### Step 2

Upload the input audio file/ video file to your user storage location and generate a presigned url (refer to the [Prerequisites](#prerequisites)).

#### Step 3

In the `curl` below, update the **Authorization** with the bearer token from step 1, **x-api-key** as per the prerequisite, **mediaType** as per input type and **url** with the generated presigned url, specify the target languages or the transcripts and if lip sync is required or not and run the curl.

<InlineAlert variant="info" slots="text1" />

Please refer to the [usage notes](../usage/) for details about supported media types and locale codes.

The API supports three workflows:

1. **Automated Dubbing:** Using target locale codes, in which case the translations and dubbing, (with or without lip sync based on user input), is done at the service end using the default transcripts. You must pass `targetLocaleCodes` in this case.

**cURL for Automated dubbing (Video)**

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

**cURL for Automated dubbing (Audio)**

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

2. **Dubbing with edited transcript:** Using edited transcripts, where the dubbing (with or without lip sync based on user input) is done at service end. You'll need to pass the `targetLocaleCodes` and `edited transcripts` in this case. The `transcripts` **should contain only one value with the url for the edited transcript**.

**cURL for Dubbing with edited translations (Video)**

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

**cURL for Dubbing with edited translations (Audio)**

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

3. **Dubbing with Pre-Existing Translations:** In this workflow only dubbing (with or without lip sync based on user input) is done at service end using the pre-existing translations provided as input. `transcripts` along with `localeCode` should be passed in this case. Each value in the `transcripts` contains the url to download the transcript and the locale code for the same.

**cURL for Dubbing with Pre-Existing Translations (Video)**

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

**cURL for Dubbing with Pre-Existing Translations (Audio)**

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

#### Step 4

Check the job id in response and follow the steps in [GET Result API](#get-result-api) to get the final result.

##### Sample response

```bash
{
    "jobId": "986fc222-1118-4242-b326-eb9873e3982f",
    "statusUrl": "https://audio-video-api.adobe.io/beta/status/<<Replace with the job id>>"
}
```

### GET Result API

#### Step 1

Update the `jobId`, `Authorization` and `x-api-key` in the command below. **Note:** The `jobId` was returned in the response of the [transcribe](#transcribe-api) or [dub](#dub-api) API call.

**cURL for Get Status**

```bash
curl --location 'https://audio-video-api.adobe.io/beta/status/<<Replace with the job id>>' \
--header 'Authorization: Bearer <<Token>>' \
--header 'x-api-key: <<Client-ID>>' \
--header 'Content-Type: application/json'
```

The status of the job can be:

- `"pending"`
- `"running"`
- `"failed"`
- `"succeeded"`
- `"partially_succeeded"`

When it's `succeeded`, you will see the result for the operation.

##### Sample Transcribe API response

```bash
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

The `url` can be used to download the transcript file for the input.

##### Sample Dub API Response

```bash
{
    "jobId": "d639c2a7-4b18-44cc-9f9b-d4d90dc48595",
    "status": "succeeded",
    "outputs": [
        {
            "localeCode": "de-DE",
            "audio": {
                "mediaType": "audio/wav",
                "destination": {
                    "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/d639c2a7-4b18-44cc-9f9b-d4d90dc48595/signed_output_de_DE_0_soundliftmix.wav?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=okbACJJHLxFLbysdPhjbho9LFT4%3D&Expires=1725446974"
                }
            },
            "video": {
                "mediaType": "video/mp4",
                "destination": {
                    "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/d639c2a7-4b18-44cc-9f9b-d4d90dc48595/signed_output_de_DE_0_soundliftmix.mp4?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=7UK1%2FY%2FVTAWRUupKG%2FqmXJE%2F4OQ%3D&Expires=1725446974"
                }
            },
            "transcript": {
                "destination": {
                    "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/d639c2a7-4b18-44cc-9f9b-d4d90dc48595/translation_de_DE.txt?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=FN%2Fg%2FM%2BrwLWi8Ve4JluaLX6KLkI%3D&Expires=1725446974"
                }
            }
        },
        {
            "localeCode": "en-US",
            "audio": {
                "mediaType": "audio/wav",
                "destination": {
                    "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/d639c2a7-4b18-44cc-9f9b-d4d90dc48595/signed_output_en_US_0_soundliftmix.wav?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=TaN5jAs%2BPkxcGXzSprY762OrUZ4%3D&Expires=1725446974"
                }
            },
            "video": {
                "mediaType": "video/mp4",
                "destination": {
                    "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/d639c2a7-4b18-44cc-9f9b-d4d90dc48595/signed_output_en_US_0_soundliftmix.mp4?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=1NTrzLspbHdc3wai4hFomZnwVQQ%3D&Expires=1725446974"
                }
            },
            "transcript": {
                "destination": {
                    "url": "https://auto-dubbing-stage-ue1.s3-accelerate.amazonaws.com/d639c2a7-4b18-44cc-9f9b-d4d90dc48595/translation_en_US.txt?response-content-disposition=attachment&AWSAccessKeyId=AKIATIXTMZXK45BXP3W2&Signature=KH46%2BTBaispa4FfILVO7bIojI7s%3D&Expires=1725446974"
                }
            }
        }
    ]
}
```

- `audioOutput`: the dubbed audio file in `wav` format.
- `videoOutput`: the dubbed video output with/without lip sync based on input configuration.
- `transcriptOutput`: the translated transcript for the target language.

### Verifying the Content Credentials on output

Introduces a content authentication initiative for AI-generated assets, addressing concerns around content legitimacy.

#### Step 1

Download the final output video/audio using the presigned url in the success response of [GET Result API](#get-result-api).

#### Step 2

Upload the file <https://contentcredentials.org/verify> to check the credentials.
