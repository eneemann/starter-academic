---
title: Web GIS
subtitle: Montana Water Usage Web Map
summary: Web Mapping
tags:
- Spatial Algorithms
- Cartography
- Communication
- Scripting
- JavaScript
date: "2018-04-18"

# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: ''
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

* **{{% staticref "files/Web GIS - presentation.pdf" "newtab" %}}Slides{{% /staticref %}}**

## Overview

**Note: the servers that hosted the web page for this project were retired in 2018, so a live version of the page no longer exists**

As a result of changes in climate and population growth, there has been increased competition for freshwater in the Western U.S. in recent decades. This trend is likely to intensity in the future as populations continue to grow and uncertainty surrounding the climate in the Intermountain West continues. The objective of this project was to investigate county-level water consumption in Montana through the creation of a web map (Figure 1). Specifically, surface water usage and sources were mapped and explored.

{{< figure src="Web GIS full page big.png" title="Figure 1. Screenshot of final web page." >}}

## Data & Methods
The primary data sets for this project include:
-	Excel spreadsheet with county-level water consumption statistics from 2010
-	Shapefile of Montana county boundaries (polygons)
-	Shapefile of Montana rivers and streams (polylines)
-	Shapefile of Montana lakes (polygons)
-	Shapefile of Montana cities (points)

First, to prepare the data for consumption by the web map, the spreadsheet was joined to the counties shapefile to link surface water statistics to their geographic region.  Second, all shapefiles were loaded into an ArcMap document, labelled, and symbolized.  Third, the data was published as a map service, which was later consumed by the web page using the ArcGIS JavaScript API v4.3.  Additional organization of the web page and customization of features was completed through a combination of HTML, CSS, and JavaScript coding (Figure 2).

{{< figure src="Web GIS code.png" title="Figure 2. Snapshot of JavaScript code." >}}

## Functionality

The finished web page had the following functionality:

* Query information with a pop-up window on click (Figure 3)
  * County Name
  * Population
  * Area
  * Surface Freshwater Withdrawals
  * Total Water Withdrawals
* Layer list toggle on/off capability
* Basemap toggle between “streets” and “satellite”
* Legend display
* Zoom in/out by scroll or widget

{{< figure src="Web GIS popup.png" title="Figure 3. Example of pop-up functionality." >}}

## Data Sources

* Montana State Library Geographic Information Clearinghouse [http://geoinfo.msl.mt.gov/](http://geoinfo.msl.mt.gov/)

## MSGIS Program Skills

* Spatial Data and Algorithms
* Cartography and Graphic Design
* Communication Skills
* Programming and Scripting (HTML, CSS, JavaScript)
