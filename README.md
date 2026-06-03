# Advanced Robotics Computer Vision Pipeline

A modular, high-performance computer vision repository developed with OpenCV and Python for advanced robotic applications. This pipeline moves beyond basic image manipulation to focus on real-time spatial awareness, geometric vision, and feedback loops for autonomous systems.

---
<br>

## 📁 Repository Structure

This repository uses a production-ready modular design to keep core vision engines isolated from execution logic, configurations, and test assets:

```text
.
├── assets/
│   └── setup_preview.gif      # Animated execution and tracking visualization
│   
├── config/
│   ├── camera_matrix.yaml     # Intrinsic camera parameters from calibration
│   └── distortion.yaml        # Lens distortion coefficients
│   
├── modules/
│   ├── __init__.py
│   ├── calibration.py         # Handles camera matrix parsing and lens unwrapping
│   ├── feature_tracker.py     # Core tracking engine (ORB, SIFT, Optical Flow)
│   └── pose_estimator.py      # 3D spatial coordinate solver (Perspective-n-Point)
│   
├── .gitignore
├── README.md
├── requirements.txt           # Package dependencies
└── run_pipeline.py            # Main real-time video execution stream
```
<br><br>
## 🚀 Key Modules & Implementation
This pipeline breaks down autonomous robot vision into three dedicated, decoupled engineering layers:
### 1.&nbsp;&nbsp;&nbsp;&nbsp;Feature Tracking (<kbd>modules/feature_tracker.py</kbd>)
   Utilizes fast feature detection algorithms to track environmental points across successive frames. Designed to serve as the front-end for Visual Odometry (VO) or feature-based Monocular SLAM systems to estimate motion without relying entirely on wheel encoders.
### 2.&nbsp;&nbsp;&nbsp;&nbsp;Camera Calibration & Rectification (<kbd>modules/calibration.py</kbd>)
   Provides dynamic loading of intrinsic camera parameters and lens distortion matrices. Essential for metric accuracy in distance estimation, visual servoing, and stereo disparity calculations.
### 3.&nbsp;&nbsp;&nbsp;&nbsp;Spatial Pose Estimation (<kbd>modules/pose_estimator.py</kbd>)
   Implements Perspective-n-Point (solvePnP) tracking to compute the exact 3D translation ($X, Y, Z$) and rotation (Roll, Pitch, Yaw) vectors of known targets relative to the camera center. This data forms the error vector for closed-loop visual servo controllers (Eye-in-the-Hand or Mobile Base tracking).

<br><br>
## 🛠️ Getting Started
### Prerequisites
Ensure you have a Python 3.10+ environment set up on your machine.

### Installation & Setup
1.    Clone the vision repository to your workspace:
```Bash
git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
cd YOUR_REPO_NAME
```
2.    Install the required system dependencies:
```Bash
pip install -r requirements.txt
```
3.    Run the real-time vision pipeline:
```Bash
python3 run_pipeline.py
```
<br><br>
## ⚙️ Configuration
Before running spatial estimation or depth modules, calibrate your camera sensor using a standard checkerboard pattern and export the parameters to the config/ directory:
* camera_matrix.yaml: Stores focal lengths ($f_x, f_y$) and principal points ($c_x, c_y$).
* distortion.yaml: Stores radial and tangential lens coefficients to un-distort high field-of-view camera lenses.
