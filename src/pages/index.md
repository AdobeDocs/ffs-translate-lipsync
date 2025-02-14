---
title: Adobe Dubbing and Lip Sync (ADLS) Overview
description: This is the overview page for the Adobe Dubbing and Lip Sync (ADLS) APIs.
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../styles/main.css";

<Hero slots="heading, text" background="rgb(233, 80, 80)" className="adls-header"/>

# Adobe Dubbing and Lip Sync (ADLS) APIs

Use ADLS to translate and transcribe your source, and create audio or video from those transcriptions.

## Overview

The Dubbing and Lip Sync (ADLS) API is a resource that allows you to translate and transcribe your source content, and then use those transcriptions to generate audio and video with precise, accurate dubbing and lip sync.

The current features include:

### [Transcribe API](./api/index.md)

Generate accurate transcriptions in the source language or in another target language. You are able to download and edit these transcripts to use to create a dub.

### [Dub API](./api/index.md)

Use audio and video voice transriptions to produce high-quality dubs, regardless of background noise and music. **Lip Sync** is included as a parameter of the Dub API to create high-quality composited videos with precise lip-syncing. This feature supports multi-speaker scenarios. [Content Authenticity Initiative (CAI)](http://contentauthenticity.org/) support ensures protection against deepfakes.

There are three supported workflows:

1. **Automated Dubbing** for audio and video
2. **Dubbing with edited transcripts** 
3. **Dubbing with pre-existing translations**

### [Get Result API](./api/index.md)

See the result for an async dubbing or transcribe job.

[Check out the Getting Started page](./getting_started/) when you're ready to set up your project, obtain and authenticate your credentials, and learn to build efficient workflows by chaining API calls across these endpoints.
