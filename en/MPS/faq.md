# FAQ

Frequently asked questions about Media Processing Service (MPS) and troubleshooting common issues.

## Basics

### Concepts

**Q: What Is MPS?**

Media Processing Service (MPS) is a cloud-based transcoding and audio-video processing service capable of handling vast amounts of data. You can use it to transcode your videos stored in Tencent Cloud COS or AWS S3 to make them suitable for OTT services or playback on PC and mobile devices. You can also transcode videos to different bitrates and resolutions for different platforms. Other services MPS offers include watermarking, video screenshot, audio and video enhancement, intelligent analysis, intelligent recognition, live broadcasting recording, and more.

**Q: What Is Video Bitrate?**

Video bitrate is the number of data bits transferred per unit time. It is often measured in Kbps (kilobits per second).

Formula: **Bitrate (Kbps) = File size (KB) × 8 ÷ Transfer time (s)**

**Q: What Is TESHD in MPS?**

TESHD (Top Speed Codec High Definition) is a process where videos are processed to reduce bandwidth usage while retaining or improving video quality. It allows you to deliver higher-definition videos to your users with less bandwidth usage.

**Q: Does MPS Use Hardware or Software for Decoding?**

MPS offers video processing services such as on-cloud transcoding, watermarking, thumbnail generation, and audio and video enhancement. It does not offer decoding services.

### Features

**Q: Does MPS Provide Test Accounts?**

No, it does not. If you have test requirements, you can contact Tencent Cloud's business team to apply for testing vouchers.

**Q: What Screenshot Taking Modes Does MPS Support?**

MPS supports:
- Time point screenshot (single screenshots)
- Sampled screenshot (multiple screenshots)
- Image sprite screenshot
- Animated screenshot

For details, refer to the Screenshot Template documentation.

**Q: Does It Support Conducting Multiple Processing Tasks on a Single Input Source Simultaneously?**

Yes, you can add multiple processing nodes within the orchestration to perform different operations on the same input file.

**Q: Does MPS Support Video Splicing?**

Yes, it does. You cannot splice videos via the console, but you can call the **EditMedia** API to splice videos programmatically.

**Q: Is It Possible to Convert the Audio in a Video into Text?**

Yes. After performing content recognition on a video through MPS Video Content Recognition, the outcome provides text recognized from the video's audio. Refer to Intelligent Video Recognition for detailed instructions.

**Q: Can the Intelligent Cover Be Set as an Animated Image?**

The intelligent cover extraction selects one or several screenshots from the video as the recommended cover. It does not support automatic generation of animated images through this feature.

If you require an animated cover, you can:
1. Create a highlight video clip intelligently using the Intelligent Analysis - Highlight Clipping feature
2. After selecting an appropriate segment, use the Animated Screenshot feature to obtain an animated image

**Q: Can Multiple Output Directories Be Configured in the Orchestration Simultaneously?**

Yes. Taking the audio/video transcoding node as an example, you can configure it under **More Settings > Customize Transcoding Output Path**. This feature also allows you to modify the naming convention of the output files using filename variables.

**Q: Does MPS Support Video Segmentation?**

Yes. When the packaging format is set to HLS, you can configure segmentation format and data splitting format:
- **Segment File (segment)**: Multiple segment files
- **Single File (single-file)**: Single file with byte range requests (note: not all HLS devices and players support single file/byte ranges)

**Q: Does MPS Support HDR?**

Yes. The audio/video enhancement feature supports HDR activation and allows switching between two modes:
- **HDR10**
- **HLG** (Hybrid Log-Gamma)

Note: Using HDR requires the encoding standard to be set to H.265. Failure to do so will result in processing task failure.

## Account Authorization

### Scenario 1 (Required): MPS Service Not Enabled for an Account

**Problem:** If the MPS service is not enabled for your account, you cannot use MPS normally.

**Solution:**
1. Contact the root account owner and log in with the root account
2. Go to the MPS console and click **Activate For Free**

Alternatively, if a sub-account has full read/write permissions for MPS, it can directly enable MPS under the sub-account.

