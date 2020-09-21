---
title: Spatial Modeling
subtitle: A Simplified Fire-Evacuation Model for Eagle Mountain, Utah
summary: Simple Wildfire Modeling
tags:
- GIS Analysis
- Spatial Algorithms
- GIS Workflow
- Model Building
- Data Models
- Project Design
- Project Management
- Communication
- Scripting
- R
date: "2018-05-03"

# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: 'Image source: https://kutv.com/news/local/utah-on-fire-wildfires-erupt-across-the-state'
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

* **{{% staticref "files/Fire-Evac - Full Report.pdf" "newtab" %}}Full Report{{% /staticref %}}**
* **{{% staticref "files/Fire-Evac Model ODD Protocol.pdf" "newtab" %}}Model Description Document{{% /staticref %}}**
* **{{% staticref "files/Fire-Evac NetLogo code.txt" "newtab" %}}NetLogo Code{{% /staticref %}}**


## Background

In recent decades, the population in the US has grown outward from urban centers and begun to encroach on the urban-wildland interface, putting developments and communities in jeopardy of being affected by wildfires. This has become more common occurrence and will continue to be as populations increase along with extreme precipitation and drought events. To help analyze this problem we hope to build a model to simulate wildfire spread and community evacuation within a wildland-urban setting. This type of model could be useful when attempting to make planning decisions and informing populations of risk when developing within these areas.

Eagle Mountain, Utah is relatively new area of development with rapid growth along the urban-wildlife interface. This growth puts some locations at risk of wildfire due to their proximity to vulnerable vegetation in the nearby hills. This research seeks to model the potential impacts of wildfire on the surrounding area and to recommend some evacuation strategies to local residents. An approach for modeling wildfire dispersion patterns can be done with a percolation model. The percolation model will combine vegetation, elevation and fire threat layers to observe the probability of wildfire occurrence and its characteristics within the study area. Agent based modeling can be used to find out what evacuation strategies will work best under the local context. It can be assumed that each household will possess one vehicle (agent) and the optimal routing options (ruleset) to evacuate the total number of vehicles will be designated through this study. Implementing this model will help to observe how wildfire from varying points of origin will produce different routing patterns.

## Data and Methods

The model designed in this project simulates wildfire ignition and spread in the vicinity of Eagle Mountain, Utah and subsequent evacuation using a simplified road network. To test the model and learn how changes in parameters impact the simulation outcome, a suite of experiments were run using the NetLogo BehaviorSpace tool. Datasets used within the model include a Fire Threat raster from Utah’s Department of Natural Resources (DNR), which is used to determine where the initial fire starts. Vegetation data from the DNR is used to set the vegetation density, which affects the probability that patches neighboring a currently burning patch catch fire. A digital elevation model from DNR is also used to modify the probability of fire spread. Finally, a road network from the city of Eagle Mountain was simplified and used as the road network for vehicles evacuating neighborhoods.

{{< figure src="Fire-Evac table1.png" title="Table 1. Parameter values used in model setup. Bracketed values indicate a range, notated in the following manner: [low-value step high-value]." >}}

The model has adjustable parameters for the probability of fire ignition in each cardinal direction (e.g. “ignitionS”), the probability of fire extinction (“extinction”) at each time step, and the probability that exiting cars will correctly follow their evacuation route when they approach an intersection (“q”). To experiment with the model, two primary experiments were designed, one representing a fire in southwesterly winds and one representing a fire in northwesterly winds. These two scenarios represent the most likely directions for strong winds during a wildfire event. This is particularly true for the southwesterly scenario, which typically occurs in a dry environment ahead of approaching low pressure systems. These experiments are run over a variety of settings for “extinction” and “q”, with each permutation run for 25 iterations. Table 1 describes the model setup; brackets indicate a range of values in the following manner: [low-value step high-value]. An example screenshot of a typical model run in mid-simulation is shown in Figure 1.

{{< figure src="Fire-Evac model snapshot.png" title="Figure 1. Example screenshot of typical model run." >}}

## Results

