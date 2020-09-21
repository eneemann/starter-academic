---
title: Geocomputation
subtitle: Quantifying Wildfire Susceptibility in Utah Using an Artificial Neural Network
summary: Machine Learning Wildfire Analysis
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
- Data Models
- Database Design
- Scripting
- Machine Learning
- R
date: "2018-12-09"


# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: Architecture diagram of a typical neural network
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

* **{{% staticref "files/NeuralNet - Presentation.pdf" "newtab" %}}Slides{{% /staticref %}}**
* **{{% staticref "files/NeuralNet - Full Report.pdf" "newtab" %}}Final Report{{% /staticref %}}**


## Introduction

Wildfire is a common hazard faced by large regions in the western US due to the combination of vegetation/fuels, climate, topography, and ignition sources. In recent decades, with increases in population, communities and residential areas have continually expanded outward from urban centers. In the mountainous west, this expansion typically leads to additional development in the urban-wildland interface, thereby increasing the number of people exposed to the potential wildfire hazard. Identifying areas of wildfire susceptibility is important to ensure at-risk populations have emergency management plans and are able to mitigate fire risk as much as possible. The most effective method of identifying risk areas is producing maps by combining multiple wildfire parameters in a geographic information system (GIS). This study aims to quantify wildfire susceptibility in Utah and identify locations at greatest risk.

A multi-layer perceptron (MLP) neural network (NN) was chosen as the model for this study due to the recent success of other research projects in implementing NNs to predict forest fire susceptibility (Satir et al., 2015; Bui et al., 2017). Neural Networks are a natural choice for analyzing fire potential because they are good at approximating complex functions, are able to capture both linear and nonlinear relationships that exist between predictors and dependent variables, and adaptively learn from training data (Kantardzic, 2011; Satir et al., 2015).

## Data

All data used in this research came from free, publicly-available sources. The original data sets were initially gathered on disparate grids (different cell sizes, projections, dimensions, etc.) and were aligned to a uniform grid via projections in ESRI’s ArcMap software and with the use of ArcPy scripts. The data were also clipped down to the same geographic areas of interest (figure 1). This resulted in raster data sets with a Universal Transverse Mercator coordinate system in zone 12 North (UTM 12N). Each grid cell is 30 by 30 m with total dimensions of 2867 by 4251 pixels. The data was then resampled to a 90 by 90 m grid to alleviate computational challenges encountered on the full-resolution data.

A snapshot of all data sets used in the NN model is shown in Figure 1, below. A description of each data set can be found in the following paragraphs.

{{< figure src="NeuralNet all data.png" title="Figure 1. Snapshot of the data used in the neural network." >}}

_Historical Fires_

* Historical fire occurrence and burn severity data was collected from the Monitoring Trends in Burn Severity (MTBS) project. For this study, data from 2007-2016 was used to train the NN in order to place an emphasis on the most recent decade of fire data, which should best correspond with recent vegetation and infrastructure data. The ten annual data sets from 2007-2016 where then reclassified to only include burned areas (data value of 1-4), and summed up into a single data set. This resultant MTBS fire data set accounts for a combination of cumulative fire occurrences (multiple fires) and burn severities, called the historical fire index.

_Terrain_

* The Digital Elevation Model (DEM) used in this study was downloaded from the Utah Wildfire Risk Assessment Portal (WRAP). Slope and aspect data sets were calculated from the DEM and used as inputs into the NN model. These three terrain-related data sets are important for the neural network model because each has an influence on wildfire and fire-related parameters.

_Vegetation_

* Vegetation data sets were also gathered from the Utah WRAP, each on the same UTM 12N, 30 m grid as the DEM data. The vegetation type data set categorizes each grid cell into one of 19 different categories. The vegetation type information is important for identifying the type of biomass available for burning, where some vegetation types burn more readily than others due to their biophysical properties (Bui et al., 2017). Two additional vegetation data sets, canopy cover (%) and bulk canopy density (kg/m<sup>3</sup> * 100) are also included to help quantify the amount of biomass fuel that is available for burning on a grid cell.

_Infrastructure_

