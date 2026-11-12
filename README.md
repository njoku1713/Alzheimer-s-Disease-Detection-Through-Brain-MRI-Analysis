# Alzheimer Disease Detection | MRI Brain Scan Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Tools and Technologies](#tools-and-technologies)
- [Dataset Breakdown](#dataset-breakdown)
- [Feature Engineering](#feature-engineering)
- [Power BI Dashboard](#power-bi-dashboard)
- [Insights and Findings](#insights-and-findings)
- [Recommendations](#recommendations)
- [Future Work](#future-work)
### Project Overview
This project analyzes 44,000+ MRI brain scans to extract image-based features that help understand the progression of Alzheimer’s Disease. Using Python for image processing and Power BI for interactive visualizations, we convert raw medical images into actionable insights.
### Tools and Technologies
- Python (OpenCV, NumPy, Pandas, Matplotlib)
- Power BI
- Jupyter Notebook
- Dataset of labeled brain MRI scans (NonDemented, Mild, Moderate, etc.)

### Dataset Breakdown
The dataset contains MRI scans labeled under 4 categories:
- NonDemented
- VeryMildDemented
- MildDemented
- ModerateDemented

Each image was analyzed to extract:
- Mean pixel intensity
- Standard deviation of pixel intensity
- Entropy
- Edge density
- Center brightness

### Feature Engineering
Python was used to automate image processing and extract meaningful features.
``` import cv2
import numpy as np

img = cv2.imread('example.jpg', cv2.IMREAD_GRAYSCALE)
mean_intensity = np.mean(img)
std_intensity = np.std(img)
entropy = -np.sum((img/255.0) * np.log2(img/255.0 + 1e-10))

# Additional features
edges = cv2.Canny(img, 100, 200)
edge_density = np.sum(edges > 0) / edges.size

h, w = img.shape
center = img[h//4:3*h//4, w//4:3*w//4]
center_brightness = np.mean(center)
# Extracted features were compiled into a structured dataset to be visualized in Power BI.
```
#### 1. Dataset Exploration
The MRI images were distributed across 4 labeled folders:
- NonDemented
- VeryMildDemented
- MildDemented
- ModerateDemented

Each image was grayscale, showing cross-sections of the brain from various angles. I manually examined samples to understand lighting, structure, and variation.
<img width="1080" height="607" alt="image" src="https://github.com/user-attachments/assets/031b2bb3-39f1-4868-b308-04f6333abdce" />

#### 2. Python Feature Extraction
I wrote Python scripts using OpenCV, NumPy, and Pandas to extract the following features for each image:
- Mean Pixel Intensity: Measures overall brightness
- Standard Deviation: Shows brightness variation
- Entropy: Indicates the level of structural complexity
- Edge Density: Captures texture and detail using Canny edge detection
- Center Brightness: Focuses on brightness in the central brain area

<img width="1080" height="607" alt="image" src="https://github.com/user-attachments/assets/60f5baf3-e415-45df-9b84-9defcd2fe0df" />

Each scan was processed in a loop, and the features were saved row by row into a structured dataset.

#### 3. Creating a Clean Feature Dataset (Excel/CSV)
After feature extraction, I compiled everything into a structured Excel file (and CSV) containing:

|Filename|Label|Mean|Std Dev|Entropy|Edge Density|Center Brightness|is_Augumented|
|--------|-----|----|-------|-------|------------|-----------------|-------------|
|Mild_1234.jpg|MildDemented|....|....|....|....|....|True|
|Non_4567.jpg|NonDemented|....|....|....|....|....|False|

<img width="540" height="252" alt="All Disease" src="https://github.com/user-attachments/assets/02c44621-aff7-496a-81a1-753043b06248" />


This dataset became the core input for my Power BI dashboard.



### Power BI Dashboard
Once the Excel dataset was ready, I imported it into Power BI to build an interactive dashboard that visualizes disease patterns, image features, and comparisons between diagnosis classes.

Key Visuals Include:
- Disease Progression Score: Based on entropy and center brightness
- Scan Disorder Level: Comparing all diagnosis classes
- Radiance Progression: Mean brightness across classes
- Top Diseased vs. Healthy Scans
- Interactive Table: All images with their extracted features
- Entropy Distribution: Shows lower entropy in Alzheimer's patients
- Brightness Variation: Used to separate Normal vs. Diseased groups

<img width="870" height="471" alt="image" src="https://github.com/user-attachments/assets/5e0a0ee7-3018-4b70-be93-8073a19f8829" />

<img width="870" height="481" alt="image" src="https://github.com/user-attachments/assets/87c8e106-974c-4e4f-b606-1189cde5301c" />

The dashboard allows filtering by diagnosis, viewing statistical differences, and exploring trends across thousands of scans in just a few clicks.



### Insights and Findings
The following insights and findings were obtained
1. Diseased brains showed lower entropy and reduced center brightness 
2. NonDemented scans had clearer structures and higher brightness variation 
3. Entropy and brightness levels may support early Alzheimer’s detection

### Recommendations

### Future Work
