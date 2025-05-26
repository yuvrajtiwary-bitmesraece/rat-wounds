# rat-wounds

A wound healing analysis project using polygonal annotations of rat wound images. Calculates wound area in mm² over time, computes healing percentages, and visualizes average healing curves across Control, Drug, and Standard groups using Python and matplotlib in Google Colab.

## Project Overview

This project focuses on analyzing the wound healing process in laboratory rats across different treatment categories — Control, Drug, and Standard. This research is being carried out in prestigious Rajendra Institute of Medical Sciences (RIMS), Ranchi. Firstly the raw unprocessed image was captured by scholars conducting the research on periodic basis. Each rat was monitored over a 13-day period, with wound images captured on odd-numbered days. Then we resized the images wihout tampering the zoom/spatial features of wound and used Oxford's VGG Image Annotator (VIA) to annotate the wound boundary by encapsulating the wound using closest fitting polygon and storing the segmentation polygon annotations in .csv format. Using polygonal annotations created for each image, we calculated the wound area in square millimeters (mm²) and tracked healing progression over time. The goal is to quantify and compare healing rates across groups using structured analysis and visualization techniques in Python.

## Folder Structure

After unzipping the dataset, the folder structure is organized as follows:

```
/my_extracted_folder/
└── Rat Wounds/
    └── Rat_wounds/
        ├── Control 1/
        │   └── Control 1 Annotations.csv
        ├── Control 2/
        ├── Drug 1/
        ├── Standard 1/
        └── ...
```

Each rat folder (e.g., Control 1, Drug 2) contains a corresponding annotation file named as <Folder Name> Annotations.csv, which includes polygonal coordinates marking the wound area for each image. These files serve as the input for wound area calculation and analysis.

##  Dataset Description

The dataset comprises wound progression images from 12 rats, divided equally into three treatment categories:
```
- Control (no treatment)

- Drug (test drug applied)

- Standard (standard treatment)
```

Each rat has 7 images, captured on alternate days: Day 1, 3, 5, 7, 9, 11, and 13.

For each image:
```
- A polygonal annotation (in JSON format) is provided inside a corresponding CSV file.

- These annotations contain the X and Y coordinates defining the wound boundary.
```
Each annotation CSV includes:
```
- filename – name of the wound image.

- region_shape_attributes – JSON string encoding polygon coordinates.
```

This structured dataset enables measurement of wound area over time and comparative healing rate analysis across the three treatment categories.

## Project Workflow Summary

This project follows a systematic Colab-based pipeline:

1. **Import Dependencies**
```
   Essential libraries such as pandas, numpy, json, matplotlib, and file utilities are imported.
```
2. **Shoelace-Based Polygon Area Calculation**
```
   A custom function calculates wound area (in pixels) using the Shoelace formula,
   then converts it to mm² using a known pixel-to-mm scale.
```
3. **Data Upload & Extraction**
```
   - Users upload the zipped dataset (Rat Wounds.zip).
   - It is extracted and prepared for parsing.
```
4. **Annotation Parsing**
```
   - Annotation CSVs from each rat folder are read.
   - From each image's polygon coordinates, wound area is computed.
   - Metadata such as category, rat number, and day is extracted
```
5. **Dataframe Creation**
```
   - A master DataFrame stores all parsed data: category, rat number, day, and wound area (mm²).
   - Data is sorted chronologically per rat.
```
6. **Pivot Table Generation**
```
   - Wound areas are reshaped into a rat-wise summary table with one row per rat and columns for each day.
```
7. **Healing Rate Calculation**
```
   - Percent wound healing is calculated relative to Day 1.
   - A new table showing % healed across days is generated.
```
8. **Visualization**
```
   - A line plot visualizes average healing curves for each category over time.
```

This pipeline enables transparent wound area tracking and objective healing rate comparison across treatment groups.

## Key Concepts Used

This project integrates key concepts from geometry, data processing, and visualization:

1. **Shoelace Formula**
```
   Used for calculating the area of polygonal regions (wound boundaries) based on their (x, y) coordinates.
```
2. **Pixel-to-mm² Conversion**
```
   Each pixel-based area is converted to real-world units (mm²) using a fixed scale factor (0.264583 mm/pixel)
```
3. **Regular Expressions (Regex)**
```
   Applied to extract metadata (e.g., rat number and day) from file and folder names.
```
4. **Data Cleaning & Transformation**
```
   Structured parsing of CSV files and reshaping into a pivot table for comparison across rats and days.
```
5. **Percentage-Based Healing Calculation**
```
   Healed area is computed as a percentage reduction from the original wound size on Day 1.
```
6. **Matplotlib Plotting**
```
   Visual representation of healing trends across control, drug, and standard treatment groups.
```
These concepts collectively form a robust framework for image-derived wound area analysis in biomedical research.

## Output Tables and Visuals

### 1. Wound Area Table (mm²) 

A comprehensive pivot table showing the wound area (in mm²) for each rat across Days 1 to 13.

![Pivot Table of Wound Areas](https://raw.githubusercontent.com/yuvrajtiwary-bitmesraece/rat-wounds/main/Pivot%20Table%20of%20Wound%20Areas.png)  

### 2. % Healing Table

A transformed version showing percent healing from Day 1 for each rat.

![Wound Healing Percentage Table](https://raw.githubusercontent.com/yuvrajtiwary-bitmesraece/rat-wounds/main/Wound%20Healing%20Percentage%20Table.png)  

### 3. Mean Healing Curve Plot

A line chart showing the average healing trend per treatment group over time:
```
   - X-axis: Days (1 to 13).
   - Y-axis: Avg wound area (mm²).
   - Lines: Control, Drug, Standard categories.
   - Markers: Show precise daily measurements.
```
![Category-wise Average Wound Healing Curve](https://raw.githubusercontent.com/yuvrajtiwary-bitmesraece/rat-wounds/main/Category-wise%20Average%20Wound%20Healing%20Curve.png)

## Thank You

Grateful for your time and attention — it truly means a lot!
