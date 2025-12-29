# Live Stream Recording Integration

## Overview

The live stream recording feature of MPS captures streaming content and saves it as files for on‑demand playback. This integration guide explains how to set up templates, schemes, and tasks to record live streams.


## Steps to configure live recording

### Step 1 – Create a live recording template

A template defines how the stream is recorded and saved. When creating a live recording template, set parameters such as:
- Recording container (e.g., HLS or MP4).
- Segment duration (for HLS).
- Recording file naming pattern.

### Step 2 – Create a live processing scheme

A scheme binds the template to a specific input source and output destination. To create one:
1. Choose the source COS bucket and directory where the original stream will be ingested.
2. Add a “Live Recording” step and select the recording template created earlier.
3. Define the output COS bucket and path where the recorded files will be stored.
4. Keep the automatically generated random string in the output path—removing it may cause multiple tasks to overwrite each other.

### Step 3 – Initiate the live recording task

Once a scheme is ready:
1. Go to the **Live tasks management** page in the MPS console.
2. Click **Create task** and enter the URL of the live stream you wish to record.
3. Select the scheme created in Step 2.
4. Submit the task. MPS will pull the stream, record segments according to the template, and save them to the specified output path.

**Note:** The system attempts to pull the live stream three times. If it cannot fetch the stream after three retries, the recording task fails.

## Managing live recording tasks

All active and completed recording tasks appear in the **Live tasks management** list. You can:
- Check the status (in progress, completed, failed).
- View details such as start/end times and file sizes.
- Stop a running task manually if needed.

## Best practices

- Use short segment durations (e.g., 5–10 seconds) for HLS to ensure that live recordings play smoothly when delivered as on‑demand streams.
- Store recordings in buckets separate from your original live stream source to avoid accidental overwrites.
- Monitor tasks via the console or API and set up callbacks for automatic notifications when recordings finish.

