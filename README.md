# RoadScan AI — Automated Pothole Detection & Tracking

RoadScan AI is a computer vision system built to automatically detect and track potholes in road footage — including dashcam, drone, and fixed-camera video.

At its core, the system uses a **YOLO11n model fine-tuned on a custom pothole dataset**, paired with **ByteTrack for multi-object tracking**. This enables the system to maintain a consistent identity for each pothole across frames rather than treating every detection as a new, isolated event.

---

## Overview

The pipeline processes video footage frame by frame. Each frame is passed through the detection model, potholes are localized and classified, and tracking IDs are assigned and maintained across the sequence.

The results are rendered directly onto the output video as annotated bounding boxes and tracking IDs.

Alongside the processed video, RoadScan AI generates quantitative summary metrics including:

- Total frames processed
- Total detections
- End-to-end processing time

This provides both a visual representation of road conditions and measurable information about the detection process.

---

## Features

- **Custom-trained detector** — YOLO11n fine-tuned specifically on a custom pothole dataset for road-surface defect detection.

- **Persistent multi-object tracking** — ByteTrack assigns and maintains consistent tracking IDs across frames, preventing the same pothole from being treated as multiple independent detections.

- **Interactive web interface** — Upload road footage, configure detection parameters such as confidence threshold and inference resolution, and preview or export the processed results directly from the browser.

- **Quantitative output** — Reports total frames processed, total detections, and processing time alongside the annotated video.

- **Browser-safe playback** — Output videos are automatically re-encoded when necessary to ensure reliable inline playback directly within the browser.

---

## How It Works

1. Video footage is loaded through the web interface.
2. The video is read frame by frame using OpenCV.
3. Each frame is passed through the fine-tuned YOLO11n model for pothole detection.
4. ByteTrack maintains tracking IDs for detected potholes across consecutive frames.
5. Bounding boxes, confidence scores, and tracking IDs are rendered onto each frame.
6. Annotated frames are compiled into the final output video.
7. Summary statistics are generated, including frames processed, detections, and processing time.
8. The output video is re-encoded when required for reliable browser playback.

---

## Use Cases

### Municipal Road Inspection

Identify potholes from road-survey footage and assist in prioritizing road maintenance based on detected defect density.

### Fleet Dashcam Monitoring

Scale pothole detection across vehicle fleets covering large road networks and continuously collect road-condition information.

### Infrastructure Defect Logging

Convert raw road footage into structured, annotated, and reviewable data for civil engineering surveys, road inspections, and maintenance reporting.

---

## Tech Stack

| Component | Technology |
|---|---|
| **Programming Language** | Python |
| **Object Detection** | YOLO11n |
| **Object Tracking** | ByteTrack |
| **Computer Vision** | OpenCV |
| **Deep Learning Framework** | Ultralytics |
| **Web Interface** | Streamlit |
| **Video Processing** | OpenCV |
| **Video Encoding** | FFmpeg |

---

## System Architecture

```text
                    Road Video
                        │
                        ▼
                ┌───────────────┐
                │    OpenCV     │
                │ Frame Reading │
                └───────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │    YOLO11n    │
                │    Detection  │
                └───────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │   ByteTrack   │
                │    Tracking   │
                └───────┬───────┘
                        │
                        ▼
              Bounding Boxes + IDs
                        │
                        ▼
                Annotated Frames
                        │
                        ▼
                ┌───────────────┐
                │ Output Video  │
                └───────────────┘
                        │
                        ▼
              Processing Metrics
