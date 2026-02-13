# SDK Integration Guide

**Last Updated:** 14 Oct 2024  
**Applies to:** Mobile Apps, Web Platforms  

This document describes how to integrate a **cloud-based live streaming SDK** to enable **live video push (broadcast)** and **live playback** across mobile and web platforms.

The SDK provides a stable, low-latency streaming infrastructure suitable for real-time communication, live events, education, broadcasting, and interactive sessions.

---

## 1. Overview

The SDK enables:

- Real-time **video/audio capture and broadcast**
- Multi-protocol **live playback**
- **Low-latency interactive streaming**
- Support for **multi-party interaction** (e.g., co-hosting)

It can be integrated into:

- **Mobile Applications** (iOS / Android)
- **Web Applications** (Browsers)

---

## 2. Mobile App Integration (iOS & Android)

The mobile SDK supports both **live stream publishing** and **live stream playback**.

### 2.1 Live Stream Publishing (Mobile Push)

Mobile devices can capture video/audio and publish streams to the cloud streaming service.

**Supported capture sources:**

- Device camera (front or rear)
- Device microphone
- Screen capture (screen recording / screen sharing)

**Publishing protocol:**

- **RTMP** (Real-Time Messaging Protocol)

**Typical use cases:**

- Mobile live broadcasting  
- Game streaming from device screen  
- Remote reporting  
- Online teaching from smartphones  

---

### 2.2 Live Stream Playback (Mobile Pull)

Mobile apps can play live streams using multiple playback protocols.

**Supported playback protocols:**

- **RTMP** – low latency
- **HTTP-FLV** – low latency over HTTP
- **HLS (HTTP Live Streaming)** – high compatibility, adaptive bitrate

This allows developers to build:

- Live viewing apps  
- Event streaming apps  
- Interactive classrooms  
- Viewer-side streaming clients  

---

### 2.3 Interactive Live Streaming

The SDK supports **low-latency multi-party communication**, enabling:

- Host + guest co-hosting
- Real-time audience interaction
- Viewer participation modes

Viewers who do not join the interactive session can still watch the main live stream through standard playback protocols.

---

## 3. Web Integration

Web platforms can implement both **live publishing** and **live playback**.

---

### 3.1 Live Stream Publishing (Web Push)

Web browsers can publish live streams using **WebRTC**.

**Capabilities:**

- Camera and microphone capture
- Real-time encoding
- Stream multiplexing (audio + video)
- Embeddable publishing interface via JavaScript

**Protocol used:**

- **WebRTC**

**Typical steps:**

1. Access browser media devices (`getUserMedia`)
2. Establish WebRTC connection
3. Send encoded media stream to cloud streaming server

---

### 3.2 Audio Codec Compatibility Note

WebRTC publishing uses the **Opus** audio codec.

If playback uses traditional streaming protocols (RTMP, HTTP-FLV, or HLS):

- The backend streaming service will convert **Opus → AAC**
- This ensures compatibility with standard players
- Audio transcoding may introduce **additional processing costs**

---

### 3.3 Web Playback

Web applications can play streams using:

- **HTTP-FLV** (via JavaScript player)
- **HLS** (native browser support in many environments)
- **RTMP** (typically via dedicated players or plugins)

---

## 4. Feature Summary

| Feature | Mobile Apps | Web |
|---------|-------------|-----|
| Camera Capture | ✅ | ✅ |
| Screen Capture | ✅ | Limited (browser-dependent) |
| Live Publishing | RTMP | WebRTC |
| Playback Protocols | RTMP, HTTP-FLV, HLS | HTTP-FLV, HLS, RTMP (player-based) |
| Low-Latency Interaction | ✅ | ✅ |
| Multi-Party Streaming | ✅ | ✅ |

---

## 5. Typical Architecture

**Publisher (Mobile/Web)**  
→ Encodes video/audio  
→ Sends stream to cloud streaming server  

**Cloud Streaming Service**  
→ Distributes stream  
→ Handles protocol conversion  
→ Performs transcoding if required  

**Viewers (Mobile/Web)**  
→ Pull stream using RTMP / HTTP-FLV / HLS  

---

## 6. Common Use Cases

- Live education platforms  
- Interactive webinars  
- Event broadcasting  
- E-commerce live selling  
- Social live streaming  
- Remote collaboration  
