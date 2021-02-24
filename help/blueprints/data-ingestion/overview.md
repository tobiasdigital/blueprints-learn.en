---
title: Data Preparation and Ingestion
description: Prepare and ingest data for modeling, analysis and activation in Experience Platform
solution: Experience Platform
kt: 
thumbnail: 
---

# Data Preparation and Ingestion

## Description

The data ingestion and preparation blueprint encompasses all the methods by which data can be ingested and prepared in Adobe Experience Platform. 

Data preparation includes the concepts of mapping source data to XDM (Experience Data Model) schema, as well as performing transformations on data including date formatting, field splitting and concatenation, conversions, as well as joining, merging and re-keying of records to facilitate unifying customer data, providing aggregated or filtered reporting and analysis, or preparing data for customer profile assembly, data science, and activation.

![Data Ingestion](assets/dataingest.svg)


## Data Ingestion Methods

| Methods of Ingestion         | Description                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Web/Mobile SDK               | Latency:<br>Real-time - same page collection to Experience Edge<br>Streaming ingestion to Profile ~1 min<br>Streaming ingestion to Data Lake (micro batch ~15 minutes)<br>Documentation: <br>[WebSDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en)<br>[MobileSDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en)                                                                     |
| Streaming Sources            | Latency:<br>Real-time - same page collection to Experience Edge<br>Streaming ingestion to Profile ~1 min<br>Streaming ingestion to Data Lake (micro batch ~15 minutes)<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)                                                                                                                                               |
| Streaming API                | Latency:<br>Real-time - same page collection to Experience Edge<br>Streaming ingestion to Profile ~1 min<br>Streaming ingestion to Data Lake (micro batch ~15 minutes)<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F)                                                                                              |
| ETL Tooling                  | Use ETL tools do modify and transform enterprise data prior to ingestion into AEP.<br>Latency:<br>Timing dependent on external ETL tool scheduling then standard ingestion guardrails apply based on the method used for ingestion.                                                                                                                                                                                                     |
| Batch Sources                | Scheduled fetch from sources<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)                                                                                                                                                                                                                                                                                         |
| Batch API                    | Latency:<br>Batch ingestion to Profile dependent on size and traffic loads ~45 min<br>Batch ingestion to Data Lake dependent on size and traffic loads<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch)                                                                                                                                                        |
| Adobe Application Connectors | Automatically ingest data that is sourced from Adobe Experience Cloud Applications<br>[Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors)<br>[Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors) |






## Data Preparation Methods

| Methods of Data Preparation                                | Description                                                                                                                                                                                                                                                                                    |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Data Science Workspace - Data Prep                         | Model driven transformation, Scripted transformation.<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)                                                                                                                   |
| External ETL Tool (Snaplogic, Mulesoft, Informatic, etc.) | Perform complex transformations in ETL tooling and leverage standard AEP Source APIs or Connectors to ingest the resultant data.                                                                                                                                                               |
| Query Service - Data Prep                                  | Joins, Splits, Merge, Transform, Query and Filter data into a new dataset. Using CTAS (Create Table as Select)<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql)                                                                       |
| XDM Mapper & Data Prep functions (Streaming and Batch)     | Map source attributes in CSV or JSON format into XDM attributes during AEP ingestion.<br>Compute functions on data as it is ingested - i.e. data formatting, splitting, concat, etc.<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |
