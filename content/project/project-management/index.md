---
title: Project Management
subtitle: Rose Park Golf Course GIS Database & Mobile Application 
summary: Golf Course GIS Project
tags:
- Database Design
- SQL
- Data Models
- Cartography
- Project Management
- Project Design
- Communication

date: "2017-11-20"

# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: Rose Park project cost overview
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

* **{{% staticref "files/Rose Park - Presentation.pdf" "newtab" %}}Slides{{% /staticref %}}**
* **{{% staticref "files/Rose Park - Final Report.pdf" "newtab" %}}Final Report{{% /staticref %}}**

## Background

The goal of this course was to come up with an original project that could be used to demonstrate an end-to-end project management lifecycle, to include producing many of the project artifacts, without actually executing the project. In this case, producing a GIS database and mobile application for Salt Lake City’s Rose Park Golf Course was chosen to fulfill this goal. The project work emphasizes the Project Management Body of Knowledge’s ten knowledge areas, with specific focus on Scope, Time, Cost, Quality, Risk, and Procurement Management.

{{< figure src="schematic.png" title="Schematic of Rose Park Golf Course GIS database" >}}

## Introduction

The Salt Lake City Municipal Golf Course system aims to provide an excellent recreation option and golfing experience to citizens, while maintaining a profitable or financially solvent enterprise. However, Salt Lake City’s municipal golf courses have been plagued by financial issues over the last several years due to a variety of factors, including: decreased golf rounds played, uncooperative weather, water costs, and land lease problems (Piper, 2017a). This has resulted in the closure of two golf courses (Jordan River Par 3 and Wingpointe; McKellar, 2015), and the transfer of Rose Park from the Golf Enterprise Fund to the General Fund of Salt Lake City’s budget (Mayor’s Proposed Budget, 2017). Rose Park was removed from the Golf Enterprise Fund because it operated at a net loss of $1.4 Million over the last 10-year period of complete data (2005-2014; Rowland, 2017). The Golf Enterprise Fund is intended to be a self-contained and self-sustaining city-run business venture where golf course profits are re-invested for course improvements. Just a few years ago it operated eight golf courses, but it now operates only five. Rose Park’s move to the General Fund by Mayor Biskupski essentially marks it as a taxpayer-funded course in order to preserve it as a desirable green space and community asset in the broader northwest Salt Lake City recreation area (Piper, 2017b). The move also protects the Golf Enterprise Fund from having to make up for Rose Park’s losses, increasing its own likelihood of success.

Rose Park’s financial struggles have presented Salt Lake City with an opportunity for it to return to profitability through the implementation of innovative solutions. The goal of this project is to implement a detailed GIS database and develop a mobile application to exploit the GIS data for financial benefit. The mobile app will have three primary functions:

1. Golf Course Maintenance: This function will improve the efficiency of resource consumption for golf course and turf maintenance. It will include modules to estimate and predict the needs of water, seed, fertilizer, pesticide/herbicide, etc.
1. Golf Course Management: This function will provide services for golfers, including tee time reservations, snack bar menu navigation, and food purchases. The course will also be able to manage and implement advertising within the application to promote local businesses and increase course revenue.
1. Golfer GPS: This function will help improve the golf experience by exposing the GIS database for detailed distances to course features in a manner unlike any other golf apps on the market. It will help improve the golf experience and pace of play, leading to an increase in golf rounds played each year.

{{< figure src="Rose Park final docs table.png" title="Figure 1. List of Project Management artifacts and deliverables" >}}

In turn, this project will help spur cost savings, increase the number of golfers at Rose Park, and increase profits by adding a new revenue stream through in-app advertising. If successful, this project will restore Rose Park’s financial stability, allowing it to return to the Golf Enterprise Fund with a positive impact. Additional details on the project, artifacts, and deliverables (Figure 2) can be found in the full project report and documentation. A few of these artifacts have been selected for discussion below.

{{< figure src="Rose Park timeline.png" title="Figure 2. Timeline for the Rose Park GIS Database & Mobile Application project" >}}

## Scope Management

The Rose park project will need to be completed on a precise timeline in order for the benefits to be realized at the start of the 2018 spring golf season. For this reason, scope management is critical to ensure that the work focuses on the agreed upon requirements and stakeholder needs. The documents below help define and control what work will be included in the project.

Broad requirements outlining the scope of the project are listed below:

