---
title: Geoprocessing with Python
subtitle: Who Taxes Me?
summary: Python Scripting
tags:
- GIS Analysis
- Spatial Algorithms
- GIS Workflow
- Model Building
- Communication
- Scripting
- Python
date: "2018-12-03"

# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: Snapshot of Python Code
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

* **{{% staticref "files/Python - Presentation.pdf" "newtab" %}}Slides{{% /staticref %}}**
* **{{% staticref "files/Python - Export.pdf" "newtab" %}}Script Output Example{{% /staticref %}}**

## Objective

The objective of this project was to create a Python script tool that answers the question: “Who Taxes Me?” for residents of Utah. To accomplish this, a Python script was written to accept an input address from a user (and optional property value) and provide a simple map of the location/property, a listing of entities that levy taxes on the property, and the levy rate and amount. The listing includes the tax levy as a percentage or, optionally, as a dollar amount if a property value is provided. The data is also presented in bar graph form to visually represent which entities levy higher taxes. Finally, the script produces an automated map of the property location and tax levy information in PDF format.

{{< figure src="Python comic.png" title="Image source: https://www.davegranlund.com/cartoons/2005/01/23/property-tax-bills/" >}}

## Data and Methods

Data for this study was pulled from the Utah Automated Geographic Reference Center [(AGRC) web page](https://gis.utah.gov/data/economy/taxingareas/), which has tax entity datasets available as shapefiles and geodatabase feature classes. The study area incorporates the entire state of Utah and the script works for any address located within the state. The Python code utilizes several different data structures and methods for completing the task, primarily employing the ArcPy module. Data structures include lists, dictionaries, and Pandas dataframes, while the spatial data format is an ESRI geodatabase and feature classes. An outline of the Python script workflow is outline in Figure 1.

{{< figure src="Python diagram.png" title="Figure 1. Diagram of Python script workflow" >}}

## Results

The final results showing the script tool (Figure 2) a code snippet (Figure 3), and the exported PDF document (Figure 4) are shown below:

{{< figure src="Python inputs.png" title="Figure 2. Script tool interface and typical processing dialog window with execution time." >}}

{{< figure src="Python snippet.png" title="Figure 3. Example snippet of Python code." >}}

{{< figure src="Python pdf report.png" title="Figure 4. Example PDF exported by the Python tool." >}}

## Python Libraries
* ArcPy
* Numpy
* Pandas
* Matplotlib

## MSGIS Program Skills

* GIS Analysis
* Spatial Data and Algorithms
* GIS Workflow
* Model Building
* Communication Skills
* Scripting (Python)
