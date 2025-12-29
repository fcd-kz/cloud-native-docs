# API Reference

This guide provides an introduction to Media Processing Service (MPS) APIs and how to use them to initiate and manage media processing tasks.

## Overview

Media Processing Service provides comprehensive APIs for media processing operations. All MPS APIs comply with the OpenAPI 3.0 specification and support RESTful calls.

**API Base URL:** `mps.intl.tencentcloudapi.com`

For latency-sensitive operations, you can specify a regional endpoint (e.g., `mps.ap-guangzhou.tencentcloudapi.com` for Guangzhou).

## API Categories

### Processing Task Initiation APIs

These APIs are used to start media processing tasks:

| API Name | Feature | Rate Limit |
|----------|---------|-----------|
| **ProcessMedia** | Initiate single media processing task | 100 req/sec |
| **BatchProcessMedia** | Initiate batch processing from multiple URLs | 20 req/sec |
| **ProcessLiveStream** | Initiate live stream processing task | 100 req/sec |
| **ProcessImage** | Initiate image processing task | 20 req/sec |
| **EditMedia** | Edit video | 20 req/sec |
| **DescribeMediaMetaData** | Get media metadata | 20 req/sec |
| **ExtractBlindWatermark** | Extract digital watermark from video | 20 req/sec |

### Task Management APIs

These APIs are used to query and manage media processing tasks:

| API Name | Feature | Rate Limit |
|----------|---------|-----------|
| **DescribeTaskDetail** | Query task details | 100 req/sec |
| **DescribeTasks** | Get task list | 100 req/sec |
| **DescribeBatchTaskDetail** | Query batch task details | 20 req/sec |
| **ManageTask** | Manage/terminate task | 20 req/sec |
| **DescribeImageTaskDetail** | Query image processing task details | 20 req/sec |

### Template Management APIs

These APIs manage processing templates:

- **Transcoding Templates**: CreateTranscodeTemplate, DeleteTranscodeTemplate, DescribeTranscodeTemplates, ModifyTranscodeTemplate
- **Adaptive Bitrate Templates**: CreateAdaptiveDynamicStreamingTemplate, DeleteAdaptiveDynamicStreamingTemplate, DescribeAdaptiveDynamicStreamingTemplates, ModifyAdaptiveDynamicStreamingTemplate
- **Watermark Templates**: CreateWatermarkTemplate, DeleteWatermarkTemplate, DescribeWatermarkTemplates, ModifyWatermarkTemplate
- **Screenshot Templates**: CreateSnapshotByTimeOffsetTemplate, CreateSampleSnapshotTemplate, CreateImageSpriteTemplate, CreateAnimatedGraphicsTemplate, and delete/describe/modify variants
- **Media AI Templates**: CreateSmartSubtitleTemplate, CreateSmartEraseTemplate, CreateContentReviewTemplate, CreateAIAnalysisTemplate, CreateAIRecognitionTemplate, and variants
- **Quality Control Templates**: CreateQualityControlTemplate, DeleteQualityControlTemplate, DescribeQualityControlTemplates, ModifyQualityControlTemplate
- **Live Recording Templates**: CreateLiveRecordTemplate, DeleteLiveRecordTemplate, DescribeLiveRecordTemplates, ModifyLiveRecordTemplate

### Orchestration/Workflow APIs

These APIs manage automated processing workflows:

| API Name | Feature | Rate Limit |
|----------|---------|-----------|
| **CreateSchedule** | Create orchestration scheme | 20 req/sec |
| **CreateWorkflow** | Create workflow | 200 req/sec |
| **DeleteSchedule** | Delete scheme | 20 req/sec |
| **DeleteWorkflow** | Delete workflow | 20 req/sec |
| **DescribeSchedules** | Query schemes | 20 req/sec |
| **DescribeWorkflows** | Get workflow list | 20 req/sec |
| **EnableSchedule** | Enable scheme auto-trigger | 20 req/sec |
| **EnableWorkflow** | Enable workflow | 20 req/sec |
| **DisableSchedule** | Disable scheme | 20 req/sec |
| **DisableWorkflow** | Disable workflow | 20 req/sec |

### Notification Parsing APIs

| API Name | Feature | Rate Limit |
|----------|---------|-----------|
| **ParseNotification** | Parse offline task notifications | 20 req/sec |
| **ParseLiveStreamProcessNotification** | Parse live stream task notifications | 20 req/sec |

## Getting Started with ProcessMedia API

### Overview

The **ProcessMedia** API is used to initiate a processing task for video URLs or media files in Cloud Object Storage (COS).

