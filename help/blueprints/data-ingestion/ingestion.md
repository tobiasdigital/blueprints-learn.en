---
title: Data Preparation and Ingestion Blueprint
description: This blueprint shows all the methods by which data can be ingested and prepared in Adobe Experience Platform.
solution: Data Collection
kt: 7204
thumbnail: 
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1
---
# Data Preparation and Ingestion Blueprint

Data Preparation and Ingestion Blueprint encompasses all the methods by which data can be prepared and ingested into Adobe Experience Platform.

Data preparation includes the mapping of source data to Experience Data Model (XDM) schema. It also includes performing transformations on data, including date formatting, field splitting/concatenation/conversions, and joining/merging/re-keying of records. Data preparation helps unify customer data to provide aggregated/filtered analysis, including reporting or preparing data for customer profile assembly/data science/activation.

## Architecture

<img src="../experience-platform/assets/aep_data_flow.png" alt="Reference architecture for the Data Preparation and Ingestion Blueprint" style="width:80%; border:1px solid #4a4a4a" />

## Data Ingestion Guardrails

The below diagram illustrates the average performance guardrails and latency for data ingestion into Adobe Experience Platform.

<img src="../experience-platform/assets/aep_data_flow_guardrails.png" alt="Experience Platform Data Flow" style="border:1px solid #4a4a4a" width="90%" />

## Data Ingestion Methods

| Methods of Ingestion         | Description                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Web/Mobile SDK               | Latency:<ul><li>Real time - same page collection to Edge Network</li><li>Streaming ingestion to Profile ~1 minute</li><li>Streaming ingestion to data lake (micro batch ~15 minutes)</ul>Documentation: <ul><li>[Web SDK](https://experienceleague.adobe.com/docs/web-sdk.html)</li><li>[Implement Adobe Experience Cloud with Web SDK tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)</li><li>[Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en)</li><li>[Implement Adobe Experience Cloud in mobile apps tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html)</li></ul>                                                                     |
| Streaming Sources            | Latency:<ul><li>Real time - same page collection to Edge Network</li><li>Streaming ingestion to Profile ~1 minute</li><li>Streaming ingestion to data lake (micro batch ~15 minutes)</li></ul>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)                                                                                                                    |
| Streaming API                | Latency:<ul><li>Real time - same page collection to Edge Network</li><li>Streaming ingestion to Profile ~1 minute</li><li>Streaming ingestion to data lake (micro batch ~15 minutes)</li><li>7 GB/hour</li></ul>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F)                                                                                             |
| ETL Tooling                  | Use ETL tools to modify and transform enterprise data before ingestion into Experience Platform.<br><br>Latency:<ul><li>Timing dependent on external ETL tool scheduling, then standard ingestion guardrails apply based on the method used for ingestion.</li></ul>                                                                                                                                                                                                     |
| Batch Sources                | Scheduled fetch from sources<br>Latency: ~ 200 GB/hour<br><br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[Video Tutorials](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html)                                                                                                                                                                                                                                                                                         |
| Batch API                    | Latency:<ul><li>Batch ingestion to Profile dependent on size and traffic loads ~45 minutes</li><li>Batch ingestion to data lake dependent on size and traffic loads</li></ul>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch)                                                                                                                                                        |
| Adobe Application Connectors | Automatically ingest data that is sourced from Adobe Experience Cloud Applications<ul><li>Adobe Analytics: [Documentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors) and [Video Tutorial](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)</li><li>Audience Manager: [Documentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors) and [Video Tutorial](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html)</li></ul> |


## Data Preparation Methods

| Methods of Data Preparation                                | Description                                                                                                                                                                                                                                                                                    |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!UICONTROL Data Science Workspace] - Data Prep                         | Model driven transformation, scripted transformation.<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)                                                                                                                   |
| External ETL Tool ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica], and so on) | Perform complex transformations in ETL tooling and use standard Experience Platform [!UICONTROL Flow Service] APIs or source connectors to ingest the resultant data.                                                                                                                                                               |
| [!UICONTROL Query Service] - Data Prep                                  | Joins, Splits, Merge, Transform, Query, and Filter data into a new dataset. Using Create Table as Select (CTAS) <br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql)                                                                       |
| XDM Mapper & Data Prep functions (Streaming and Batch)     | Map source attributes in CSV or JSON format into XDM attributes during Experience Platform ingestion.<br>Compute functions on data as it is ingested; that is, data formatting, splitting, concatenation, and so on.<br>[Documentation](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |

## Related Blog Posts

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform’s Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
