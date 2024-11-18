# Approaches

## Frame Processing
Iterates through each frame of the input video.

## Window Detection
Uses the **YOLOv8 Nano** window detection model to detect windows containing tofus:
- **Classes**: Full, Empty, Half.

## Tofu Detection
- Triggered only when the window detection model gives a "Full" class.
- Cropped window images are fed into the tofu detection model.
- Models tried:
  - YOLOv8 Segmentation (Nano, Small, Medium)
  - FastSAM Small
  - Final Choice: **YOLOv8 Nano Detection**, which gave satisfactory results.

## Annotation and Output
- Annotates frames with detected tofus.
- Saves results in:
  - Annotated output video.
  - CSV file with detection timings and counts.

## Counting Mechanism
- Counts tofus based on detected regions.
- Maintains a cumulative count throughout the video.

## Performance Metrics
- Logs performance metrics:
  - Frame processing time.
  - Model inference time.
  - Overall script execution time (displayed in the terminal).

---