---
title: Spatial Database Design
subtitle: Utah Recreation Database
summary: Recreation Database
tags:
- Database Design
- SQL
- Data Models
- Cartography
- Project Management
- Communication
date: "2017-12-04"

# Optional external URL for project (replaces project detail page).
external_link: ""

# links:
# - name: Final Report
#   url_pdf: files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}

image:
  caption: Snapshot of Entity-Relationship diagram
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

* **{{% staticref "files/Recreation Database Slides.pdf" "newtab" %}}Slides{{% /staticref %}}**
* **{{% staticref "files/Recreation Final Report w Figures.pdf" "newtab" %}}Final Report{{% /staticref %}}**


## Introduction

This project presents a statewide recreation database for Utah. The database gathers many recreational datasets in one place for Utahns to explore and use to plan trips or activities. A variety of data related to hiking, camping, skiing, canyoneering, swimming/boating, golfing, and parks/wilderness are included. The data are associated through relationship classes (where appropriate), to help query and make sense of inherent connections. Some example queries the database helps to answer include:

* What trailheads provide access to Goblin Valley’s Dark Side of the Moon trail?
* How many ski lifts are in the ski resort containing “Chips Run?”
* What boat ramps provide access to Lake Powell?


With a wide variety of functionality, users are able to use the database to find the necessary trailhead for their desired hiking route (Figure 1) or determine what runs and lifts are available to them at a ski resort. Users can also determine what boat ramps provide access to a specific lake or river, identify which campgrounds in Washington County have more than 50 campsites, and see what Utah peaks are higher than 13,000 feet above sea level. This represents just a small sampling of information that the database can provide.

{{< figure src="Recreation overview.png" title="Figure 1. Snapshot of layers in the Utah Recreation Database" >}}


## Conceptual Model

A conceptual Entity-Relationship diagram was created based on the integrity constraints for the project (Figure 2). In this diagram, each dataset is represented by a rectangular entity, and the relationships between entities are represented by diamonds. The ovals depict attributes belonging to each of the entities. Most of the relationships are one-to-many, meaning one entity connects to many other entities through the relationship (e.g., one ski resort contains many ski runs and ski lifts). The exception to this is the many-to-many relationships between trailheads, trail segments, and trail routes (e.g., several trailheads can initiate one route and several routes can begin at one trailhead).

The double lines connecting some entities to a relationship indicate that the specific entity is required to participate in the relationship. For example a ski lift must be within a ski resort, and a boat ramp must be adjacent to a river or lake. The third mandatory participation constraint is for the disjoint subtype of parks. This means that parks must either be local, state, or national parks, but they can only be in one of those three categories. Finally, among the attributes of each entity, the underlined attribute is the unique identifier for the entity that links allows it to be linked to other entities through the relationships.

{{< figure src="Recreation conceptual model.png" title="Figure 2. Conceptual Model: Entity-Relationship Diagram" >}}

## Logical Model

The conceptual Entity-Relationship diagram was translated into a logical Relational Model diagram (Figure 3).  In this process, primary and foreign keys were specified for each relation (entity) and many-to-many relationships were connected through the creation of an additional relation.  Further, domains where added for each attribute, to include data type and length constraints.  Three many-to-many relationships exist in the Utah Recreation Database, so relations were added for each.  An “Initiation” relation was added between both Trailheads and Trail Routes and between Trailheads and Trail Segments.  A “Connection” relation was also added between Trail Segments and Trail Routes.  For the Boat Ramp relation, the “Water_body” attribute is used as the foreign key to both the Lake and River relations to connect Boat Ramps to appropriate water bodies.  Finally, the Park supertype relation is linked to the “Local_Park,” “State_Park,” and “National_Park” subtype relations, where each park ID is both a foreign key and primary key.

{{< figure src="Recreation logical model.png" title="Figure 3. Logical Model: Relational Model Diagram" >}}

## Physical Model

To translate the logical relational model into a physical model, a geodatabase was created and populated in ArcCatalog (Figure 4). A feature class was imported or created for each dataset and relationship classes were created to link feature classes together, where appropriate. Several of the relationship classes were simple, one-to-many relationships placing the feature within the state. However, a few required more careful design. The many-to-many relationships among trailheads, trail segments, and trail routes were created by selecting appropriate features and adding them to the associated relationship class’s table. Additionally, boat ramps were linked to their adjacent rivers and lakes through relationship classes and ski lifts and ski runs were connected to their parent ski resorts. In its completed form, the geodatabase provides a coherency to the data that enables additional functionality as described below.

After putting the recreation database together, new functions are now available that weren’t possible when the datasets were disparate. This can be demonstrated by answering the questions in the introduction. In ArcMap, the trailheads leading to Goblin Valley’s “Dark Side of the Moon” trail can be identified by selecting the trail and finding its associated trailheads by clicking on the “TH_to_Routes” relationship class. By selecting “Chip’s Run” from the ski runs dataset and clicking on the “SkiResort_SkiRuns” relationship class, Snowbird is identified as the resort. Snowbird’s attributes note that it contains 11 ski lifts. Lastly, Lake Powell’s boat ramps can be found by selecting the lake and using the “Lakes_BoatRamps” relationship class. All of these functions, and many more, can now be executed quickly and easily to interrogate the database to meet a user’s needs.

{{< figure src="Recreation physical model.png" title="Figure 4. Physical Model: ESRI File Geodatabase" >}}

## Future Work

While this database ended up relatively complete, there are several improvements that could be made in the future. Most of the datasets were gathered from open sources (listed in the report), resulting in inconsistent or minimal attributes. For example, it would be informative to have starting elevation, ending elevation, and vertical gain data for the ski runs, trail routes, etc. Additional attribute improvements or geometry changes would also lead to a better overall database (e.g., slot canyons represented as line segments). In some cases, the data were trimmed into subsets to make it more manageable (only ski runs in Snowbird were used, trail segments/routes were clipped to the San Rafael Swell/Goblin Valley region), so including more complete data would provide a better product. Finally, adding datasets for more recreation options would also produce a more comprehensive database (rock climbing locations, whitewater rafting/kayaking areas, etc.).

**A complete accounting of datasets, business rules, and references can be found in the {{% staticref "files/Recreation Final Report w Figures.pdf" "newtab" %}}Full Report{{% /staticref %}}.**

## MSGIS Program Skills

* Spatial Data and Algorithms
* Cartography and Graphic Design
* Data Models and Structures
* Database Design
* Structured Query Language (SQL)
* Project Management
* Communication Skills
