# Media AI Integration

Freedom Cloud Native's Media Processing Service offers advanced AI capabilities that automate transcription, highlight extraction, summarization and region‑of‑interest (ROI) tracking. This guide covers integration methods for Smart captions and subtitles, Intelligent highlights, LLM summarization and ROI intelligent recognition.

## Prerequisites

- Activate the Media Processing Service and ensure your account has access to COS.
- For live-stream features, activate StreamLive and authorize MPS to access StreamLive data.
- Create or select AI templates in the console, or record their template IDs if using the API.

## Smart captions and subtitles

### Overview

Smart captions convert spoken words into subtitles via Automatic Speech Recognition (ASR) and optionally translate them into different languages. The system supports hundreds of languages and allows you to embed subtitles directly into videos or output them as separate files. Subtitle styles (font, size, colour, background and position) are fully configurable.

### Key advantages

- **Comprehensive platform support:** Works with on-demand files, live streams and interactive RTC streams. Live captioning offers steady and gradient modes without changing the player.
- **High accuracy:** Leverages large-scale models and supports hotword and terminology lexicons.
- **Rich language variety:** Recognises mixed-language speech (e.g., Chinese and English) and supports multiple dialects.
- **Customizable styles:** Adjusts font, colour, position and background.

### Creating tasks

1. **Console:** On the MPS console, click **Create VOD Processing Task**. Choose an input file, add the Smart Subtitle node in the workflow, select a preset or custom template, set output storage and create the task.
2. **API:** Call `ProcessMedia` with `SmartSubtitlesTask.Definition` set to the template ID. Specify `InputInfo`, `OutputStorage`, `OutputDir` and (optionally) `TaskNotifyConfig` for callbacks.
3. **Automatic trigger:** Create an on‑demand orchestration with a Smart Subtitle node, set a trigger bucket and directory, and enable it. New uploads automatically start subtitle tasks.

## Intelligent highlights

### Overview

Intelligent highlights automatically extract the most engaging segments of a video (e.g., goals in sports, dramatic moments in films) using AI models that align image and text features. Highlights improve viewing experience and are ideal for previews and social sharing.

### Creating tasks

1. **Console:** Create a processing task or schedule, insert an AI Analysis node and select the preset Intelligent Highlights template.
2. **API:** Call `ProcessMedia` with `AiAnalysisTask.Definition` set to the preset template ID (often 26). Use `ExtendedParameter` for fine-tuning, such as specifying the number of clips (`top_clip`), categories (`force_cls`), voice activity detection (`need_vad`), similarity threshold and merging behaviour.
3. **Callbacks and queries:** Set `TaskNotifyConfig` for result notifications, or poll `DescribeTaskDetail` with the Task ID.

## LLM summarization

### Overview

LLM summarization leverages large language models to summarise video content. It segments videos into logical units and produces concise textual summaries. This is useful for educational courses, news recaps and knowledge extraction.

### Creating tasks

1. **Console (via schedule):** Create an orchestration with an AI Analysis node and choose the preset LLM Summarize template.
2. **API:** Call `ProcessMedia` with `AiAnalysisTask.Definition` set to the LLM summarization template ID (commonly 22). `ExtendedParameter` accepts settings such as:
   - `split.method`: segmentation method (llm or nlp).
   - `split.model`: choose a model (e.g., Hunyuan, DeepSeek-V3).
   - `need_ocr`: enable OCR to incorporate on-screen text.
   - `text_requirement`: constraints for summary length or content.
   - `dstlang`: language of the summary.
3. **Output and notifications:** Specify `OutputStorage` and `OutputDir` for result files; set up callbacks or query the task status via `DescribeTaskDetail`.

## ROI intelligent recognition

### Overview

Region of interest recognition identifies important visual elements—faces, game characters or hosts—in real time. This information can be sent to the playback device, enabling features like:

- Automatically blurring the background to focus on the main subject.
- Preventing on-screen comments from covering key elements.
- Guiding horizontal-to-vertical transformations by centering on relevant areas.

### Integration

ROI recognition is typically used within other tasks (e.g., vertical transformation or intelligent cropping). To enable it:

1. Create a template with ROI detection enabled (often available in the horizontal-to-vertical transformation settings).
2. Use the console or API to initiate tasks with ROI recognition. When using the API, include the appropriate parameters in the `AiAnalysisTask` or specific cropping API.
3. The output includes coordinate data for each frame that indicates the ROI position.

## Best practices

- **Combine features judiciously:** For example, generate subtitles and summaries in one pipeline to improve accessibility and comprehension.
- **Tune parameters:** Extended parameters let you control clip length, segmentation models and thresholds; test these values to match your content.
- **Automate workflows:** Save orchestration templates and enable triggers so new uploads automatically generate subtitles, highlights and summaries.
- **Monitor costs:** AI tasks incur additional fees beyond standard transcoding. Choose the appropriate number of clips, summary length and languages to balance quality and cost.

By integrating Media AI functions into your workflow, you can enhance content discovery, accessibility and engagement at scale.

