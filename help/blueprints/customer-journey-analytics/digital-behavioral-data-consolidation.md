---
title: Cross Channel Journey Analysis
description: Analyze and extract insights from customer interactions across the customer journey.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
exl-id: b042909c-d323-40d5-8b35-f3e5e3e26694
---
# Cross Channel Journey Analysis Blueprint

Have a single consolidated view of customer behavior across various channels by unifying data from various web, mobile, and offline properties.

## Use Cases

* Analyze customer interactions across desktop and mobile to understand customer behavior and extract insights to optimize digital customer experiences.
* Analyze customer interactions across channels, including digital and offline channels such as support interactions and in-store purchases to better understand and optimize the customer journey. 

## Applications

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics (optional)

## Integration Patterns

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## Architecture

<img src="assets/CJA.svg" alt="Reference architecture for the Customer Journey Analytics Blueprint" style="border:1px solid #4a4a4a" />

## Implementation Steps

1. [Create schemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) for data to be ingested.
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) for data to be ingested.
1. Ingest data[Ingest Data Tutorial](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) into Experience Platform.
    Data must be ingested into Platform before processing into Customer Journey Analytics. For further information on data ingestion and types of data sources see the following documentation. [Data Sources](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en) including the [Analytics Data Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en)
1. Analyze cross-channel event datasets to be analyzed in union to make sure they have a common namespace ID or are rekeyed through the field-based stitching capability of Customer Journey Analytics. See the cross channel analytics documentation for further information on identity stitching in Customer Journey Analytics. [Identity Stitching](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/cca/overview.html?lang=en)
 
    >[!NOTE]
    >
    >Customer Journey Analytics does not currently use the Experience Platform Profile or Identity services for stitching.

1. Perform any custom data preparation or use of the field-based identity stitching on the data to ensure a common key across time series datasets to be ingested into Customer Journey Analytics.
1. Give lookup data a primary ID that can join to a field in the event data. Counts as rows in licensing. 
1. Set the same primary ID for profile data as the primary ID of the event data.
1. Configure a data connection to ingest data from Experience Platform to Customer Journey Analytics. After data lands in the data lake, it processes into Customer Journey Analytics within 90 minutes.
1. Configure a data view on the connection to select the specific dimensions and metrics to be included in the view. Attribution and allocation settings are also configured in the data view. These settings are computed at report time.
1. Create a project to configure dashboards and reports within Analysis Workspace.

## Implementation Considerations

### Identity Stitching Considerations

* Time-series data to be unioned must have the same ID namespace on every record.
* The union process of unifying disparate datasets requires a common primary person/entity key across the datasets. 
* Secondary key-based unions are not supported currently.
* The field-based identity stitching process allows for rekeying identities in rows based on subsequent transient ID records, such as an authentication ID. This allows for resolving disparate records to a single ID for analysis at the person level rather than at the device or cookie level.
* Stitching happens once a week, with replay after the stitch.

## FAQs

* What are the downstream impacts of data models in Customer Journey Analytics?

    Objects and attributes of the same XDM field merge into one dimension in Customer Journey Analytics. To  merge multiple attributes from various datasets into the same Customer Journey Analytics dimension, the datasets should reference the same XDM field or schema.

## Related Documentation

* [Customer Journey Analytics product description](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics documentation](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Customer Journey Analytics tutorials](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
