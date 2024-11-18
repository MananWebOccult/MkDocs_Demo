# Fried-Tofu-Counting

Prepared by: **Manan Patel**

---

## Table of Contents
1. [Introduction](#introduction)
2. [Estimation & Timeline](#estimation--timeline)
3. [Approaches](#approaches)
4. [Hardware Specifications / Tech Stack](#hardware-specifications--tech-stack)
5. [Dataset Information](#dataset-information)
6. [Implementation Instructions](#implementation-instructions)
7. [Results with Performance Metrics](#results-with-performance-metrics)
8. [Explanation of False Cases](#explanation-of-false-cases)

---

## Introduction
As an input, a video of a system in which tofus are passing through a potential area (window) is provided. The objective is:
1. To count the number of tofus each time a bunch of tofus passes through the window.
2. To count the total number of tofus in the entire video.
3. Display the output in the video and create a CSV file that includes the count of tofu in a bunch from its first occurrence.

### Useful Links:
- **The dataset shared by the client**: [Dataset Video by Client](#)
- **Jira Epic**: [Fried Tofu Counting Jira Issue](#)
- **Project Zip Link**: [Fried Tofu Counting Zip](#)
- **NAS Paths**:
  - Window Detection Model: `/media/ai_projects/Fried Tofu Counting/Window Detection Models`
  - Tofu Detection Model: `/media/ai_projects/Fried Tofu Counting/Tofu Detection Models`

---

## Estimation & Timeline

| Task                               | ETA         |
|------------------------------------|-------------|
| R&D for Approaches                 | 4 Hours     |
| Window Detection Model (Annotations and Training) | 4 Hours |
| Tofu Detection Model (Annotations and Training)  | 10 Hours |
| Logic Writing and Inference using Trained Models | 10 Hours |
| Setup and Inference on Jetson Orien Nano         | 2 Hours  |
| Documentation for the Project      | 4 Hours     |
| **Total**                          | **34 Hours**|

---

## Approaches

### Frame Processing
Iterates through each frame of the input video.

### Window Detection
Uses the **YOLOv8 Nano** window detection model to detect windows containing tofus:
- **Classes**: Full, Empty, Half.

### Tofu Detection
- Triggered only when the window detection model gives a "Full" class.
- Cropped window images are fed into the tofu detection model.
- Models tried:
  - YOLOv8 Segmentation (Nano, Small, Medium)
  - FastSAM Small
  - Final Choice: **YOLOv8 Nano Detection**, which gave satisfactory results.

### Annotation and Output
- Annotates frames with detected tofus.
- Saves results in:
  - Annotated output video.
  - CSV file with detection timings and counts.

### Counting Mechanism
- Counts tofus based on detected regions.
- Maintains a cumulative count throughout the video.

### Performance Metrics
- Logs performance metrics:
  - Frame processing time.
  - Model inference time.
  - Overall script execution time (displayed in the terminal).

---

## Hardware Specifications / Tech Stack
- **System**: Jetson Orien Nano
- **Performance**: ~23 FPS

---

## Dataset Information

### Window Detection Model
- **Total Images**: 705 annotated images.
- **Classes**: Full, Empty, Half.

### Tofu Detection Model
- **Total Images**: 306 cropped window images.
- **Annotations**: Annotated tofus within windows.

---

## Implementation Instructions

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/weboccult-ai/tofu-stack-monitoring.git
