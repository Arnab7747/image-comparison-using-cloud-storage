# Image Comparison with Object Detection Using Cloud Storage

This project demonstrates a powerful system for identifying objects in a given image and finding the most visually similar images from a cloud-based database. It uses the **YOLOv5** model for object detection and employs a multi-layered approach with **pHash**, **SSIM**, and **ORB** algorithms for efficient and accurate image comparison against a **Firebase Cloud Storage** backend.

---

## 📖 Overview

The core functionality of this project is to take a local image (`testImage.jpg`), detect all the objects within it, and for each detected object, search through a collection of images stored in Firebase Cloud Storage to find the best match.  

This is achieved by combining state-of-the-art **object detection** with a cascade of **image similarity algorithms**.

---

## ✨ Key Features

- **Object Detection**  
  Utilizes the powerful **YOLOv5** model to accurately detect and crop multiple objects from a source image.

- **Cloud Integration**  
  Seamlessly connects to **Google Firebase**, using **Firestore** to store image metadata (like pHashes) and **Cloud Storage** to hold the actual image files.

- **Efficient Comparison Funnel**  
  - **pHash (Perceptual Hashing):** A fast, initial screening of all database images to quickly find potential matches based on image "fingerprints."  
  - **Threshold-Based Deep Dive:** If the pHash similarity exceeds a user-defined threshold, the system proceeds to more computationally intensive checks.  
  - **SSIM (Structural Similarity Index):** Measures the perceptual similarity between the test image and the best pHash match, focusing on structural information.  
  - **ORB (Oriented FAST and Rotated BRIEF):** Compares key feature points between the images to provide another robust similarity score.  

---

## ⚙️ How It Works

The process is orchestrated by the **`main.py`** script and follows these steps:

1. **Initialization**  
   Cleans up any artifacts from previous runs.

2. **Object Detection**  
   - Loads the YOLOv5 model.  
   - Processes `testImage.jpg`.  
   - Detected objects are cropped and saved into `runs/detect/exp/crops`, organized into subfolders by class (e.g., `car`, `cup`).  

3. **Firebase Connection**  
   Establishes a secure connection to your Firebase project (Firestore + Cloud Storage).  

4. **Iterative Comparison**  
   - Calculates the **pHash** of the local object.  
   - Queries Firestore to compare with stored pHashes of the same class.  
   - Identifies the **top candidate** based on pHash similarity.  

5. **Detailed Analysis**  
   - If the top candidate’s pHash similarity is above the threshold, downloads the image from Cloud Storage.  
   - Performs **SSIM** and **ORB** comparisons.  

6. **Results**  
   After processing all objects, prints a **detailed report** showing:  
   - Most similar cloud image for each detected object  
   - pHash, SSIM, and ORB similarity percentages  

---

## 🛠️ Technologies Used

- **Python 3**
- **PyTorch** (YOLOv5)
- **Google Firebase**  
  - Firestore (database)  
  - Cloud Storage (file storage)  
- **OpenCV**
- **scikit-image**
- **Pillow (PIL)**
- **ImageHash**
- **pandas**

---

## 🚀 Setup and Installation

### ✅ Prerequisites
- Python 3.8 or higher  
- A **Google Firebase** project  

### 🔧 Installation
Clone the repository:
```bash
git clone https://github.com/your-username/image-comparison-using-cloud-storage.git
cd image-comparison-using-cloud-storage