### Scenario 2 (Required): No MPS Operation Permissions for a Sub-account

**Problem:** Error message: "You do not have permission to operate Media Processing Service - DescribeUserInfo" or "AuthFailure. Unauthorized Operation"

**Solution 1: Associate the Sub-account with QcloudMPSFullAccess Policy (Recommended)**

1. Contact the root account owner and log in with the root account
2. Go to Cloud Access Management > Users
3. Find the sub-account that needs to use MPS
4. Click **Authorize** and search for **QcloudMPSFullAccess**
5. Grant the QcloudMPSFullAccess preset policy to the sub-account

**Solution 2: Associate the Sub-account with a Custom Policy**

1. Go to Cloud Access Management > Policies under the root account
2. Click **Create Custom Policy** and select **Create by policy builder**
3. Select **Media Processing Service (mps)** as the service
4. Choose the required actions (Read, Write, or specific operations)
5. Select **All resources** under Resource
6. Enter a policy name
7. Grant this permission to the sub-account in the "Authorize this permission to the user" field
8. Click **Done**

### Scenario 3 (Optional): MPS Not Authorized to Perform Read/Write Operations on Files in Your Buckets

**Problem:** Tasks fail when trying to access COS or VOD Pro files without proper authorization.

**Solution:**

**For COS:**
1. Log in with the root account
2. Go to MPS console overview page
3. Click **COS Authorization** and click **Authorize** in the pop-up window
4. The **MPS_QcsRole** service role will be automatically created

**For VOD Pro:**
1. Log in with the root account
2. Go to MPS console overview page
3. Click **VOD Authorization**
4. The **MPS_QCSLinkedRoleInVOD** service role will be automatically created

**For AWS S3 or URL:**
- COS authorization can be skipped
- Ensure URLs are publicly accessible and support direct download

> **Note:** These authorization operations do not require enabling COS/VOD and will not incur COS/VOD fees. They only grant MPS the necessary API read/write permissions for your buckets.

### Scenario 4 (Optional): No cam:GetRole Permission for a Sub-account

**Problem:** Error message: "You do not have permission to operate on resource role/xxxx Get Role Detail"

**Explanation:** The MPS console frontend calls the GetRole API to query if the user has the MPS_QcsRole service role. If the sub-account lacks cam:GetRole permission, the console cannot query the role and displays an error. Note: APIs can still be called; this only affects console access.

**Solution:**

1. Contact the root account owner and log in with the root account
2. Go to Cloud Access Management > Policies
3. Click **Create Custom Policy** and select **Create by policy generator**
4. Select **Cloud Access Management (CAM)** for Service
5. Select **GetRole** as the read operation
6. Select **All resources**
7. Enter a policy name
8. Grant this permission to the sub-account
9. Click **Complete**

## Task Configuration

**Q: How Do I Receive Callbacks?**

MPS supports callback notification methods based on:
- Message queues (CMQ)
- Cloud functions (SCF)
- HTTP push

**Q: What Do I Do If I Do Not Receive Callbacks?**

Possible reasons:
1. The workflow was not set up correctly - verify workflow settings
2. If you initiated the transcoding task via API, use the **DescribeTaskDetail** API to query task progress
3. Message backlog in the task queue - submit a ticket to check your queue status

**Q: How Do I Set Up Callback?**

For detailed instructions, refer to Configuring Event Callback Notification.

**Q: Is There a Fee Associated with Using Callbacks?**

- **CMQ-related usage**: See CMQ Cost Description
- **Serverless Cloud Functions (SCF)**: See SCF Billing Overview
- **HTTP push method**: Currently free of charge

**Q: How to Configure Automatic Trigger Tasks?**

1. Complete orchestration configuration
2. Navigate to **Orchestrations > Offline Orchestration** page
3. Click **Enable** to activate the automatic trigger feature
4. Files uploaded to the trigger bucket will be automatically processed

## Task Initiation

**Q: What Should I Do If Automated Triggering Is Enabled in Orchestration, but Tasks Are Not Automatically Initiated?**

