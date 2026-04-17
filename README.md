
# 📷Visual Feature Matching and Panoramic Image Stitching

## 🧠 Objective

This project focuses on two core computer vision tasks using **OpenCV**:

1. **Analyzing video frames** to detect and visualize features such as edges, lines, and corners.
2. **Stitching a sequence of images** into a seamless panorama using feature matching and homography transformations.

---
---

## 🔧 Dependencies

- Python 3.x
- OpenCV (`cv2`)
- NumPy
- Matplotlib
- Google Colab (or local Jupyter)

Install necessary packages:
```bash
pip install opencv-python numpy matplotlib
```

---

## 📽️ Part A: Video Frame Analysis

### 1. **Video Loading & Initialization**
- Mounts Google Drive to access input video
- Checks if the video is accessible
- Extracts frame rate, resolution, and total frames

### 2. **Blurriness Detection**
- Uses the **Variance of Laplacian** method
- Blurry frames (low variance) are skipped from processing
- Stats are logged (total vs. blurry frames)

### 3. **Feature Detection on Frames**
- **Canny Edge Detection** to highlight object boundaries
- **Hough Line Transform** to detect straight lines (e.g., paper edges)
- **Harris Corner Detector** to highlight corners (visualized as red dots)
- **Filtered Frames** are drawn with overlays and saved into `output_video.mp4`

### 🎥 Video Demo

[![Watch the demo](https://img.youtube.com/vi/JN9h0tltMcI/hqdefault.jpg)](https://youtu.be/JN9h0tltMcI)

click on the image to watch full video


## 🖼️ Part B: Image Stitching for Panorama

### 1. **Image Loading**
- Loads all image files from `images/` folder
- Converts them to RGB for visualization

### 2. **Feature Extraction with SIFT**
- Converts images to grayscale
- Detects keypoints and descriptors using **SIFT (Scale-Invariant Feature Transform)**

### 3. **Feature Matching with FLANN**
- Uses **FLANN (Fast Library for Approximate Nearest Neighbors)** for descriptor matching
- Applies **Lowe’s ratio test** to filter strong matches between image pairs

### 4. **Homography Estimation**
- Uses **RANSAC** to compute transformation matrices between image pairs
- Filters outliers to ensure robust transformations

### 5. **Image Warping and Stitching**
- Warps subsequent images onto a common reference frame using computed homographies
- Applies **feather blending** for seamless transitions between stitched images
- Crops the final panorama to remove black borders

### 6. **Final Output**
- Displays the **stitched panoramic image** in full resolution

- Final panorama image:
- ![image](https://github.com/user-attachments/assets/ff018219-222f-4f7d-8c06-0defb4ff65fb)


---

## 🧠 Conceptual Insight

> **Why does panoramic stitching work best when the camera rotates in place?**  
When the camera rotates around its optical center, the scene maintains a consistent perspective across all images. This allows homographies to effectively align the overlapping regions. In contrast, camera translation introduces **parallax**, which distorts alignment due to varying object depths.


