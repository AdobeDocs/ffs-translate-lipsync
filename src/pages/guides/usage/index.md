---
title: API Usage Notes
description: This is a guide explaining limitations, workarounds, and current support.
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../../../styles/main.css";

# API Usage Notes

This guide provides details to refer to while using the APIs, including what's currently supported, limitations and workarounds, and the current usage limits set for each API.

## Video Services: Using the Transcribe, Dubbing, Lip Sync APIs

### Understanding Limitations and Workarounds

- **Speaker Mismatch:** Output transcripts may occasionally feature speaker mismatches or additional/missing speakers, observed in approximately 9% of cases.
- **Children's Voices:** Currently, we do not support children's voices for translation. Support for children's voices is planned for the upcoming v4 model.
- **Voice Modulation:** Output may vary in pitch or voice due to significant modulation. Regenerating the video/audio can often resolve this issue.
- **Re-dubbing Dubbed Content:** Avoid using deepfake content for re-dubbing purposes.

#### Language Support

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
- Dutch (Netherlands) (`nl-NL`)
- Swedish (Sweden) (`sv-SE`)
- German (`de-DE`)
- Italian (`it-IT`)
- Portugese (Brazil) (`pt-BR`)
- Portugese (Portugal) (`pt-PT`)
- Hindi (India) (`hi-IN`)
- Japanese (Japan) (`ja-JP`)
- Korean (South Korea) (`ko-KR`)
- Chinese (Simplified, China) (`zh-CN`)

#### Input Video Support (Audio + Lip Sync dubbing):

- **Duration (max):** 30 mins
- **FPS:** 24 fps, 25 fps, 29.97, 30, 50, 59.94, 60
- **Resolution (max):** Full HD `1,920*1,080px` or `1080*1920px`
- **CODEC**: `H.264`
- **Formats/container:** `.mp4, .mp3, .wav `
- ***Input Medium:** Pre signed URL
- **Render time:** 2x the video length (for 30 fps and 1080 resolution) if LipSync is enabled
- **Min speaker speech:** 5 secs

#### Input Audio Support (Audio dubbing):

- **Duration (max):** 30 mins
- **CODEC:** `MPEG, PCM`
- **Formats/container:** `.mp3, .wav, .aac`
- **Input Medium:** Pre signed URL
- **Render time:** 2.5x the video length if LipSync is disabled
- **Dubbing + Lip Sync:** Multi speaker support

#### Editing Transcripts Note

Currently, only sentence editing is supported. Please do not modify the timestamps. Speakers can be updated accordingly; however, do not remove speakers before dubbing, and dub using the edited transcripts in different target languages.

## Request Limits per API

To ensure you enjoy equitable peak performance with the APIs, Adobe places limits on the volume, frequency, and concurrency of API calls, and monitors your API usage to proactively contact you and resolve any risks to API performance. We currently limit the rate of API requests per minute to the following:

### Video APIs

**Dubbing/Lip Sync:**  5 request per minute and 150 requests per day.

**Transcribe:** 5 request per minute<br/>

**Get Result:** 100 requests per minute<br/>

<InlineAlert variant="warning" slots="text1" />

Bear in mind that these usage limits apply to **your entire organization** <br/>