Possible reasons and solutions:

1. **Upload failed**: If file upload to COS failed (4XX or 5XX error), no COS event notification is triggered
   - Solution: Check whether the file is successfully uploaded to COS

2. **Upload succeeded but automatic processing not triggered**: Possible scenarios include incorrect orchestration settings
   - Solution: Verify and ensure that the orchestration is configured accurately

**Q: What Should I Do If Initiating a Task Fails?**

Possible causes:

1. **Incorrect request parameters**: Check API parameters and ensure the API call is successful
2. **No authorization**: Check whether you have granted MPS permissions to COS and CMQ resources
3. **Permission errors**: Verify proper account and sub-account authorization

**Q: What Should I Do If a Task Was Successfully Initiated but Failed During Processing?**

Task failure can occur in any subtask (transcoding, screen capturing, watermarking, intelligent recognition, intelligent analysis).

**Solutions based on error type:**

1. **Incorrect source file metadata or unsupported format**
   - Verify the accuracy of file metadata and encoding parameters
   - Check that the file format is supported

2. **Incorrect template parameter configuration**
   - Review and correct template settings

3. **Other error types**
   - Submit a ticket for assistance

**Q: Will Having the Trigger Directory and Output Directory as the Same Cause a Loop Trigger?**

No. If the orchestrated trigger directory and output directory are the same file path, it will **not** cause a loop trigger.

**Q: What Is the Maximum Number of Concurrent Transcoding Channels?**

The default limit for concurrent transcoding channels is **60**. To increase this quota, submit a ticket.

## Task Result Viewing

**Q: How to Obtain Media Metadata?**

Use the **DescribeMediaMetaData** API to retrieve detailed information about your media files.

**Q: Can I Query Newly Finished Tasks Using ScrollToken?**

You may not be able to query newly finished tasks using the pagination flag parameter **ScrollToken** because tasks are returned sorted by creation time.

> **Note:** ScrollToken is used for pagination. If not all tasks can be returned in one request, the API returns ScrollToken. Pass it in the next request to continue from the next record.

**Q: How to Query the Task List?**

Use the **DescribeTasks** API. Tasks are returned sorted by creation time.

**Q: How to Add Animated Watermarks?**

1. Convert animated images into APNG format
2. Add them as watermarks in workflow settings

**Q: How to Modify a Watermark Template?**

Use the **ModifyWatermarkTemplate** API to modify watermark templates.

**Q: How to Associate MPS with COS Buckets?**

When configuring a workflow, select a trigger bucket. Videos uploaded to the selected bucket will be processed automatically. Refer to Workflow Management for more information.

**Q: OCR Results Are Generated for a Video Frame. How Do I Get the Frame in Question?**

1. Note the time point when OCR results are generated
2. Use the **ProcessMedia** API with the **SnapshotByTimeOffsetTaskInput** parameter
3. Pass the time point to take a screenshot at that specific moment

**Q: How to Query Statistical Data?**

1. Log in to the Media Processing Service Console
2. Click **Usage Statistics** to access detailed statistical data
3. View resource usage by type (transcoding, enhancement, etc.)
4. Monitor cost trends

## Troubleshooting Checklist

When experiencing issues with MPS:

- [ ] Verify MPS service is activated on your account
- [ ] Confirm user/sub-account has appropriate permissions
- [ ] Check COS/VOD Pro authorization is completed
- [ ] Verify input files are accessible and in supported formats
- [ ] Review task configuration and template parameters
- [ ] Check workflow orchestration is properly configured
- [ ] Verify trigger and output bucket settings are correct
- [ ] Use **DescribeTaskDetail** API to check task status and error messages
- [ ] Review callback notification configuration
- [ ] Submit a ticket if error persists

## Related Topics

- [Getting Started Guide](/docs/MPS/quickstart)
- [Transcoding Tasks](/docs/MPS/operations/transcoding)
- [API Reference](/docs/MPS/index/api-ref)
- [Pricing](/docs/MPS/index/pricing)
