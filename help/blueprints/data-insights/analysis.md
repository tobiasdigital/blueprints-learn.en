---
title: Data Analysis and Intelligence Blueprint
description: This blueprint shows the ability within Adobe Experience Platform to perform exploratory query and analysis of the data that exists in the data lake.
solution: Experience Platform
kt: 7207
thumbnail: 
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441

---
# Data Analysis and Intelligence Blueprint

Data Analysis and Intelligence comprises the ability within Adobe Experience Platform to perform exploratory query and analysis of the data that exists in the data lake.

Experience Platform's [!UICONTROL Query Service] allows SQL queries to be performed on the data. [!UICONTROL Data Science Workspace] enables data exploration, data science, and machine learning workloads to be performed on the data. 

In addition, Experience Platform allows connections with third-party SQL clients, interfaces, and Business Intelligence (BI) tools to directly connect to, access and query the data within Experience Platform, using the [!DNL PostgreSQL] protocol.

Certain guardrails apply for the query timeout and for the amount of data that is included in the query result, as noted within the blueprint details.

## Use Cases

* Interactive query and aggregation of data
* Row and column access to ingested data for exploration and validation
* Dashboarding and visualization of data via Business Intelligence tooling

## Applications

* Adobe Experience Platform

## Architecture

<img src="assets/data_exploration.svg" alt="Reference architecture for the Enterprise Data Exploration and Reporting Blueprint" style="width:80%; border:1px solid #4a4a4a" />

## Guardrails

Refer to the Query Service Product Documentation for details on best practices and guardrails.
[Query Service Guidance](https://experienceleague.adobe.com/docs/experience-platform/query/best-practices/writing-queries.html?lang=en#best-practices)

## Implementation Steps

1. [Create schemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) for data to be ingested.
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) for data to be ingested.
1. [Ingest data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) into Experience Platform.
1.  Confirm that data is available to [[!UICONTROL Query Service]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=en) and [[!UICONTROL Data Science Workspace]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/load-data-in-jupyterlab-notebooks.html?lang=en) for raw access and query.
1.  [Connect Business Intelligence tools and SQL clients to [!UICONTROL Query Service]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.qsvc.dash) for visualization, data query, and exploration.

## Related Documentation

* [Adobe Experience Platform Intelligence product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Query Service] documentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
