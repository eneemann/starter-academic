---
title: Remote Sensing Analysis
subtitle: Assessing California's Thomas Wildfire and Montecito's Debris-Flow Risk with Sentinel-2 Imagery and the High-Resolution Rapid Refresh Model
summary: Wildfire and Debris-Flow Analysis
tags:
- GIS Analysis
- GIS Workflow
- Spatial Algorithms
- Model Building
- Project Design
- Project Management
- Communication
- Cartography
- Spatial Analysis
date: "2018-04-18"


# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: Sentinel-2 Shortwave Infrared (SWIR) false color image from 22 Jan 2018
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

* **{{% staticref "files/Thomas - Presentation.pdf" "newtab" %}}Slides{{% /staticref %}}**
* **{{% staticref "files/Thomas - Final Report.pdf" "newtab" %}}Final Report{{% /staticref %}}**
* **{{% staticref "files/Thomas - Poster.pdf" "newtab" %}}Conference Poster{{% /staticref %}}**

## Background

The Thomas fire burned areas of Ventura and Santa Barbara counties in southern California between ignition on 4 December 2017 and containment on 12 January 2018. It erupted in early December as high pressure over the Great Basin fueled strong Santa Ana winds and dry conditions. When it was finally contained in mid-January 2018, the Thomas Fire had burned 281,893 acres, making it the largest California wildfire in modern history. The fire caused the evacuation of more than 100,000 people and destroyed over 1300 structures (Cal Fire 2018). The large swath of burn-scarred land immediately became vulnerable to mudslides and debris-flows. On 9 January 2018, an atmospheric river event brought tremendous precipitation to southern California and 13.7 mm (0.54 in) of rain fell in just 5 minutes on Montecito and the nearby mountains to the north (National Weather Service 2018). The resulting debris-flows killed 21 people, destroyed 166 structures (Figure 1), and damaged 395 additional structures (Cal Fire 2018). Much of the region ended up with 7-15 cm (2.75-5.9 in) of rain in just 2 days. The combination of recent wildfires, intense precipitation, and terrain characteristics (slope severity and soil properties) generated the devastating debris-flows.

{{< figure src="Thomas -background.png" title="Figure 1. Photos from Santa Barbara County Fire-Public Information Officer Twitter: @EliasonMike, SBCFireInfo" >}}


## Data

All data used in this project came from free, publicly-available sources. Satellite imagery from the Sentinel-2 Multispectral Imager (MSI) was gathered from the European Space Agency via Google Earth Engine. The MSI has 13 bands spanning the visible to shortwave infrared wavelengths at variable resolutions of 10, 20, and 60m. Digital Elevation Model (DEM) data was collected from the USGS National Map at 1/9 arc-second resolution (~10m). Soil erodibility data came from the Natural Resources Conservation Service State Soil Geographic Data Base. Precipitation observations were gathered from the National Weather Service and precipitation forecasts from the operational High-Resolution Rapid Refresh (HRRR) model were downloaded from the HRRR Archive at the University of Utah. The fire perimeter (Figure 2) and watershed outlets (pour points) were derived from USGS data. The debris-flow polygons were pulled from a web map produced by the Santa Barbara Independent.

{{< figure src="Thomas - region.png" title="Figure 2. Thomas Fire perimeter and study area" >}}

## Methods

Sentinel-2 imagery of southern California was collected for pre-fire (3 December 2017) and post-fire (22 January 2018) conditions. The NBR (Brewer 2005) was then calculated for each image using, Band 12 (SWIR, 2190 nm) and Band 8A (NIR, 865 nm) from the formula below:

$$NBR = 1000*\frac{NIR - SWIR}{NIR + SWIR}$$  

A differenced NBR (dNBR) was generated from the pre- and post-fire NBR data to identify burn severity resulting from the Thomas Fire (Figure 3). The severity thresholds for moderate (> 350) and high (> 650) burns were set as the average respective threshold from California fires in 2015, according to data from Monitoring Trends in Burn Severity (MTBS). This number was then rounded up to the next multiple of 50, to be conservative. The DEM data was used in a hydrology workflow to delineate primary streams and watershed boundaries based on USGS pour points that were snapped to the manually-created streams. Slope data were also built from the 10 m DEM data set. Once the foundational data was prepared, debris-flow probabilities for the 9 January 2018 Montecito event were calculated based on the logistic regression approach outlined by Staley et al, 2016, where statistical likelihood of debris-flow occurrence, P, is:

