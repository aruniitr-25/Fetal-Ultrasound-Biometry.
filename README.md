# Fetal Ultrasound Biometry Extraction (Computer Vision)

## Overview
This repository contains an end-to-end deep learning and computer vision pipeline designed to automate the measurement of fetal Biparietal Diameter (BPD) and Occipitofrontal Diameter (OFD) from noisy ultrasound imagery. 

The project implements and compares two distinct architectural methodologies to extract biometry points: direct landmark regression and semantic segmentation with classical CV post-processing.

## Methodologies

### Task 1: Landmark Detection (Regression)
* **Approach:** Direct spatial coordinate regression.
* **Architecture:** Modified ResNet-18 configured for single-channel grayscale input.
* **Mechanism:** The network maps raw pixel data directly to 8 continuous coordinate values representing the biometry endpoints. 

### Task 2: Semantic Segmentation & CV Post-Processing
* **Approach:** Foreground-background pixel classification combined with deterministic geometric fitting.
* **Architecture:** ResNet34-encoded U-Net trained with a combined BCE + Dice Loss to mitigate severe class imbalance.
* **Mechanism:** The deep learning model predicts a binary mask of the fetal cranium. A classical computer vision algorithm (OpenCV) then extracts the largest contour and fits a parametric ellipse to mathematically derive the exact major/minor axis endpoints (BPD and OFD).

## Model Weights
Due to GitHub's file size limits, the trained PyTorch `.pth` weights are hosted externally. You will need to download these files to run the inference notebooks.

**Model Weights:** [Download .pth files here](https://drive.google.com/drive/folders/1pL5stIVQV41sLIeqkxKNj2oIhKCdkxa1?usp=drive_link)

*(Please download the weights and place them in their respective `Model_Weights` folders before running `Tester.ipynb`).*

## Repository Structure
* `/task_1_landmark/`: Contains the Trainer and Tester notebooks for the regression approach, along with detailed research reports.
* `/task_2_segmentation/`: Contains the Trainer and Tester notebooks for the segmentation and ellipse-fitting approach.

## How to Run
1. Download the repository to your local machine or Google Colab.
2. Download the model weights from the link above and place Task 1's weights in `task_1_landmark/Model_Weights/` and Task 2's weights in `task_2_segmentation/Model_Weights/`.
3. Open `Tester.ipynb` in either folder, update the input image path, and run all cells to visualize the automated measurements.
