---
title: Advanced Geographic Data Analysis
subtitle: Analyzing Manually-Collected Uber Data to Maximize Driver Earnings in Salt Lake City
summary: Uber Trip Analysis
tags:
- Spatial Analysis
- GIS Analysis
- GIS Workflow
- Spatial Algorithms
- Data Models
- Database Design
- Communication
- Scripting
- Machine Learning
- R
date: "2017-12-13"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Figure 1. Uber trip start and end points, route line density, and end point density.
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

* **{{% staticref "files/Uber Final Report w Figures.pdf" "newtab" %}}Final Report{{% /staticref %}}**

## Introduction

As Uber and other rideshare platforms continue to grow in popularity, the companies amass tremendous amounts of data from the thousands of rides logged every day in major cities (Dogtiev 2017). This data would be extremely useful for municipality planners and engineers, as well as Uber drivers alike. However, Uber understands the power of this and keeps a close hold on the raw data. This study takes a more detailed look at Uber data that was manually-collected in Salt Lake City from August to November of 2017. The goal is to help answer questions, such as:

* Where should drivers position themselves to get the highest-earning rides?
* How accurately can a trip’s earnings be predicted based on a few variables?
* Do trip distances, tips, or earnings differ by rider gender?


A variety of data analysis methods were employed to interrogate the data, including: summary statistics, linear regression, generalized linear models (GLMs), regression trees and random forests, principal component analysis (PCA), geostatistics, and spatial point patterns. These techniques have been applied in a variety of ways throughout the scientific literature over the past few decades and were useful in examining the Uber data. 

## Data and Methods

Data was collected from 125 Uber trips between August and November 2017, primarily on Friday mornings between 5:30-9:30am. Of these 125 trips, the analysis data set was trimmed down to those trips starting in Salt Lake County (117), while the remaining trips (7) were used for model verification. The spatial data were collected with a smartphone GPS application and the attributes were gathered from the Uber app and website. These attributes include trip date, start/end time, duration, distance, driver earning total, surge multiplier, tip, rider gender, latitude, longitude, and an airport trip identifier. Some analyses were conducted on the trip’s total earnings, while other methods used a corrected (standardized) value with the surge multiplier and tips removed. This was done in an effort to remove the seemingly random components of the total earnings. Polyline features from the GPS traces were collected, but the geographical analysis presented here is limited to the trip starting points (and ending points) and their associated attributes (Figure 1).

Of the data collected, a typical trip lasted around 12.5 minutes, covering 4-5 miles with no tip or surge multiplier, resulting in a total driver earning of $5-6. While this trip is considered “typical,” there are a wide variety of trip total earnings, corrected earnings (tip & surge multiplier removed), distances, durations, and tips, as shown in the histograms below (Figure 2). Trip earnings and tips tend to follow an exponential distribution, while distance and duration are closer to normal or gamma distributions. The differences in these distributions created challenges in analyzing the data, resulting in some caveats for interpretation.

{{< figure src="Uber_histograms.png" title="Figure 2. Histograms of total earning (left), distance (center), and duration (right) for all Uber trips." >}}

While only 16.2% of Uber trips end at the airport, airport trips result in higher driver earnings (Figure 3); the mean airport trip earns $11.09, compared to $5.83 for non-airport trips. A T-test confirms that this is a statistically significant result at greater than 99.9% confidence. Additionally, males make up 53.8% of Uber riders, but differences in driver earnings based on rider gender are not statistically significant. Driver total earnings most closely correlated with trip distance, and Figures 4 shows a scatterplot of corrected earnings by distance. These plots also break out gender by color with males (females) in blue (pink), and airport trips by size where non-airport trips (airport trips) are small dots (large dots).

{{< figure src="Uber Box-Whiskers.png" title="Figure 3. Box and whiskers plots of non-airport and airport Uber trips." >}}

{{< figure src="Uber corrected earning (scatter).png" title="Figure 4. Scatterplot of corrected Uber trip earnings by distance, with male/female rider, and airport/not-airport trips symbolized distinctly." >}}

Several methods that were used to analyze the Uber data will be described in the following paragraphs. First, a handful of prediction models will be discussed, followed by geostatistical and spatial point pattern analysis. The first two prediction models were built with linear regression. One was a very simple model that relied purely on distance to predict total earnings -- distance is known to be the largest component of Uber’s actual driver earning calculation. The second model used stepwise automatic selection starting from a null model and with a total scope of 8 variables (distance, duration, surge, tip, gender, airport, longitude, latitude). This resulted in an “optimum” model with 5 variables (distance, duration, tip, surge, gender). The third model was a GLM that used a Poisson distribution and log link function. The fourth and fifth models used regression trees, the fourth of which used a single tree, pruned to a moderately aggressive level of complexity. The fifth model employed a random forest of 500 trees, with 5 variables considered at each split. Finally, principal component regression was used for the sixth model. This applied 4 components resulting from the PCA that accounted for 98.4% of the variance in the data. Once all models were built, they were used to predict total earnings and log-earnings from the 7 data points that fell outside of Salt Lake County.

The next set of analyses consisted of geostatistical prediction and simulation. Ordinary kriging was initially done to estimate total earnings across Salt Lake City based on trip starting points. This was followed by conditional kriging simulations done to estimate the probability of earnings above a certain threshold. Both start and end points were used for kriging simulations, but the end point data proved much more difficult to fit with variograms, resulting in limited success.

## Results

The prediction model results showed a variety of performance skill in estimating the total earnings of the 7 Uber trips that fell outside of Salt Lake County. Using root mean squared errors (RMSE) as the primary metric, the optimized linear model performed the best, followed by the PCR model and random forest model (not shown). All models showed improved performance for log-earnings (vs. total earnings; not shown), except for the PCR model (Figure 5). In this case, the random forest model was the best, followed by the single regression tree and the optimum linear model. The fact that nearly all models performed better with log-earnings, demonstrates that using log-earnings as the dependent variable is probably the best choice for regression modeling, given the distribution mentioned previously.

{{< figure src="Uber model results.png" title="Figure 5. Scatterplot of predicted Uber trip total earning by model (left) and RMSE bar charts by model (right)." >}}

A plot of total earnings based on start points were used to interpolate a surface of values across the Salt Lake Valley with an ordinary kriging technique (not shown). The ordinary kriging results showed relatively high cross-validation errors (not shown) even though the residuals appeared random. A kriging simulation of 50 iterations was conducted across the region to predict the probability of total earnings greater than $8 (Figure 6). The simulation identified similar regions as the ordinary kriging, with the addition of a fourth high-probability region between downtown and the airport. The highest probabilities, approaching 80%, are shown near Kearns and on the east side north of I-80. Total earnings for the Uber end points (Figure 6) were also used for kriging simulations. Figure 22 shows the results, with the airport identified by high probabilities of earnings greater than $8 at 90%. Another, broad region of high probabilities covers the southeast quadrant of the Salt Lake Valley, where only a few data points exist. However, the small sample size and poor variogram fit (not shown) for the end point data make this result highly suspect. The area between downtown Salt Lake City and the university also stands out as trips ending there have very low probabilities (less than 10%) of exceeding $8.

{{< figure src="Uber kriging simulations.png" title="Figure 6. Kriging simulations showing the probability of Uber trip earnings greater than $8 based on trip start points (left) and end points (right)." >}}

**All references and citations can be found in the {{% staticref "files/Uber Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}.**


## MSGIS Program Skills

* GIS Analysis
* Spatial Data and Algorithms
* GIS Workflow
* Spatial Analysis
* Data Models and Structures
* Database Design
* Communication Skills
* Scripting (R)
