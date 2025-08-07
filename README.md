# People Flow Detection using Object Tracking & Heatmap Visualization

This project implements a robust computer vision system to detect, track, and count people moving through a specific area in a video. It also generates a heatmap to visualize movement intensity across the frame. This can be applied to retail analytics, crowd monitoring, and smart surveillance systems.


## Input/Output Files

| File             | Description                                |
|------------------|--------------------------------------------|
| `people-walking.mp4` [Link](https://drive.google.com/file/d/1IiM2T7Lh0sdg4KVmfExsiN04vWxJYFq7/view?usp=sharing)| Input video file with human activity     |
| `output_video.mp4` [Link](https://drive.google.com/file/d/1l998QNjg42kQCo2G5p1-Ck3IZSF0WznY/view?usp=sharing)  | Annotated video with boxes and counters  |
| `heatmap.png` [Link](https://github.com/mdmahamudmredha/People-Flow-Detection-using-Object-Tracking-Heatmap-Visualization/blob/main/heatmap_enhanced.png)       | Generated heatmap of footfall patterns   |


## Key Objectives

- Detect individuals using a pre-trained YOLOv8 object detector.
- Track them frame-by-frame using the ByteTrack algorithm.
- Count the number of people entering and exiting through defined virtual lines.
- Generate a heatmap of movement density for spatial flow analysis.


## 🔧 Tools and Technologies Used

| Component      | Technology / Library         |
|----------------|-------------------------------|
| Detection      | YOLOv8 (Ultralytics)          |
| Tracking       | ByteTrack                     |
| Visualization  | Supervision, OpenCV           |
| Heatmap        | NumPy, Matplotlib             |
| Programming    | Python                        |
| Environment    | Jupyter Notebook              |


##  Project Workflow

### 1. **Object Detection with YOLOv8**

- Uses `yolov8n.pt`, a lightweight pre-trained model from the YOLOv8 family.
- Only class `0` (person) is considered for detection.
- Bounding boxes and confidence scores are generated per frame.

### 2. **Object Tracking with ByteTrack**

- Assigns unique ID to each detected person.
- Maintains identity across frames even under partial occlusion or movement.
- Implemented via `supervision` library's tracking wrapper.

### 3. **Line Crossing Logic for IN/OUT Counting**

Two virtual lines are defined horizontally in the frame:

| Line     | Position             | Role                        |
|----------|----------------------|-----------------------------|
| IN Line  | ⅓ height from top    | Detects people entering     |
| OUT Line | ⅔ height from top    | Detects people exiting      |

#### Movement Logic

- **IN:** Center y-coordinate crosses IN line downward (previous < line, current ≥ line).
- **OUT:** Center y-coordinate crosses OUT line upward (previous > line, current ≤ line).

Counts are tracked in real-time and updated on the output frame.

### 4. **Heatmap Generation**

- Collects all center points of tracked individuals.
- Plots them as a 2D histogram on the frame.
- Applies Gaussian smoothing and `'hot'` colormap using Matplotlib.
- Highlights zones with higher traffic density.


## Sample Output (Visual Description)

- **Output Video**
  - Green bounding boxes with object ID labels.
  - Blue and Red horizontal lines for IN and OUT zones.
  - Dynamic IN/OUT counters at the corner.

- **Heatmap**
  - Color gradient showing footfall concentration.
  - Brighter areas indicate high movement zones.


## Potential Use Cases
- Retail store customer flow analysis
- Entry-exit management in public venues
- Urban footfall monitoring
- Smart office space utilization
- Queue length and waiting time optimization

---

##  Setup Instructions

Make sure the following libraries are installed:

```bash
pip install ultralytics supervision opencv-python numpy matplotlib
