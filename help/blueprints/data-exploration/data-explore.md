---
title: Data Exploration & Enterprise Reporting
description: Gain insight from raw data
solution: Experience Platform
kt: 
thumbnail: 
---

# Data Exploration & Enterprise Reporting

Personalize based on online behavior and audience data.

## Use Cases

* Interactive query and aggregation of data
* Row and column access to ingested data for exploration and validation
* Dashboarding and visualization of data via Business Intelligence tooling


## Reference Architecture

<img src="assets/dataexplore.svg" alt="Reference architecture for the Data Exploration and Enterprise Reporting Blueprint" style="border:1px solid #4a4a4a"/>

## Prerequisites

* Adobe Experience Platform

## Guardrails

* 10 minute time out for queries
* 100 records returned in the UI, 50,000 records via SQL connector

## Implementation Steps

1.  Datasets and schemas configured for data ingestion into the data lake
1.  Data ingested
1.  Data is then available by Query Service and Data Science Workspace for raw access and query
1.  Business Intelligence tools and SQL clients can be connected to the Query Service for visualization and data query and exploration.

## FAQs & Reference Documentation

1. [Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
2. [Product Documentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
