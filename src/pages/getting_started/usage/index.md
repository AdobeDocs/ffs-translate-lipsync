---
title: ADLS API Usage Notes
description: This is a guide explaining limitations, workarounds, and current support for the ADLS API.
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../../../styles/main.css";

# Video Services API Usage Notes

On this page you'll find what's currently supported, known limitations and workarounds, and the current usage limits set for the Adobe Dubbing and Lip Sync (ADLS) API.

## Known limitations and workarounds

- **Speaker Mismatch:** Speaker mismatches or additional/missing speakers may occasionally occur in output transcripts. This has been observed in approximately 9% of cases.
- **Voice Modulation:** Voices in the output may vary in pitch or show significant modulation. Regenerating the video/audio can often resolve this issue.
- **Re-dubbing Dubbed Content:** Avoid using deepfake content for re-dubbing purposes.

## For editing transcripts

Only sentence editing is currently supported. Please don't modify the timestamps.

Speakers can be updated, however don't remove speakers before dubbing. Also, dub using the edited transcripts in different target languages.

## Language support

Dubbing is supported for the following languages:

- English (Indian) (`en-IN`)
- English (American) (`en-US`)
- English (British) (`en-GB`)
- Spanish (Spanish) (`es-ES`)
- Spanish (Argentina) (`es-AR`)
- Spanish (Latin America) (`es-419`)
- French (France) (`fr-FR`))
- French (Canada) (`fr-CA`)
- Danish (Denmark) (`da-DK`)
- Norwegian (Norway) (`nb-NO`)
- German (`de-DE`)
- Italian (`it-IT`)
- Portuguese (Brazil) (`pt-BR`)
- Portuguese (Portugal) (`pt-PT`)
- Hindi (India) (`hi-IN`)
- Japanese (Japan) (`ja-JP`)
- Korean (South Korea) (`ko-KR`)

## Input video support

Technical details for videos used as input:

- **Duration (max):** 30 mins
- **FPS:** 24 fps, 25 fps, 29.97, 30, 50, 59.94, 60
- **Resolution (max):** Full HD `1920*1080px` or `1080*1920px`
- **CODEC**: `H.264, HEVC`
- **Formats/container:** `.mp4, .mov`
- **Input medium:** Pre-signed URL
- **Render time:** 3x the video length, 10x the video length (for 30 fps and 1080 resolution) if `lipSync` is enabled
- **Speaker speech (min):** 5 secs
- **Dubbing and Lip Sync:** Multi-speaker support

## Input audio support

Technical details for audio used as input:

- **Duration (max):** 30 mins
- **CODEC:** `MPEG, PCM`
- **Formats/container:** `.mp3, .wav, .aac`
- **Input medium:** Pre-signed URL
- **Render time:** 3x the audio length
- **Dubbing:** Multi-speaker support

## Request limits per API

To ensure equitable peak performance, Adobe places limits on the volume, frequency, and concurrency of API calls, and monitors API usage in order to proactively reach out and resolve any risks to performance.

<InlineAlert variant="warning" slots="text1" />

These usage limits apply to your entire organization. <br/>

The current limitations are:

**Transcribe endpoint:** 5 requests per minute.

**Dubbing/Lip Sync endpoint:**  5 requests per minute and 150 requests per day.

**Get Result endpoint:** 100 requests per minute.
