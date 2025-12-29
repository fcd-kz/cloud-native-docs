# Audio/Video Transcoding Integration

## Overview

Transcoding converts the original audio/video stream into another stream by changing parameters such as codec, resolution and bitrate. This offline process adapts media for different devices and network conditions. MPS supports multiple transcoding types for **video**—standard, Top Speed Codec (TSC), adaptive bitrate streaming and Remux—and **audio**—standard, TSC and adaptive bitrate streaming.

- **Standard transcoding:** reduces bitrate and converts encoding standard, resolution or frame rate.
- **TSC transcoding:** an upgraded feature that optimises videos and audios to deliver high‑definition experiences while cutting bandwidth consumption.
- **Adaptive bitrate streaming:** converts a source file into multiple bitrate streams so end‑users can choose the appropriate version based on network conditions.
- **Remux:** changes only the container format of a video without re‑encoding.

## Technical strengths

Freedom Cloud MPS provides comprehensive encoding methods (e.g., VP8, H.264, VP9, H.265, AV1, AVS3, H.266) to significantly reduce bitrate without quality loss. Top Speed Codec uses intelligent dynamic encoding to improve subjective quality, supports real‑time encoding up to 8K resolution and integrates technologies such as super‑resolution, HDR and Dolby Vision/Dolby Atmos. Distributed transcoding across numerous instances accelerates tasks and reduces bandwidth costs.



## Creating tasks

MPS offers three ways to create transcoding tasks.

### Method 1 – Console (zero‑code)

1. In the MPS console, click **Create Task > Create VOD Processing Task**.
2. **Specify the input file:** select a file from COS or AWS S3, or provide a download URL.
3. **Add a Transcoding node** in the workflow.
4. **Choose a template or customise parameters** in the Transcoding settings window.
5. **Specify the output path** and click **Create** to start the task.

### Method 2 – API

Use the **ProcessMedia** API:

- **Specify a template ID:** Provide input and output storage information and include a `TranscodeTaskSet` with the template ID.
- **Specify an orchestration ID:** For complex workflows, use a Schedule ID instead of a `TranscodeTaskSet`.

Additional parameters (`StdExtInfo`) allow advanced settings, such as enabling silence packets in audio streams or uploading outputs to third‑party storage (OSS, AWS S3) by specifying bucket, region, credentials and headers.

### Method 3 – Automatic trigger

To automatically transcode files uploaded to a COS bucket:

1. When creating a task, click **Save the Orchestration** and configure the trigger bucket and directory.
2. In the VOD orchestration list, enable the orchestration. After a brief activation period, the configuration takes effect.
3. Files added to the trigger directory automatically start transcoding tasks, and outputs are saved to the configured output path.

## Querying task results

- **Task callback:** When calling `ProcessMedia`, you can specify `TaskNotifyConfig` so MPS will send notifications upon completion.
- **DescribeTaskDetail:** Query the status and result of a task by providing its Task ID to the `DescribeTaskDetail` API.
- **Console:** On the VOD processing tasks page you can see each task, and when subtasks succeed you can preview or download output files.

## Additional features

- **Watermarking:** When creating a transcoding task, you can attach watermark templates. For API usage, supply a `WatermarkSet` within the `TranscodeTaskSet`.
- **Subtitles (hard subtitles):** You can embed subtitles into the video. The console lets you select a subtitle file or track and customise the style; the API supports the same via parameters. Embedding subtitles incurs transcoding fees.
- **Audio silence packet supplementation and custom storage:** Use `StdExtInfo` for options such as enabling silence packets when audio frames are discontinuous or uploading results to third‑party storage.