* A statewide Utah roads data set was gathered from the Utah Automated Geographic Reference Center (AGRC). The vector road features were used to calculate a distance-to-roads raster layer using Euclidean distance, meaning the minimum distance from a pixel to a road is calculated “as the crow flies.” Distance to roads is employed as a mechanism to measure the anthropogenic influence on wildfires and relates to the potential cause of wildfires (Satir et al., 2015; Bui et al., 2017).

_Climate_

* Climate data for this study was collected from Oregon State’s PRISM Climate Group. Monthly 30-year normal temperature and precipitation data sets were downloaded with 800 m grid cells. Only data from the months of June through October were used, representing the primary fire season in Utah. The monthly climate data sets, for both temperature and precipitation, were averaged into a single data set representing the mean conditions for the entire fire season. These data were resampled to 30 m grid cells with cubic interpolation.

## Methods

_Data Preprocessing_

In order to prepare the data for input into the neural network model, several preprocessing steps were necessary. First, the data was scaled with a max-min normalization to place each data set between a range of 0 to 1. This was needed to ensure that the scale variations among the different data sets didn’t lead one or two variables to overwhelm the training process and contaminate the results.

The historical fire severity MTBS data, used for training the NN, was thinned in order to improve the training process. The vast majority of the area of interest is comprised of pixels that have not been burned (~98%), but it was desirable to have better balance among burned and unburned pixels in the training data set. For this reason, a subset of the entire AOI was used for training, where polygons around the burned areas where chosen to provide a more balanced mix of burned/unburned pixels (black polygons in figure 2). This also improved the efficiency of training the NN, as data set used for training was about 10% of the original size.

{{< figure src="NeuralNet training data.png" title="Figure 2. Historical fire severity data used to train neural network." >}}

_Artificial Neural Network_

The R statistical language was used to implement the NN using RStudio software, specifically with the ‘neuralnet’ library. A forward-feed MLP NN was employed with a resilient backpropagation learning algorithm. The network was “fully-connected,” meaning that every neuron in a layer was connected to every neuron in adjacent layers. The final NN architecture including 15 hidden layers and 1 output node, representing fire susceptibility. In addition to building a NN model with the full complement of input data sets, a second model was generated without the vegetation type data. This was done to examine the influence of vegetation type and its effect on the results. Other than the removal of the vegetation type categories, there were no other differences between the models. This model will hereafter be referred to a “NVT.”

{{< figure src="NeuralNet fire suscep table.png" title="Table 1. Final categorization of fire susceptibility model." >}}

Finally, the output of each model was normalized with a min-max normalization method to put the Fire Susceptibility Index on a 0-1 scale. The results from each model were then categorized into 6 fire susceptibility groups with a natural breaks methodology. However, because the categories from the Original and NVT models were very similar, the final categorization for each model was standardized based on table 1. This created a consistent symbology for generating fire susceptibility maps and allowed for a more direct comparison between the two models.  A diagram showing the final architecture of the NVT model is shown in figure 3.

{{< figure src="NeuralNet diagram.png" title="Figure 3. Final neural network architecture and weights for the No Vegetation Type (NVT) model." >}}

## Results

The output from each of the NN models showed results with many similarities and some notable differences. Both models had a strong histogram peak centered on 0.55 (not shown), but the distribution of values around that peak varies. In the Original model, the vast majority of pixels were placed between 0.4 and 0.8, with a narrower distribution and shorter tails. The NVT model, however, had a wider distribution and longer tails, with a generally broader range between 0.2 and 0.85. This indicates that the Original model has many more values scoring in the middle of the range, while the NVT model’s larger range has more pixels assessed with “very low” or “extreme” values. Visually, this is depicted in figure 4, which displays a map of the Wasatch Front region with the Fire Susceptibility Index calculated for each pixel. Compared to the Original Model, the NVT model has more values in the “extreme” category for high-threat areas such as Antelope Island in the Great Salt Lake, the northern Oquirrh Mountains, the Lake Mountains, and the mountain range south of Utah Lake. The NVT model also has a larger quantity of “very low” pixels along the high peaks of the Wasatch Front and Oquirrh Mountains.