$$P = \frac{e^\chi}{1 + e^\chi}$$

Further, χ is determined by the link function:

$$\chi = \beta + C_{1}TR + C_{2}FR + C_{3}SR$$  

The parameters in the link function are represented by: 

{{< figure src="Thomas - Table 1.png" >}}

The logistic regression approach was used to model predicted debris-flow probability based on a common USGS rainfall threshold (6 mm in 15 min), actual observations in Montecito (13.7 mm in 15 min), and rainfall rates from HRRR hourly accumulated precipitation forecasts (~1.0-8.7 mm in 15 min) valid within 2 hours of the observed debris-flows. The 0500 UTC run of the operational HRRR model was used, with hourly rainfall at the end of forecast hour 08, valid 1300 UTC. This output was selected because it was representative of observed rainfall, though the timing was off by 75-90 min from the actual rainfall maximum (~1130 UTC).

{{< figure src="Thomas - method.png" title="Figure 3. Methodology of debris flow probability calculation" >}}

## Results

The logistic regression approach successfully identified the debris-flow threat posed by the Thomas Fire to Montecito for the 9 January 2018 storm (Figure 4). All models indicated an elevated threat (P >= 0.5) for the watersheds above Montecito. When observed rainfall totals from Montecito on 9 January (13.7 mm in 15 min) were used in the model, it indicated P > 0.99 (not shown). The uniform rainfall threshold of 6 mm in 15 minutes, also identified the high threat, generally 0.591 < P < 0.798. Additionally, forecasts from the HRRR model demonstrated intense rainfall leading to 0.663 < P < 0.882 in the watersheds above Montecito. Predictions based on HRRR data also generated better spatial results, with the eastern portions of the Thomas Fire watersheds showing low debris-flow probability.

{{< figure src="Thomas - probabilities.png" title="Figure 4. Debris-flow probabilities based on uniform rainfall (top-left), HRRR forecast rainfall (top-right), and probability difference (bottom)" >}}

Overall, the spatially-varying debris-flow probabilities generated with HRRR model data decreased the percentage of high-probability watersheds (see table below). When compared to the uniform precipitation probabilities, the added information from the HRRR model forecasts appear useful in isolating the greatest debris-flow threat, as opposed to generalizing high probabilities over a large area. If extended to other events, this could help reduce false alarms, constrain evacuation regions, modify response plans, and stage resources for recovery efforts.

{{< figure src="Thomas - Table 2.png" >}}

Closer inspection of the Montecito area, shows the HRRR-based probabilities accurately characterized the debris-flow hazard in the watersheds above the town (Figure 5), which feed the primary streams. All 561 structures that were damaged or destroyed in the event were located in the purple damage report area of the figure below.

{{< figure src="Thomas - Montecito.png" title="Figure 5. Zoomed-in view of watersheds in Montecito region with damage report areas" >}}

## Conclusions

* Calculating dNBR from Sentinel-2 imagery is an effective way to quantify burn severity and coverage.
* The debris-flow probability method used by the USGS and introduced by Staley et al. 2016, performed well in assessing the debris-flow threat in Montecito, CA on 9 January 2018.
* The use of spatially-varying precipitation forecasts from high-resolution weather models may be useful in identifying the areas of greatest debris-flow risk. This may be particularly true near large fires or fire complexes and additional research using ensemble models is recommended.
* While regional modification would likely be required, this methodology could potentially be extended to other locations around the world to identify regions and populations at risk from debris-flows.

**Additional details on the methodology and results, including supervised classification and NBR change detection, and all references can be found in the {{% staticref "files/Thomas - Final Report.pdf" "newtab" %}}Full Report{{% /staticref %}}.**

## MSGIS Program Skills


* GIS Analysis
* Spatial Data and Algorithms
* GIS Workflow
* Model Building
* Cartography and Graphic Design
* Spatial Analysis
* Project Design
* Project Management
* Communication Skills
