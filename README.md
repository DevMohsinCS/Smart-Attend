# Smart Attend: The Automatic Attendance System

**Smart Attend** is an AI-powered automatic attendance system that marks student attendance using a single picture. Attendance data is stored securely in a *MongoDB* backend. Attendance reports for each class can be generated as *CSV* files for later use.

---

## Table of Contents

- [Overview](#overview)
- [How to Use](#how-to-use)
- [Technologies \& Tools](#technologies--tools)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Running the Application](#running-the-application)
- [Model Details](#project-details)
- [Key Scripts](#key-scripts)
- [Requirements](#requirements)
- [License](#license)

---

## Overview

Smart Attend simplifies attendance management by leveraging face recognition technology. Teachers can create classes, add students, collect face samples, train models, and mark attendance automatically with minimal effort.

---

## How to Use

1. **Sign Up / Log In:**
The teacher creates an account or logs into the application.
2. **Manage Classes:**
    - The classes panel displays all classes the teacher is currently handling.
    - Click on a class to view details or click **Add Class** to create a new one.
3. **Add Students:**
    - Click **Add Students** to input each student’s details individually.
    - After adding all students, click **Done** to finish.
4. **View Class Information:**
    - Clicking a class shows details such as number of students, class name \& ID, and teacher name.
5. **Collect Face Samples:**
    - Click **Add Samples** to open the webcam and capture student images.
    - Images are augmented using the *Albumentations* library to increase dataset size and variability.
6. **Mark Attendance:**
    - Click **Mark Attendance** and upload a photo.
    - The system detects faces and marks attendance for recognized students.
7. **Generate Reports:**
    - Export attendance data as a *CSV* file for record-keeping and analysis.

---

## Technologies \& Tools

| Technology | Purpose |
| :-- | :-- |
| **OpenCV** | Face detection bounding boxes and webcam image capture |
| **ONNX Runtime** | Converts pretrained face detector model for efficient inference |
| **Scikit-Learn** | Trains and tests the Random Forest classifier for face recognition; data preprocessing |
| **MongoDB** | Stores teachers, classes, students, and attendance records |
| **Custom Tkinter** | Provides a professional and clean GUI interface |
| **Albumentations** | Performs image augmentation to improve model robustness |


---

## Project Structure

```
SmartAttend/
├── src/
│   ├── main.py                   # Main application entry point
│   ├── model_testing.py          # Face detection and recognition testing
│   ├── initialize_db.py          # MongoDB database initialization
│   └── initialize_folders.py     # Folder structure setup
├── detection_model/
│   ├── architecture.prototxt     # Caffe model architecture file
│   └── weights.caffemodel        # Pretrained model weights
└── requirements.txt              # Python dependencies
```


---

## Installation

### Prerequisites

- Python 3.8 or higher
- MongoDB installed and running locally
- Webcam (for face sample collection)


### Steps

1. **Clone the repository:**

```bash
git clone https://github.com/yourusername/ICAT-2.git
cd ICAT-2
```

2. **Install Python dependencies:**

```bash
pip install -r requirements.txt
```

3. **Start MongoDB service:**

```bash
sudo systemctl start mongod
```

4. **Initialize the system:**

```bash
python src/initialize_db.py
python src/initialize_folders.py
```


---

## Running the Application

1. Launch the app:

```bash
python src/main.py
```

2. Log in or create a new teacher account.
3. Create classes and add students.
4. Collect face samples via webcam.
5. Train the recognition model.
6. Start marking attendance automatically!

---

## Project Details

### Face Detection

- Utilizes a **Caffe-based deep learning model**.
- Real-time detection powered by **OpenCV**.
- Adjustable confidence threshold for detection sensitivity.


### Face Recognition

- Employs a **Random Forest classifier** trained per class.
- Extensive data augmentation using **Albumentations** to improve robustness.


### Data Augmentation Techniques

- **Geometric Transforms:**
Random rotation (±30°), horizontal flips, random scaling (±20%), elastic deformations.
- **Color Adjustments:**
Brightness/contrast changes, gamma correction, random brightness shifts.
- **Noise Injection:**
Gaussian noise, motion blur.
- **Environmental Simulation:**
Lighting changes, shadows.

These augmentations help the model generalize better, reduce overfitting, and handle diverse lighting and pose variations.

---

## Database Schema

| Collection | Fields |
| :-- | :-- |
| **Teachers** | `teacherID`, `username`, `password` |
| **Classes** | `classID`, `className`, `teacherID`, `students[]` |
| **Students** | `studentID`, `name`, `age`, `gender`, `batch`, `major` |
| **Attendance** | `date`, `classID`, `present[]` |


---

## Key Scripts

| Script | Description |
| :-- | :-- |
| `initialize_db_for_testing.py` | Resets and seeds MongoDB with test data |
| `initialize_folder_structure_for_testing.py` | Cleans and sets up class folders for fresh start |
| `main.py` | Main application with GUI and core logic |
| `model_testing.py` | Standalone script for testing face detection and recognition |


---

## Screenshots

### Sign-Up / Log-In Screen
![Sign-Up_Log-In_Screen](https://github.com/user-attachments/assets/f56a96e1-dcec-471d-a78e-53f5b2e68654)

### Classes Screen
![Classes Screen](https://github.com/user-attachments/assets/92cb8c5f-ddc8-4564-b0bd-daf05618df2f)

### Students Screen
![Students Screen](https://github.com/user-attachments/assets/55d6ded2-9180-4dd3-8a40-87b1aeb870ca)

---

## Requirements

- Python 3.8 or higher
- MongoDB (local instance)
- Webcam for sample collection
- See `requirements.txt` for full Python package list

---

## License

This project is intended for **educational purposes only**.
