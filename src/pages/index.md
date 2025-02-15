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

Use ADLS to create audio or video dubs.

## Overview

The Dubbing and Lip Sync (ADLS) API is a resource that allows you to use transcriptions to generate audio and video with precise, accurate dubbing and composited lip sync. This feature supports multi-speaker scenarios.

There are three supported workflows:

1. **Automated Dubbing** for audio and video.
2. **Dubbing with edited transcripts**.
3. **Dubbing with pre-existing translations**.

**Lip Sync** is also included as a parameter of the Dub API to create high-quality composited videos with precise lip-syncing.

[Content Authenticity Initiative (CAI)](http://contentauthenticity.org/) support ensures protection against deepfakes.

<DiscoverBlock slots="heading, link, text"/>

### Current features

[Dub API](./api/index.md)

Use audio and video voice transriptions to produce high-quality dubs, regardless of background noise and music.

<DiscoverBlock slots="link, text"/>

[Get Result API](./api/index.md)

See the result for an async dubbing or transcribe job.

[Check out the Getting Started page](./getting_started/) when you're ready to set up your project, obtain and authenticate your credentials, and learn to build efficient workflows by chaining API calls across these endpoints.
