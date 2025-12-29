# Content Auditing Integration

## Overview

Content auditing (also known as intelligent auditing) helps you detect inappropriate or illegal content in videos, audio and embedded text. It uses AI models to identify explicit imagery, violent scenes, weapons and other objectionable material. By integrating auditing, you can automatically filter user‑generated content, comply with regulations and improve the safety of your platform.

## Detection types

Auditing covers three areas:

- **Video image auditing:** Scans each video frame for inappropriate imagery. Categories include pornographic content, vulgar or sexually suggestive scenes, intimate behaviour, weapons (guns), bloody or violent scenes, explosions and banned icons or logos.
- **Audio auditing:** Listens to speech and other sounds to detect keywords related to erotica, violence or illegal activity. Custom keyword lists can be configured to improve accuracy for specific domains.
- **Text auditing:** Extracts on‑screen text (via OCR) and checks for banned or sensitive words. It works even with vertical or stylised text.

## Initiating an auditing task

Auditing tasks can be created in three ways:

1. **Console:** Create a new VOD processing task, add an “Intelligent Auditing” node and select a preset template or customise detection categories. Specify input source (COS or URL) and output directory, then submit the task. For recurring workflows, save the configuration as an orchestration.
2. **API:** Call `ProcessMedia` with an `AiContentReviewTask` parameter containing the template ID and desired detection types. Provide the input source, output storage and output path. Configure `TaskNotifyConfig` to receive callback notifications when the task completes.
3. **Automatic trigger:** Create an on‑demand orchestration with an auditing node and enable it. When new media files appear in the trigger bucket, auditing tasks automatically start.

## Reviewing results

- **Callback notifications:** When a task finishes, MPS sends a JSON notification containing the result. The event includes lists of time segments where violations were detected.
- **Console:** In the VOD processing tasks page, open a completed task to view the auditing report. The report shows each violation with start/end timestamps, category and confidence score.
- **API query:** Use `DescribeTaskDetail` with the task ID to retrieve the auditing results programmatically.

## Best practices

- **Choose templates wisely:** Different content categories require different detection thresholds. Use a custom template if preset templates are insufficient.
- **Combine with quality inspection:** Run quality inspection before auditing to ensure the video is decodable; corrupted files can trigger false positives.
- **Handle false positives:** Review flagged segments manually for critical content. Adjust thresholds or keyword lists based on false positive feedback.
- **Integrate with moderation tools:** Use callbacks to trigger downstream moderation workflows—e.g., automatically block content, request manual review, or notify creators.

