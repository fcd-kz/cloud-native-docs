# Video Screencapturing Integration

## Overview

Screencapturing is an offline task that captures an image from a video at a specific time. MPS supports multiple screenshot modes:

- **Time‑point screenshot:** takes screenshots at specified timestamps.
- **Sampled screenshot:** captures frames at regular intervals.
- **Image sprite:** captures a set of screenshots at intervals and splices them into a single image.
- **Animated screenshot:** converts a video segment into an animated GIF or WebP.

Common use cases include generating video thumbnails, creating highlight collections, assisting manual moderation, assembling video summaries and providing preview thumbnails on player progress bars.

## Screenshot templates

Screenshots are configured through **templates**. You can use preset templates or create custom ones in the console. Key parameters include:

### Time‑point screenshot templates

- **Format:** output format (currently only JPG).
- **Width and Height:** dimensions in pixels (128–4096).
- **FillType:** how to handle mismatched aspect ratios – options include **Scale to fill** (stretch), **Black bars**, **White bars** and **Gaussian blur**.

### Sampled screenshot templates

- Same fields as time‑point templates (format, width, height).
- **SampleType:** defines how intervals are measured – either **by percent** (e.g., Interval = 5 %) or **by time** (e.g., Interval = 10 s).
- **Interval:** value for the chosen measurement.
- **FillType:** same options as above.

### Image sprite templates

- **Format:** currently only JPG.
- **Width/Height:** size of each sub‑image.
- **Rows/Columns:** number of rows and columns in the sprite.
- **SampleType:** currently only time‑based sampling.
- **Interval:** sampling interval (seconds).
- Ensure that width × columns and height × rows both fall within 128–4096 pixels.

### Animated screenshot parameters

- **Format:** GIF or WebP.
- **Width/Height:** dimensions (128–4096 px).
- **FPS:** frames per second (1–60).

## Initiating screenshot tasks

You can start screenshot tasks through the API or console:

1. **API:** Call **ProcessMedia** and specify the screenshot template ID in `MediaProcessTask.SnapshotByTimeOffsetTaskSet`. For sampled screenshots, use `SampleSnapshotTaskSet`. For sprites, use `ImageSpriteTaskSet`. You can trigger screenshot tasks when uploading videos by setting the `procedure` parameter to the name of a task flow created in the console.
2. **Console:** Create a task flow in the console, add a screenshot step and configure template parameters; run the flow against selected videos or set it as an automatic procedure applied to uploaded videos.

## Getting the result

Once a screenshot task finishes, you can:

- **Listen for notifications:** Provide `TaskNotifyConfig` when calling `ProcessMedia` to receive asynchronous callbacks. The callback includes the Task ID, file information and result sets for each screenshot type. Each entry lists the time offsets and URLs of the generated images.
- **Query via API:** Use `DescribeTaskDetail` with the Task ID to synchronously retrieve the status and result.
- **Console:** The VOD task management page lists screenshot tasks; you can preview or download the images.

## Best practices

- **Select appropriate templates:** choose time‑point templates for thumbnails, sampled templates for moderation or highlight extraction, and sprite templates for summarizing long videos.
- **Set fill modes carefully:** using black/white bars or Gaussian blur preserves aspect ratio without distortion.
- **Automate through task flows:** create and save task flows in the console and attach them to upload procedures so that new videos are processed automatically without manual intervention.