1.	Build comprehensive GIS database with features representing tees, greens, fairways, bunkers, water hazards, and other golf course infrastructure items.
1.	Provide enough attributes in the GIS database to improve the golf experience and course maintenance operations.
1.	Develop a mobile app with two primary interfaces:
	* Staff interface for course maintenance and golf management functions
	* Public interface for golfers to access GPS distances and snack bar features
1.	Mobile app capability for in-app advertising to increase revenue
1.	Mobile app capability for food/drink menu editing, viewing, and purchasing


**Business Case Financials**

As an attachment to the business case, the financials spreadsheet goes into detail on how the costs and benefits were estimated and how they are distributed over time, including discounted costs. This ultimately results in the calculation of ROI and NPV, as well as the payback period. Each of these elements are important in making a decision on whether or not to pursue a project. The calculation of numbers in the business case financials is further detailed in the cost estimate and benefit estimate spreadsheets attached to the final report.

{{< figure src="Rose Park business case financials.png" title="Figure 3. Business case financial analysis" >}}

## Time Management

Along with scope management, time management is the other key aspect to ensure the Rose Park project is completed on time.  The documents below were developed to provide tracking and a solid plan for the project schedule.

**Gantt Chart**

A Gantt chart was created from the WBS described in the full report using MS Project and relied on the aforementioned dependencies and resources (shown on the chart) for auto-scheduling.  It also displays summary tasks and identifies project milestones as red diamonds.  The Gantt chart will be updated as the project progresses, using MS Project’s tracking functions.

{{< figure src="Rose Park Gantt Chart.png" title="Figure 4. Gantt chart showing projects tasks and timeline" >}}

## Quality Management


A high quality mobile app is needed to provide the services required by the management/maintenance staffs and to compete with commercial GPS golf apps.  In order manage quality for the Rose Park project, stakeholder involvement will be relied on to provide quality assurance through multiple stakeholder acceptance instances and extensive user acceptance testing.

**Quality Management/Testing Process**

The quality management and testing process flow chart describes the quality assurance/testing components in detail.  Using Agile concepts, stakeholders will be involved from start to finish in the software development phase.  This will begin with requirements definition and prototype acceptance and continue with several “gates” of stakeholder acceptance.  Each sprint will have an iterative process of unit-level and integration testing, followed by bug fixes, and ending with a sprint demo and stakeholder acceptance.  Software development will then be concluded with system-wide testing and stakeholder-driven user acceptance testing.  The GIS database development is more straightforward and has a simpler quality management process.  This will primarily consist of peer review among the GIS technicians, employing cause and effect diagrams when issues develop, and unit and integration testing for each database component.

{{< figure src="Rose Park quality mgmt.png" title="Figure 5. Quality management and testing process for mobile application and GIS database" >}}

## Risk Management

With the previous financial struggles of Rose Park and thin margins in the overall golf course industry, project failure would be catastrophic for the course.  To combat these perils, risk will be mitigated with the use of a risk register and probability/impact matrix, and updated frequently during bi-weekly risk review meetings.

**Risk Register**

The risk register identifies several of the project’s biggest risks, along with a description, category, root cause, triggers, potential responses, and the risk owner for each.  A probability and impact are also defined that, in conjunction with the risk matrix (not shown), help highlight risks that need to be monitored most closely.  These risks are colored and ranked by their total risk score and ordered accordingly in the register.  Those at the top pose the greatest threat.  As situations change throughout the project, the risk register and statuses will be updated during the risk review meetings.

{{< figure src="Rose Park risk register.png" title="Figure 6. Risk register" >}}

## Summary


Recent struggles encountered by Salt Lake City golf courses have provided an opportunity for innovative solutions to improve profitability.  The Rose Park GIS database and mobile application proposed here describe a path forward to return the city’s most troubled course to financial stability.  This project has the support of the Mayor, an interested and enthusiastic set of stakeholders, a realistic plan, and resources available to execute the plan.  The time has come to leverage data and technology to increase efficiency and profits for Rose Park.

**All references and project artifacts can be found in the {{% staticref "files/Rose Park - Final Report.pdf" "newtab" %}}Full Report{{% /staticref %}} and attachments.**

## MSGIS Program Skills

* Cartography and Graphic Design
* Data Model and Structures
* Database Design
* Structured Query Language (SQL)
* Project Design
* Project Management
* Communication Skills
