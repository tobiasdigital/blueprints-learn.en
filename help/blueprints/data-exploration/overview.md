---
title: Data Prep and Enterprise Reporting Blueprint
description: placeholder description
solution: Experience Platform
kt: 
thumbnail: 
---

# Data Prep and Enterprise Reporting Blueprint

## Description

Data Exploration & Enterprise Reporting comprises the ability within Adobe Experience Platform to perform exploratory query and analysis of the data that exists in the Experience Platform Data Lake.

Experience Platform's Query Service allows SQL queries to be performed on the data, while the Data Science Workspace enables data exploration, data science, and machine learning workloads to be performed on the data. 

In addition Experience Platform's SQL Connector allows connections with third-party SQL clients and interfaces and Business Intelligence tools to directly connect to, access and query the data within Experience Platform utilizing the PostgreSQL protocol.

Certain guardrails apply for the query time out and for the amount of data that is included in the query result as noted within the scenario details.

## Use Cases

* Interactive query and aggregation of data
* Row and column access to ingested data for exploration and validation
* Dashboarding and visualization of data via Business Intelligence tooling

## Scenarios

| Scenario | Description |  Experience Cloud Applications/Services | 
|---|---|---|
| **Data Exploration - raw query of data**  | <ul><li>Write and perform SQL queries in the Experience Platform Data Lake using the interactive query user interface or connecting with a SQL client. Data Science Workspace can also be used to query and gain insight from the raw data in Experience Platform.</li></ul> | <ul><li>Adobe Experience Platform</li></ul>|
| **Enterprise Dashboarding**  | <ul><li>Business Intelligence tools can be connected to Experience Platform to visualize data for dashboarding and reporting use cases.</li></ul> | <ul><li>Adobe Experience Platform</li></ul>|  

## Reference Architecture

![Data Exploration](assets/dataexplore.svg)

## Prerequisites

* Adobe Experience Platform

## Guardrails

* 10 minute time out for queries
* 100 records returned in the UI, 50,000 records via SQL connector

## Implementation Steps

* Datasets and schemas configured for data ingestion into the data lake
* Data ingested
* Data is then available by Query Service and Data Science Workspace for raw access and query
* Business Intelligence tools and SQL clients can be connected to the Query Service for visualization and data query and exploration.

## FAQs & Reference Documentation

1. [Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
2. [Product Documentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
