# Integration of Digital and Visible Watermarks

## Overview

MPS supports two types of watermarks:

- **Digital watermark:** Embeds invisible text information into the video stream. Both a basic copyright watermark and the **NAGRA NexGuard** forensics watermark are supported.
- **Visible watermark:** Adds user‑defined images (PNG or JPG) or text over the video for copyright protection or branding.



## Digital watermark

### Versions and billing

- **Basic copyright watermark:** Provides invisible text embedding.
- **NAGRA NexGuard forensics watermark:** Offers strong concealment and anti‑removal capabilities for high‑value content.
- **Billing:** Digital watermark addition is charged by the duration of the output video. Because digital watermarking depends on transcoding or enhancement, you incur fees for both watermark addition and the underlying transcoding/enhancement. Digital watermark extraction is charged per API call.

### Template creation

Log into the console and create a digital watermark template. Each user can create up to 50 NexGuard templates. Templates cannot be modified or deleted through the console; modifications require backend assistance.

### Initiating digital watermark addition

- In the console, create an offline processing task, add an **Audio/Video Transcoding** node, enable the digital watermark option and associate a digital watermark template. You can also enable digital watermark when using the enhancement feature.
- Via API, call **ProcessMedia** and specify the transcode template ID and digital watermark template ID in the `BlindWatermark` parameter.
- Up to ten visible watermarks can be added; for digital watermark only one template ID is required per task.

### Automatic triggering

To automatically add digital watermarks when files are uploaded to COS:

1. Save an orchestration when creating a task and configure the trigger bucket/directory.
2. Enable the orchestration and, after activation, new files in the directory trigger watermarking tasks.

### Digital watermark extraction

- Use the **Digital Watermark Extraction** console page to select a video and extract the basic watermark. NexGuard extraction requires a support ticket.
- Via API, call **ExtractBlindWatermark** with the watermark type (`blind-basic` for basic watermarks), specifying the COS bucket, region and object path.

## Visible watermark

### Billing

Adding a visible watermark does **not** incur extra fees.

### Template creation

Create a visible watermark template in the console; both image and text watermarks are supported.

### Initiating visible watermark addition

- In the console, create an offline processing task, select a transcoding node and enable the visible watermark option. Associate the watermark template; up to **ten** images or text watermarks can be added. Visible watermarks can also be enabled during enhancement or screencapturing.
- Via API, call **ProcessMedia** and include a `WatermarkSet` with the watermark template ID.

### Automatic triggering

Visible watermark tasks follow the same orchestration‑based auto‑trigger procedure as digital watermarks.
