# 🚗 Behavioral Cloning for Autonomous Driving  
*Self-Driving Car Steering Control Using Deep Learning*

![Simulator Demo](https://img.shields.io/badge/Udacity-Simulator-blue) ![Status](https://img.shields.io/badge/status-Production--Ready-success) ![Python](https://img.shields.io/badge/Python-3.9-blue)

---

## 📌 Overview

This project implements an end-to-end deep learning system that enables a virtual self-driving car to navigate tracks autonomously by mimicking human steering behavior. Built using a Convolutional Neural Network inspired by NVIDIA’s architecture, the model predicts steering angles from dashboard camera images.

The goal was not only to build a working model but to ensure **real-world generalization**, **robustness**, and **bias mitigation**—making it suitable for intelligent transportation systems.

---

## 🎯 Project Goals

- Develop a behavioral cloning model that drives smoothly and safely in simulation.
- Apply rigorous data preprocessing and augmentation to prevent overfitting.
- Ensure the model performs well on both **seen** and **unseen** tracks.
- Address challenges in real-time simulation integration and data quality.

---

## 📂 Repository Structure

```
📁 data/                  # Collected driving images and steering angles
📁 model/                 # Saved models and weights
📁 notebooks/             # EDA, preprocessing and model training
📄 drive.py               # Main driving script (used with Udacity simulator)
📄 model.py               # Model architecture (NVIDIA-based)
📄 requirements.txt        # project dependencies 
📄 README.md              # Project details

```
---

## 🧠 Model Architecture

The model is based on NVIDIA's end-to-end learning for self-driving cars, consisting of:

- 5 Convolutional layers with ReLU activation

- Dropout layers for regularization

- Fully connected dense layers

- Final regression output for steering angle

- All images are preprocessed to match NVIDIA’s recommended input format: 200x66 YUV images normalized to [0, 1].
---
## 🧰 Technologies Used

- Python

- OpenCV, Matplotlib

- NumPy, Pandas

- TensorFlow / Keras

- imgaug 

---
## 🧼 Data Preprocessing

Preprocessing included:

- Cropping sky and dashboard regions

- Color conversion: RGB → YUV

- Gaussian blur to reduce noise

- Resizing to 200x66

- Normalization to range [0, 1]
  
---

## 🔄 Data Augmentation

To increase dataset diversity and improve generalization:

- Panning (random shifts)

- Zooming

- Brightness variation

- Horizontal flipping (with steering angle inversion)

- Augmentations were applied conditionally with a 50% probability each.
---
## 📊 Training Performance

### 🧪 Before Augmentation

| Epoch | Train Loss | Validation Loss |
| ----- | ---------- | --------------- |
| 1     | 0.4310     | 0.0798          |
| 5     | 0.0769     | 0.0598          |
| 10    | 0.0394     | 0.0447          |

### 🎮 Simulation Result

- The model drove partially on the training track but struggled at curves.

- It got stuck and fell off into ocean. 😄

- Poor generalization to unseen tracks due to lack of variability in training data.
  
watch the simulation here: https://www.loom.com/share/111707b9ca30442bb7b56c7b1eeab0c4?sid=99412bd7-2595-4256-b08c-fd4cba64fd2d

### ✅ After Augmentation

| Epoch | Train Loss | Validation Loss |
| ----- | ---------- | --------------- |
| 1     | 0.2855     | 0.3553          |
| 5     | 0.0550     | 0.0402          |
| 10    | 0.0331     | 0.0259          |


### 🎮 Simulation Result

✅ Track 1 (seen during training): https://www.loom.com/share/ecf2a4c14dd849d7b5b6f006d7bf9dfa?sid=0953d183-8cec-445d-b334-ce0bacefd521


🌍 Track 2 (unseen during training): https://www.loom.com/share/30d6dd3f3a1143588ee17b264be79ee4?sid=3a81cb35-4a32-4a2d-8e19-c3d4e4122c25

The augmented model successfully completed both tracks with consistent lane-following and better steering behavior.
---
## 🧗 Challenges  i Faced

** 1. Dependency Conflicts with Simulator**

Integrating the model with the Udacity simulator was challenging due to version mismatches. I had to do the following:

 - Created a clean Python 3.9 virtual environment

- Downgraded packages like python-socketio,  python-engineio, eventlet

** 2. Biased Steering Data**

Over 4,000 data points had a steering angle of 0.0, creating a model that preferred driving straight. i had to 

- Experiment with thresholds (100–300)

- Get steering angle 0.0 samples at 400, which reduced the dominance in the dataset

** 3. Inefficient Initial Driving**

The first round of data collection was poorly executed. The Manual driving  i did lacked turns and consistency, which even augmentation couldn't fix . i had to 

- Re-recorded data carefully

- Drive 4 laps each direction (left and right) to capture diverse directions, this is very cruial for behavioral cloning
---
  ## 💡 Key Takeaways
  
- Data quality is just as important as a model architecture.

- Bias in steering angle distribution can indeed severely hurt performance.

- Augmentation helps, but cannot compensate for poor training data.
---

## 💼 About Me

I am a data science and machine learning practitioner passionate about building solutions that bridge research and practical deployment.
I am currently open to remote opportunities in data science, machine learning engineering, and related fields.

Feel free to connect with me:

[Linkedlin](https://www.linkedin.com/in/patrickedosoma/)

[Email](edosomapatrick41@gmail.com)
---

## ⭐️ Star This Repo

If you found this project helpful, please star ⭐️ it to show support!

