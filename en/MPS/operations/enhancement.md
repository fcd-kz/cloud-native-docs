# Audio/Video Enhancement Integration

## Overview

The audio/video enhancement feature uses Freedom Cloud’s AI processing models and business data to deliver professional‑grade video and audio enhancement. It offers real‑time image quality improvements such as artifact removal, denoising, color enhancement, detail enhancement, face enhancement, SDR‑to‑HDR conversion and AI model‑based super‑resolution. Enhancement is applied across OTT, e‑commerce, sports events and other scenarios to improve both quality of experience (QoE) and quality of service (QoS).

## Technical strengths

- **Full‑scenario AI enhancement:** Tailored algorithms for gaming, UGC, high‑definition films, education, live shows, e‑commerce and old films.
- **Comprehensive audio enhancement:** Voice denoising, audio separation, audio quality enhancement and volume equalization significantly improve audio clarity.


## Creating tasks

MPS provides three methods.

### Method 1 – Console

1. In the console, click **Create Task > Create VOD Processing Task**.
2. **Specify the input file** from COS/S3 or provide a URL.
3. **Add an Enhancement node** to the workflow.
4. In the **Enhancement settings** window, choose a preset enhancement template. The console templates do not allow you to adjust transcoding parameters such as codec, bitrate and GOP; if these need to be customised, use the API method.
5. **Specify the output path** and click **Create**.

### Method 2 – API

Call **ProcessMedia**:

- **Specify a template ID:** Provide input and output storage information and include a `TranscodeTaskSet`. The template ID corresponds to an enhancement template (e.g., comprehensive enhancement, color enhancement, artifacts removal).
- **Specify a service orchestration ID:** Use a Schedule ID instead of a template ID for tasks built from orchestration.

If you require precise control over transcoding parameters, create custom enhancement templates via the API.

### Method 3 – Automatic trigger

To enhance any video uploaded to COS automatically:

1. Save the orchestration when creating a task and configure the trigger bucket/directory.
2. Enable the orchestration in the list. After activation, new files uploaded to the directory automatically start enhancement tasks and results are saved to the configured output path.

## Querying task results

- **Task callback:** Specify `TaskNotifyConfig` in `ProcessMedia`; results are sent to your callback.
- **DescribeTaskDetail:** Provide the task ID to query status and results.
- **Console:** Check the VOD processing tasks page; once subtasks succeed, preview or download enhanced outputs.

## Additional enhancement features

Some models require backend configuration. Notable features include:

- **Comprehensive enhancement (optimized):** AI analyses and optimises content, particularly faces, improving clarity and detail.
- **Color enhancement (optimized):** Adjusts saturation, contrast and brightness to correct distortions and bring colours closer to real life.
- **Artifacts removal (optimized):** Repairs block effects, ringing and other distortions introduced by transcoding.
- **Diffusion Transformer video enhancement:** A deep‑learning model ideal for restoring old, severely degraded footage by leveraging prior information from foundation models.

## FAQs and billing

You can create custom enhancement templates via the console or API; use the API to configure transcoding parameters. Billing for enhancement includes both enhancement processing and the underlying transcoding fees.
