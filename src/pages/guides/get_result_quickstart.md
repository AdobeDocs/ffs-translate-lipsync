---
title: Get Result API Quickstart
description: This page is a quickstart guide for the ADLS Get Result API.
---
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
