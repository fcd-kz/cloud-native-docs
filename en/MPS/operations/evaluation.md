# Video Quality Evaluation

## Overview

Quality evaluation measures the visual fidelity of processed videos. MPS provides objective scoring tools that compare an original video with a processed version, helping developers verify improvements or regressions in encoding, enhancement and other processing steps. Evaluations can also be performed on a single video without a reference to estimate overall quality.

## Capabilities

- **Objective metrics:** Supports metrics such as VMAF (Video Multimethod Assessment Fusion), PSNR (Peak Signal‑to‑Noise Ratio), SSIM (Structural Similarity) and VMAF‑NEG (an extended VMAF variant). These metrics estimate how close the processed video is to the original.
- **BD‑Rate calculation:** Computes the bitrate saving (Bit‑Difference Rate) between two encoding settings while maintaining similar quality.
- **Flexible segmentation:** Allows evaluation of a full video or specific time segments (e.g., 00:02:00–00:05:00) for more targeted analysis.
- **Cross‑format comparison:** Evaluates videos of different resolutions or codecs to compare quality when down‑converting or re‑encoding.

## Creating evaluation tasks

1. **Console:** Navigate to “Quality Evaluation” in the MPS console and click **Create Task**. Upload or select the original and comparison videos from COS. Choose a metric (VMAF, PSNR, SSIM) and optional settings such as frame sampling rate and evaluation range. Assign an output directory and submit.
2. **API:** Use `ProcessMedia` with an `AiQualityControlTask` or `VideoQualityEvaluationTask` parameter. Provide the template ID (or choose default metrics) along with the input and reference videos. Specify output storage and path, and configure callback notifications.
3. **Automatic orchestration:** Incorporate evaluation tasks into a workflow—for example, after transcoding or enhancement—to automatically generate reports for each processed file.

## Interpreting results

Evaluation results typically include:

- **Overall score:** Numerical values for each metric (e.g., VMAF score of 92).
- **Per‑frame analysis:** A timeline of metric values across the evaluated segment, highlighting peaks and dips.
- **BD‑Rate:** A percentage indicating bitrate savings or increases between encoding configurations.

Higher VMAF and SSIM scores indicate better perceived quality, while lower BD‑Rate values indicate greater efficiency.

## Best practices

- **Use high‑quality references:** The reference video should be the highest‑quality available version. Evaluation accuracy is limited by reference fidelity.
- **Choose appropriate metrics:** For perceptual quality, VMAF is more reliable; PSNR and SSIM are simpler but less aligned with human perception.
- **Segment long videos:** Evaluating entire multi‑hour videos can be computationally expensive. Focus on critical scenes or representative segments.
- **Compare across resolutions with caution:** If resolutions differ, upsample or downsample to a common resolution before evaluating to avoid misleading results.

