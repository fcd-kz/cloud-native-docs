# Cloud Streaming Service — Key Concepts

This section explains important terms used in live streaming and cloud streaming workflows.

---

## Push

Refers to the process in which the host pushes local video and audio sources to the **Cloud Streaming Service** servers. It is also known as **RTMP push** in some cases.

---

## Playback

Refers to live playback in which source video and audio are pulled from the **Cloud Streaming Service** servers and played back at the specified address after live push is implemented.

The video source is generated in real time and is only meaningful if someone is pushing a live stream. Once the host stops streaming, the live streaming URL becomes invalid. Since live streams are played back in real time, no progress bar is displayed during playback.

---

## Push Domain Name

The domain name used to push live streams. This is a required setting. You must register the domain name before using it for live streaming. After a push domain name is configured, the Cloud Streaming Service generates the corresponding push URL.

---

## Playback Domain Name

The domain name used to play back live streams. This is also a required setting. You must register the domain name before using it. After configuration, the Cloud Streaming Service generates the corresponding playback URL.

---

## Domain CNAME

A system-assigned domain name used for acceleration. You must configure a CNAME record with your domain service provider. Once the record takes effect, the Cloud Streaming Service handles domain resolution, and all requests are forwarded to edge servers.

---

## StreamName

The unique identifier of a stream. The **StreamName** combined with the domain name uniquely identifies a live stream.

---

## AppName

The live streaming application name used to identify the storage path of a live streaming media file. The default application name is **live**, and it is customizable.

---

## Transcoding

Transcoding is an offline task that converts one video bitstream into another. It changes codec, resolution, bitrate, and other parameters to support playback on different devices and network conditions.

**Benefits:**
- Improves compatibility across devices  
- Adapts to network bandwidth conditions  
- Reduces bandwidth usage while maintaining quality  

---

## H.264

A widely used digital video compression standard developed for efficient video encoding.

**Advantages:**
- Supports SD video transfer below 1 Mbps  
- Delivers good image quality at moderate bandwidth  

---

## H.265

An improved version of H.264 with higher compression efficiency.

**Advantages:**
- Supports HD video transfer at 1–2 Mbps  
- Optimizes bitrate, encoding quality, latency, and complexity  

---

## Event Message Notification

When an event is triggered during a live push, the Cloud Streaming Service sends a request to your server based on the configured message template. Your server authenticates and responds to the request, then receives a JSON packet containing callback information for processing.

---

## Referer

A security parameter in push and playback URLs used to prevent unauthorized URL generation and stream theft.

---

## Live Recording

During live push, original stream data can be stored on the Video on Demand (VOD) platform without modifying audio/video data or timestamps.

---

## Watermark

To protect video copyright, a watermark can be added during transcoding. The watermark can be text or an image.

---

## Screencapture

Captures video frames from live streams at specified intervals and stores them as image files in object storage. Permissions must be granted for storage access.

---

## 95th Percentile Bandwidth

Bandwidth billing method where peak bandwidth is sampled every 5
