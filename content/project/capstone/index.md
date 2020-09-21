---
title: Capstone
subtitle: Automated Mapping of Invasive Phragmites Australis from Remotely Sensed Imagery Using an Object-Based Machine Learning Algorithm
summary: Machine Learning Image Classification
tags:
- GIS Analysis
- GIS Workflow
- Spatial Algorithms
- Model Building
- Project Design
- Project Management
- Communication
- Data Models
- Scripting
- Machine Learning
- Python
date: "2019-04-30"

# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: Figure 1. Image of Phragmites spraying operation (PMG Vegetation; https://www.youtube.com/watch?v=8JuxJi3Cq84)
  focal_point: Smart

#links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
#url_code: ""
#url_pdf: ""
#url_slides: ""
#url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---

* **{{% staticref "files/Phragmites - Poster.pdf" "newtab" %}}Poster{{% /staticref %}}**
* **{{% staticref "files/Phragmites - Full Report.pdf" "newtab" %}}Final Report{{% /staticref %}}**

## Introduction

The invasive species Phragmites australis, or common reed, causes numerous problems and poses a significant threat to Utah wetlands, including the Great Salt Lake. The tall reed grows very densely into invaded regions, crowds out native species, disrupts migratory bird habitats, and negatively impacts recreation. It also alters the surface water regime, often converting submerged or saturated soils to dry land. As a result, the Utah Department of Natural Resources, Division of Forestry, Fire, and State Lands (FFSL), has taken an aggressive approach to mitigating the Phragmites problem. A big component of Phragmites mitigation includes spraying a wetland-safe herbicide to kill the plant and allow native species to return (Figure 1) using GPS-guided equipment. Efficient spraying requires accurate geographic data representing Phragmites boundaries, but it is currently unavailable. This project generates Phragmites maps from remotely sensed imagery, including satellite and unmanned aerial system platforms (UAS), using a prototype, automated Python script.

{{< figure src="Phrag area.png" title="Figure 2. Reference map of Howard Slough mitigation area (left) and study area for this project, including the UAS imagery (right)." >}}

## Methodology
Remotely sensed imagery was collected from three different platforms to facilitate DNR’s Phragmites mitigation work in the Howard Slough Waterfowl Management Area (Figure 2). The image platforms (Table 1), include the European Space Agency’s Sentinel-2 satellite, DigitalGlobe’s WorldView-2 (WV-2) satellite, and PMG Vegetation’s UAS. Each platform collects imagery in different wavelength bands and spatial resolutions.

{{< figure src="Phrag table1.png" title="Table 1. Remote sensing imagery platforms used in this study and their attributes." >}}

These images are then passed into an automated Python script (workflow depicted in Figure 3) that exports a shapefile for use in GPS-enabled Phragmites spraying equipment.

{{< figure src="Phrag method wide.png" title="Figure 3. Diagram of automated script workflow. The left columns describe the script’s primary functions, while the right columns represent of snapshot of each function’s output." >}}

## Results

The final classified images show quite different results (Figure 4), but each platform scored well (above 0.9) on several validation metrics (Table 2).

{{< figure src="Phrag table2.png" title="Table 2. A sample of accuracy metrics for each platform’s final classification. Metrics are calculated from independent validation pixels that were not used to train the model." >}}

While classification differences are expected for a complex wetland scene, the high scores for each platform may indicate that the training/validation data samples were unambiguous and easy to classify. Sentinel-2 even had a perfect score for producer’s accuracy with the live Phragmites class. Both objective accuracy metrics and subjective assessment indicate that WorldView-2 performed the best. It appears to have the most probable and coherent classification, with the best representation of dead Phragmites in previously-treated areas. The UAS results are much less coherent, but the higher resolution may better capture small pockets of water and native emergent vegetation. All platforms appear to over-classify live Phragmites and may have difficulty in distinguishing it from other forms of live vegetation. Generally, both higher resolution data and additional wavelength bands appear to improve image classification.

{{< figure src="Phrag classified.png" title="Figure 4. Standard red, green, blue (RGB) image from each platform (top row) and final classified land cover image using object-based random forest model (bottom row)." >}}

## Discussion

Overall, the methods employed in this study produced reasonable land cover classification results and successfully generated a shapefile identifying Phragmites boundaries from an automated workflow. However, there were several limitations to this study that prevent strong conclusions from being drawn, including:

* Ground truth data was not available; therefore, training and validation data was derived through visual interpretation of high-resolution imagery.
* Asynchronous images were assumed to be collected at the same time and the same set of training/validation data was used on images from all platforms.
* Image resolution differences resulted in a large discrepancy between platforms in the number of pixels available to train and validate the random forest model (Figure 5; Table 3). This limits the validity of strictly using the objective metrics to assess classification performance.

{{< figure src="Phrag table3.png" title="Table 3. Number of training and validation pixels for each imagery platform." >}}

With these in mind, the study could be improved if ground truth reference data was gathered with a random sampling strategy at the time image collection. This would limit temporal differences and remove subjectivity from the data collection process.

{{< figure src="Phrag pixels.png" title="Figure 5. Example training/validation polygon (red outline) overlaid on RGB imagery from each platform to demonstrate the difference in the number pixels available for training and validation across platforms." >}}

## Future Work

* Collect ground reference data at the time of image collection
* Employ a 5-band multispectral sensor to gather high-resolution UAS imagery in red, green, blue, red-edge, and near infrared wavelengths
* Experiment with the number of land covers used in the classification
* Perform additional optimizations to the image segmentation and random forest algorithms

**Additional details on all aspects of this project, including references and citations can be found in the  {{% staticref "files/Phragmites - Full Report.pdf" "newtab" %}}Full Report{{% /staticref %}}.**

## MSGIS Program Skills

* GIS Analysis
* Spatial Data and Algorithms
* GIS Workflow
* Model Building
* Cartography and Graphic Design
* Data Model and Structures
* Project Design
* Project Management
* Communication Skills
* Scripting (Python)