{{< figure src="NeuralNet maps.png" title="Figure 4. Fire Susceptibility Index from the Original and NVT models with census tracts outlined in black." >}}

Another notable difference between the models is the apparent influence of the vegetation type variable in the Original model and its lack of influence in the NVT model (where it was removed). The Original model has a generally noisier appearance, reflective of the noisy nature of the vegetation type variable, whereas the NVT model has smoother, more gradual transitions from low to high index values. The Original model also highlights the area between Salt Lake International Airport and the Great Salt Lake with “very high” and “extreme” index values, while the NVT model shows “very low” to “moderate” values. Here, the Original model appears to be picking up on increased fire susceptibility from the shrubland and chaparral vegetation types. The NVT model also tends to be more strongly influenced by elevation and aspect in mountainous regions, whereas the Original model is strongly influenced by vegetation type.

The influence of vegetation type is further examined by plotting variable importance based on NN connection weights from each model, as seen in figure 5. Indeed, the 10 most important variables in the Original model are vegetation types, which also make up 15 of the 18 most important variables. The top non-vegetation variables include elevation, precipitation, and distance to roads. For the NVT model, the top 3 variables are precipitation, elevation, and distance to roads. This comparison shows the importance of the vegetation type variables in the Original model, perhaps even indicating that it is over-influencing results.

{{< figure src="NeuralNet variable import.png" title="Figure 5. Variable importance plots for Original and NVT models." >}}

A final, quantitative comparison of the Original and NVT models is presented in table 2. Mean squared error (MSE) and mean absolute error (MAE) metrics are calculated for each model using the subset of validation data from training the NN models. These metrics both indicate that the NVT model performs better as its errors are roughly half of the Original model’s error. The area under the curve (AUC) metric for the receiver operating characteristic (ROC) curve was also calculated for each model. This value accounts for a balance between true positive rate and false positive rate when using a broad range of thresholds to classify model results. The AUC metric indicates that the Original model (0.8875) outperformed the NVT model (0.8127) as the Original model had a higher value and was closer to the perfect score of one. These two sets of metrics (errors and AUC) show conflicting results without a clear winner on which model performs best. It should also be noted that these metrics only consider about 3% of all pixels in the study area, those used for validation of the training data.

{{< figure src="NeuralNet metrics.png" title="Table 2. Quantitative results comparing Original and NVT models. Mean Squared Error, Mean Absolute Error, and Receiver Operating Characteristic Area Under the Curve calculated from the validation data subset." >}}

## Conclusions

Overall, this study demonstrates that the NN methodology produced reasonable results in quantifying wildfire susceptibility along Utah’s Wasatch Front. Particularly, it shows that vegetation type may play a prominent role in estimating wildfire susceptibility, as was noted by the model differences between the Original an NVT models. The inclusion of vegetation type often produced noisier results, reflecting the noisy nature of the vegetation type data itself. It also demonstrated local maxima that appeared to be directly tied to the presence of specific vegetation types (e.g., grassland, exotic herb, and chaparral). A comparison of variable importance from the Original and NVT models showed that vegetation type dominated the top 18 variables in the Original model (Figure X). This reliance on vegetation type may have actually been to the detriment of the model and other methods of employing vegetation information may improve results. The removal of vegetation type in the NVT model allowed other variables to dominate the model results, often varying by geographic location (e.g., elevation, aspect).

Areas with low fire susceptibility were often characterized by the presence of water, location near urban centers, or at very high elevations. Higher fire susceptibility regions tended to exist at moderate elevations and included the presence of specific vegetation types (e.g., grassland, chaparral) in the Original model. The NVT model tended to have a larger range in fire susceptibility values, with the greatest number of pixels in the “very low” and “extreme” categories.

**Additional details on all aspects of this project, along with references and citations can be found in the  {{% staticref "files/NeuralNet - Full Report.pdf" "newtab" %}}Full Report{{% /staticref %}}.**

## MSGIS Program Skills

* GIS Analysis
* Spatial Data and Algorithms
* GIS Workflow
* Model Building
* Cartography and Graphic Design
* Spatial Analysis
* Data Model and Structures
* Database Design
* Project Design
* Project Management
* Communication Skills
* Scripting (R and Python)
