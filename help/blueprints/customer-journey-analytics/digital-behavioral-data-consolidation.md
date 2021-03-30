---
title: Digital Behavioral Data Consolidation scenario
description: Analyze and extract insights from customer interactions across the customer journey.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
---

# Digital Behavioral Data Consolidation scenario

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

## Guardrails

Data Ingestion into Customer Journey Analytics:

* Data ingestion to lake: API ~ 7 GB/hour, source connector ~ 200 GB/hour, streaming to lake ~ 15 minutes, Adobe Analytics source connector to lake ~ 45 minutes.
* After data has been published to the data lake, it can take up to 90 minutes to process into Customer Journey Analytics.

## Implementation Steps

1. Configure datasets and schemas.
1. Ingest data into Platform.
    Data must be ingested into Platform before processing into Customer Journey Analytics. 
1. Analyze cross-channel event datasets to be analyzed in union to make sure they have a common namespace ID or are rekeyed through the field-based stitching capability of Customer Journey Analytics. 
 
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




