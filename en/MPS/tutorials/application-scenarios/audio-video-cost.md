# Audio / Video Cost Optimization Scenario

**Last updated:** 2025-03-21 15:24:03

---

## Overview

Live commerce, online education, remote conferencing, short videos, short dramas, and AI creation trends are driving rapid growth in video content.  
Service providers must balance efficiency and cost. Cost optimization is critical for sustainability and competitiveness.  
Media Processing helps reduce audio and video processing and storage costs.

---

## Requirements

- The surge in video content has increased storage and data transmission costs, requiring technical solutions to reduce expenses.
- Balancing the number of activated features is crucial in audio and video processing to avoid minimal optimization or excessive costs.
- Differentiating video processing based on specific issues can maximize cost benefits.

---

## Our Solutions

### Leading Encoding Compression Capabilities

Supports encoding standards such as **VP8, VP9, H.264, H.265, AV1, AVS3, H.266**, and supports real-time encoding for **4K and 8K**, delivering ultra-high-definition and smooth video experiences.

While ensuring subjective video quality, it saves **up to 50% of bandwidth costs**.  
Over the past three years, it has consistently ranked first in the **MSU Video Coding Competition** and achieved top performance in encoding evaluations.

---

## Transcoding Templates

![Encoding Compression Illustration](image6.png)

Within the **Media Processing Console**, a variety of audio and video transcoding templates are available.  
Each template comes pre-configured with a set of transcoding parameters, allowing quick selection based on business scenarios.

You may also create new templates to customize various parameters. For details on creating templates and configuring parameters, please refer to Audio and Video Transcoding Templates. For information on the costs associated with audio and video transcoding, please contact us.

![Transcoding Evaluation Results](image7.png)

---

## On-Demand Processing Solution

Audio and video services provide high-quality transcoding and an on-demand **Quality Inspection + Transcoding & Enhancement** solution.

To optimize costs:
1. Videos are inspected before transcoding.
2. A suitable transcoding template is selected based on inspection results.
3. Videos without issues skip transcoding, reducing costs.

---

## Features

### Quality Inspection

| Feature | Description | How to use |
|---|---|---|
| Quality Inspection | **Media Quality Inspection supports:**<br><br>• Format quality inspection (DTS, PTS issues, resolution changes, sampling rate changes, frame loss, duplicate frames)<br>• Video & Audio content quality inspection (*JitterResults, BlurResults, AbnormalLightingResults, CrashScreenResults, BlackWhiteEdgeResults, NoiseResults, MosaicResults*)<br>• No-reference quality assessment | Refer to **Media Quality Inspection Integration** documentation |

---

### Transcoding Strategy

| Feature | Description | How to use |
|---|---|---|
| General transcoding / TSC transcoding / Adaptive bitrate streaming | In on-demand scenarios, media assets are inspected first. Videos with format issues or high bitrates are transcoded, while videos without issues skip transcoding, reducing costs. | Refer to **ProcessMedia** documentation |

---

## Evaluating After Transcode

After transcoding, results can be quantitatively evaluated using built-in transcoding evaluation capabilities.

Media Processing supports **VMAF, PSNR, SSIM, and VMAF-NEG** scoring for videos from various sources and formats.

---

### Evaluation Capabilities

| Classification | Feature | Description | How to use |
|---|---|---|---|
| On-demand video | Video quality evaluation | Compares original and transcoded videos.<br>Supports VMAF, PSNR, SSIM, VMAF-NEG.<br>Supports selecting time ranges or frame ranges for evaluation. | Refer to **User Guide** |
| On-demand video | BD-Rate comparison evaluation | Compares transcoding quality across different templates and bitrates.<br>Supports VMAF, PSNR, SSIM, VMAF-NEG.<br>Supports comparing scores at specified bitrates or CRF values. | Refer to **User Guide** |
| Live stream | Image quality | Supports real-time comparison and monitoring of image quality and bitrate changes before and after live stream transcoding. | Coming soon |

---

## Evaluation Results Visualization

![Transcoding Evaluation Results](image8.png)
