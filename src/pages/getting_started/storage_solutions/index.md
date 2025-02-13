---
title: Storage Solutions
description: This page explains the storage solutions that are acceptalbe for use with video services.
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../../../styles/main.css";

# Storage Solutions

You will need to be able to use some type of user owned storage (ie: Amazon S3 buckets) for the video/audio and edited transcripts to be able to generate a presigned URL to supply as the video/audio file input for the APIs.

Some ways to achieve this are described below.

## Using Amazon S3 buckets

  1. Login to your AWS account.
  2. Go to s3.
  3. Create a new bucket with some name (ex: `adobeapitesting`).
  4. Drag and drop the video file/audio file/edited transcript file you want to test in the bucket.
  5. Once the upload completes, select the file and go to **Actions**.
  6. Select the **Share with presigned url** option and give the duration you want the presigned url to be valid.
  7. Copy the generated presigned url (it will also automatically be copied when you create it).

## Using Frame.io account

  1. Login to your Frame.io account
  2. Create a project (ie: `AdobeApiTesting`)
  3. Open the inspect view of the browser. (In Chrome, press f12 and go to the "network" tab).
  4. Drag and drop the video file/audio file/edited transcript file you want to test in the bucket.
  5. Select the file and click on download.
  6. In the "network" tab, you will see a `GET` call using a presigned url to download the file.
  7. Copy that url to use in your API testing.

## Use Google's direct link service

  1. You can use [Google's direct link service](https://sites.google.com/site/gdocs2direct/?authuser=1&pli=1) to generate downloadable public links for your files.
  2. Before generating, you'll need to make sure your file's visibility in your Google Drive is set to **Anyone with the link**.
  3. You can try the `curl` requests for the APIs directly from terminal.

Optionally, you can use an http client like [Postman](https://www.postman.com/) to try out the APIs.