Supported features:
- Audio/video transcoding (standard, TSC)
- Audio/video enhancement
- Visible watermark addition
- Digital watermark addition
- Adaptive bitrate streaming
- Video-to-GIF conversion
- Time point screenshot
- Sampled screenshot
- Image sprite generation
- Media quality inspection
- Smart subtitle generation and translation
- Smart content erasing (watermark, subtitle, privacy)
- Smart content moderation (pornography detection, sensitive information)
- Smart content analysis (tags, classification, covers, frame tags, highlights)
- Smart content recognition (faces, text, speech, objects)

### Request Parameters

**Required Parameters:**

- **Action**: String - Value: `ProcessMedia`
- **Version**: String - Value: `2019-06-12`
- **InputInfo**: MediaInputInfo - The information of the file to process

**Optional Parameters:**

- **OutputStorage**: TaskOutputStorage - Target storage for output files
- **OutputDir**: String - Output directory path (must start and end with `/`)
- **MediaProcessTask**: MediaProcessTaskInput - Media processing parameters
- **AiContentReviewTask**: AiContentReviewTaskInput - Content moderation task parameters
- **AiAnalysisTask**: AiAnalysisTaskInput - Content analysis task parameters
- **AiRecognitionTask**: AiRecognitionTaskInput - Content recognition task parameters
- **AiQualityControlTask**: AiQualityControlTaskInput - Quality inspection task parameters
- **SmartSubtitlesTask**: SmartSubtitlesTaskInput - Smart subtitle parameters
- **ScheduleId**: Integer - Orchestration ID for workflow execution
- **TaskNotifyConfig**: TaskNotifyConfig - Event notification configuration
- **TasksPriority**: Integer - Task priority (-10 to 10, default: 0)
- **SessionContext**: String - Pass-through context (max 1,000 characters)
- **ResourceId**: String - Resource ID for resource-level operations
- **SkipMateData**: Integer - Skip metadata acquisition (0: no, 1: yes)

### Response Parameters

- **TaskId**: String - Unique identifier for the processing task
- **RequestId**: String - Unique request ID for locating issues

### Example 1: Initiate Transcoding Task

```json
{
  "InputInfo": {
    "Type": "COS",
    "CosInputInfo": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-chongqing",
      "Object": "movie201907WildAnimal.mov"
    }
  },
  "OutputStorage": {
    "Type": "COS",
    "CosOutputStorage": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-chongqing"
    }
  },
  "OutputDir": "output/",
  "MediaProcessTask": {
    "TranscodeTaskSet": [
      {
        "Definition": 20
      },
      {
        "Definition": 30
      },
      {
        "Definition": 40
      }
    ]
  }
}
```

**Response:**
```json
{
  "Response": {
    "TaskId": "125xxx65-procedurev2-bffb15f07530b57bc1aabb01fac74bca",
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```

### Example 2: Initiate Adaptive Bitrate Streaming Task

```json
{
  "InputInfo": {
    "Type": "COS",
    "CosInputInfo": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-shanghai",
      "Object": "video/lego-city-vehicles.mp4"
    }
  },
  "OutputDir": "share/output/",
  "MediaProcessTask": {
    "AdaptiveDynamicStreamingTaskSet": [
      {
        "Definition": 10,
        "OutputObjectPath": "inputName-adaptiveDynamicStreaming.format",
        "SubStreamObjectName": "inputName-adaptiveDynamicStreaming-{definition}-{subStreamNumber}.format",
        "SegmentObjectName": "inputName-adaptiveDynamicStreaming-{definition}-{subStreamNumber}-{segmentNumber}.format"
      }
    ]
  }
}
```

### Example 3: Initiate Media Quality Inspection Task

```json
{
  "InputInfo": {
    "Type": "COS",
    "CosInputInfo": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-shanghai",
      "Object": "image/lenna.jpeg"
    }
  },
  "OutputStorage": {
    "Type": "COS",
    "CosOutputStorage": {
      "Bucket": "TopRankVideo-125xxx88",
      "Region": "ap-shanghai"
    }
  },
  "OutputDir": "datashare/",
  "AiQualityControlTask": {
    "Definition": 30
  }
}
```

**Response:**
```json
{
  "Response": {
    "TaskId": "2600007696-WorkflowTask-67771a50b24d08baaf6165da23461e36tt7",
    "RequestId": "4a72e698-ec27-4fc1-8e17-c1cbfce1a4a9"
  }
}
```

## Querying Task Status

### DescribeTaskDetail API

Use this API to query the details and status of a completed or ongoing task.

**Request Parameters:**

- **TaskId**: String (Required) - Task ID to query

**Response:**

Returns detailed information including:
- Task status (WAITING, PROCESSING, FINISH)
- Subtask details
- Input information (file path, size, bitrate, duration)
- Output information (file location, resolution, codec)
- Processing progress and timings

### Example Query

```json
{
  "TaskId": "24000089-WorkflowTask-0723542d0c164c958ba116874fa9b0c4"
}
```

