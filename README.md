# Combat Drone — UAV Target Tracking

Object detection system for tracking unmanned aerial vehicles using YOLOv4-tiny.

<img height="200" src="/images/combot-drone.jpg"/>

## Project Goal

Build a target detection and tracking pipeline for fixed-wing UAVs from real flight footage. Existing public UAV datasets are limited, so this project includes a custom-built labeled dataset.

## Pipeline

### 1. Data Collection
- Source: HD videos from FPV drone YouTube channels
- Frame extraction with `split-videos-to-frames.py` (captures at 0.75s intervals)
- Image resizing to 640×480 with `image_resize.py`
- Manual annotation using [makesense.ai](https://www.makesense.ai/) in YOLO format

<img height="200" src="/images/makesense.png"/>

### 2. Training

Trained YOLOv4-tiny on 1000 labeled frames.

<img src="/videos/uav.gif"/>
<img height="500" src="/images/chart.png"/>

Detection accuracy is high on similar footage but degrades on unseen UAV models — the dataset needs more variety across different drone types and flight conditions.

### 3. Dataset

50 sample annotated images are included in `dataset/` (YOLO format: `class x_center y_center width height`, normalized coordinates). Full training set is 1000 images.

## Project Structure

```
combat-drone/
├── split-videos-to-frames.py   # Extract frames from video
├── image_resize.py              # Resize images to 640x480
├── dataset/                     # 50 labeled samples (JPG + TXT)
├── images/                      # Documentation assets
└── videos/
    └── uav.gif                  # Detection demo
```

## Dependencies

- OpenCV
- Pillow

## Roadmap

- [ ] Train and compare YOLOv4, YOLOv4x-Mish, YOLOv4-CSP, YOLOv5
- [ ] Export detection coordinates to file
- [ ] Convert models to TensorFlow / TensorRT
- [ ] Expand dataset with diverse UAV types

## References

- [Understanding How Image Quality Affects Deep Neural Networks](https://arxiv.org/pdf/1604.04004.pdf)

## License

MIT
