---
title: Adobe Translate and Lip Sync (TLS) Overview
description: This is the overview page for the Adobe Translate and Lip Sync (TLS) APIs.
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../styles/main.css";

<Hero slots="heading, text" background="rgb(233, 80, 80)" className="adls-header"/>

# Adobe Translate and Lip Sync (TLS) APIs

Dub audio or video with optional lip syncing.

## Overview

The Translate and Lip Sync (TLS) API uses transcriptions to generate audio and video with precise, accurate dubbing and composited lip sync. This feature supports multi-speaker scenarios.

Supported workflows include:

1. **Transcribe** audio and video.
2. **Generate captions** for audio and video.
3. **Automated Dubbing** for audio and video.
4. **Dubbing with edited transcripts**.
5. **Dubbing with pre-existing translations**.

**Lip Sync** is also included as a parameter of the Dub API to create high-quality composited videos with precise lip-syncing.

[Content Authenticity Initiative (CAI)](http://contentauthenticity.org/) support ensures protection against deepfakes.

<DiscoverBlock slots="heading, link, text"/>

### Discover

[Transcribe API](./api/index.md)

Generate transcripts for the input audio or video.

<DiscoverBlock slots="link, text"/>

[Dub API](./api/index.md)

Use audio and video voice transcriptions to produce high-quality dubs, regardless of background noise and music.

<DiscoverBlock slots="link, text"/>

[Get Result API](./api/index.md)

See the result for an asynchronous dubbing or transcribe job.

[Check out the Getting Started page](./getting_started/) when you're ready to set up your project, authenticate your credentials, and learn to build efficient workflows by chaining API calls across these endpoints.