**Response:**
```json
{
  "Response": {
    "TaskId": "24000089-WorkflowTask-0723542d0c164c958ba116874fa9b0c4",
    "Status": "FINISH",
    "TaskType": "WorkflowTask",
    "CreateTime": "2025-05-16T07:44:26Z",
    "FinishTime": "2025-05-16T07:44:30Z",
    "RequestId": "147e6b46-efeb-48cf-9186-b195b2bf4f9d"
  }
}
```

## Managing Tasks

### ManageTask API

Use this API to manage running or queued tasks.

**Request Parameters:**

- **TaskId**: String (Required) - Task ID to manage
- **OperationType**: String (Required) - Operation type
  - `Abort`: Terminate the task

**Restrictions:**

- For live stream processing tasks: Can terminate tasks with status WAITING or PROCESSING
- For other task types: Can only terminate tasks with status WAITING

### Example: Terminate Task

```json
{
  "OperationType": "Abort",
  "TaskId": "2459149217-procedure-live-xxx51da009t0"
}
```

## Batch Processing

### BatchProcessMedia API

Use this API to process multiple videos from URLs in a single request.

**Rate Limit:** 20 requests per second

**Features:**
- Smart subtitle generation with speech recognition and translation
- Input from multiple URL sources
- Batch output to single location

### Example: Batch Subtitle Generation

```json
{
  "InputInfo": [
    {
      "Type": "URL",
      "UrlInputInfo": {
        "Url": "https://test-xxx-125xxxxx.cos.ap-xxxxx.myqcloud.com/processmedia52.mp4"
      }
    }
  ],
  "OutputStorage": {
    "Type": "COS",
    "CosOutputStorage": {
      "Bucket": "test-xxxx-125xxxxx",
      "Region": "ap-xxxxx"
    }
  },
  "OutputDir": "output/",
  "SmartSubtitlesTask": {
    "RawParameter": {
      "SubtitleType": 2,
      "VideoSrcLanguage": "zh",
      "SubtitleFormat": "vtt",
      "TranslateSwitch": "ON",
      "TranslateDstLanguage": "en"
    }
  },
  "TaskNotifyConfig": {
    "NotifyType": "URL",
    "NotifyUrl": "http://xxxx.com/v2/pushmps?token=73YcsZyP"
  }
}
```

**Response:**
```json
{
  "Response": {
    "TaskId": "24000030-BatchTask-e6fefa34fc497449c1a043b9a594c7det20",
    "RequestId": "b30891cd-cdc7-47db-94d3-4dbb85641dad"
  }
}
```

## Live Stream Processing

### ProcessLiveStream API

Use this API to initiate real-time processing of live streams.

**Rate Limit:** 100 requests per second

**Supported Features:**
- Smart moderation (pornography, sensitive information detection)
- Intelligent identification (faces, objects, text, speech, translation)
- Intelligent analysis (news segmentation, real-time features)
- Quality inspection (format diagnosis, content detection, no-reference scoring)
- Live stream recording

## Developer Resources

### SDKs

TencentCloud API 3.0 provides SDKs for multiple programming languages:

- Tencent Cloud SDK 3.0 for Python
- Tencent Cloud SDK 3.0 for Java
- Tencent Cloud SDK 3.0 for PHP
- Tencent Cloud SDK 3.0 for Go
- Tencent Cloud SDK 3.0 for Node.js
- Tencent Cloud SDK 3.0 for .NET
- Tencent Cloud SDK 3.0 for C++

### Command Line Interface

- Tencent Cloud CLI 3.0

### API Explorer

Use the [API Explorer](https://cloud.tencent.com/api/explorer) tool to:
- Call APIs online
- Generate SDK code
- Test authentication and signatures
- View sample requests and responses

## Common Error Codes

| Error Code | Description |
|-----------|-------------|
| `FailedOperation.InvalidMpsUser` | Operation failed: unauthorized MPS user |
| `InternalError` | Internal service error |
| `InvalidParameterValue` | Incorrect parameter value |
| `InvalidParameterValue.Limit` | Invalid limit parameter |
| `InvalidParameter` | Invalid parameter format |
| `UnauthorizedOperation` | User not authorized |

## Best Practices

1. **Use Templates**: Create and reuse templates for consistent processing parameters
2. **Batch Processing**: Use BatchProcessMedia for processing multiple files efficiently
3. **Event Notifications**: Configure TaskNotifyConfig to receive task completion notifications
4. **Error Handling**: Implement proper error handling for failed tasks
5. **Resource Management**: Use ResourceId to track and allocate costs
6. **Rate Limiting**: Respect API rate limits and implement backoff strategies
7. **Orchestration**: Use workflows for complex multi-step processing pipelines

## Related Topics

- [Getting Started Guide](/docs/MPS/quickstart)
- [Transcoding Tasks](/docs/MPS/operations/transcoding)
- [Video Enhancement](/docs/MPS/operations/enhancement)
- [Live Stream Recording](/docs/MPS/operations/live-recording)