The outcomes from the two model scenarios showed several similar results, but also indicated a few subtle differences. Based on the combination of parameters used in the experiment, the most frequent model result burned less than 2.5% of the landscape (34% of simulations) and finished with 0 burned cars (45.3%; Figure 2). In fact, in 25.2% of simulations, the fire did not cross the neighborhood buffer and no evacuation was initiated. As expected, the percentage of the landscape and the number of cars burned decreased as the fire extinction rate increased (Figure 3). Both of these statistics were maximized when the fire extinction rate was zero. Interestingly, the southwesterly wind scenario (2.87) resulted in an average of 1 more car being burned per simulation than the northwesterly wind scenario (1.82). Figure 3 also indicates a higher median number of cars burned in the southwesterly scenario for each extinction value below 0.4.

{{< figure src="Fire-Evac fig2.png" title="Figure 2. Histogram of percent landscape and cars burned by scenario." >}}

{{< figure src="Fire-Evac fig3.png" title="Figure 3. Box plots of percent landscape and number of cars burned by varying levels of extinction in southwesterly and northwesterly wind scenarios." >}}

Of the simulations resulting in evacuation, there was a weak relationship between the number of cars burned and “q” (Figure 4), but it is not likely significant. This subtle trend indicates that fewer cars burn at higher “q” due to more efficient evacuation, while more cars burn at lower “q” due to more wrong turns and a longer evacuation process. This is also reflected in the duration of the simulation, where wrong turns (lower “q”) lead to slower evacuation and a longer median simulation (Figure 4).

{{< figure src="Fire-Evac fig4.png" title="Figure 4. Box plots of number of cars burned and simulation duration by varying levels of “q” in southwesterly and northwesterly wind scenarios. The “q” variable represents the probability that a vehicle makes the correct decision at an intersection to evacuate as efficiently as possible." >}}

Finally, Figure 5 shows plots (only for simulations with evacuation) of average percentage of landscape burned, cars burned, and simulation duration as a function of both extinction and “q”. For both wind scenarios, the maximum percentage of the landscape burned occurs when “q” is minimized and the extinction rate is zero. This is expected as low “q” values prolong the simulation and the fires never actually burn out when the extinction rate is zero. The southwesterly scenario also has a greater maximum percentage burned. This is likely because the fire is designed to start near the western and southern edges of the model domain, leaving more land downwind of the fire origin when there is a southerly component to the wind. A northerly wind component tends to push fires starting near the southern border out of the model domain. Intuitively, the maximum number of cars burned occurs at the minimums of extinction rate and “q.” This combination leads to more burned cars due to widespread fires and the slow evacuation from cars making wrong turns at intersections, as discussed previously. For the simulation length, there appears to a “sweet spot” of maximum duration where low, but non-zero extinction rates lead to a slow burning fire and low “q” values result in slower evacuations. Duration quickly drops off at higher extinction rates (0.4+) where the fires burn out quickly. The northwesterly wind scenario also had a higher maximum average simulation length than the southwesterly scenario, though it’s not entire clear why. Perhaps the low extinction rates allow fires starting on the southern periphery of the domain to burn back northward against the wind, resulting in slow-but-steady progression and long simulations when “q” is low.

{{< figure src="Fire-Evac fig5.png" title="Figure 5. Percentage of landscape burned (top), cars burned (middle) and simulation duration (bottom) as a function of both extinction and “q”." >}}

## Conclusions

While this model simulation is far from realistic, it does represent some of the basic processes in the real world. These include fire spread due to properties of vegetation, wind, and elevation, and first draft vehicle evacuation logic. Recommended future work on the model would include better scaling of fire/vehicle speeds, more robust traffic logic, and evacuations by specific neighborhood. Though relatively simple, the current model is still capable of reproducing some realistic results. This includes larger, longer-burning fires when the extinction probability is low or zero. It also demonstrates that vehicles taking wrong turns while evacuating the neighborhood will take longer to exit and, therefore, be more likely to be burned in the fire. Finally, it indicates that Eagle Mountain may be at greater risk from a fire in southwesterly winds, which is likely to burn a larger area and endanger more vehicles, than a fire in northwesterly winds.

**Additional details on the methodology and results, and all references can be found in the {{% staticref "files/Fire-Evac - Full Report.pdf" "newtab" %}}Full Report{{% /staticref %}}.**

## MSGIS Program Skills

* GIS Analysis
* Spatial Data and Algorithms
* GIS Workflow
* Model Building
* Data Model and Structures
* Project Design
* Project Management
* Communication Skills
* Scripting (NetLogo)
