# Getting Started with Freedom Cloud Media Processing Service (MPS)

The Media Processing Service (MPS) is a cloud‑based platform for offline audio/video processing and live stream media processing. This guide explains how to register, authorize resources, and begin running offline and live tasks.


## Operation steps

MPS supports **offline file processing** and **live stream processing**.

### Offline file processing

#### Step 1: Initiate a task

You can start an offline task in three ways:

1. **Quickly create a task in the console.**
   - Navigate to the console and click **Create Offline Processing Task**.
   - **Specify an input file:** choose a file from COS or Amazon S3 or enter a download URL.
   - **Scheme processing workflow:** add feature nodes (e.g., transcoding, enhancement, screencapturing) and choose either a preset template or custom parameters.
   - **Specify the output path:** define where processed files should be saved. You can customise the output path for specific nodes (e.g., screencapturing) under *More Settings > Custom Screencapturing Output Path*.
   - Confirm and create the task.

2. **Automatically trigger a task.**
   - On the *Offline Orchestration* page, create an orchestration and configure the trigger bucket/directory and output bucket/directory.
   - Enable auto‑trigger for the orchestration. New files uploaded to the trigger directory automatically initiate processing. Only new uploads are processed; existing files are not.

3. **Initiate via API.**
   - Use the **ProcessMedia** API to launch a task programmatically; this approach is suitable for batch processing or integration with existing systems.

#### Step 2: Manage tasks

- Visit the *Offline Task Management* page to view a list of initiated tasks. You can filter by status or Task ID, restart queued tasks, play the source video, or download outputs.
- Expanding a task shows subtask details and output files.

### Live stream processing

#### Step 1: Initiate a task

Two methods are available:

1. **Quickly create a task in the console.**
   - On the console task creation page, click **Create Live Processing Task**.
   - Configure the **live stream URL**, choose a scheme (for recording, moderation, enhancement, etc.), and set an output path.
   - The console supports real‑time recording. Make sure the stream address is correct; if the pull fails, MPS retries three times. Persistent failure causes the recording task to fail.

2. **Initiate via API.**
   - Call **ProcessLiveStream** to create a live processing task. The API can perform smart moderation, intelligent identification (faces, objects, text and speech, with translation and game tagging), intelligent analysis, quality inspection and live stream recording.

#### Step 2: Manage tasks

- Navigate to *Live Stream Task Management* to view and manage live tasks. You can inspect details, terminate tasks and more.
