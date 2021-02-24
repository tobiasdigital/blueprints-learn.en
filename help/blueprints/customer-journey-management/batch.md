---
title: Customer Journey Analytics - Cross-site and Cross-channel Analysis Scenario
description: Cross site and cross channel customer journey analysis
solution: Experience Platform, Customer Journey Analytics
kt: 
thumbnail: 
---

# Cross-site and Cross-channel Customer Journey Analysis scenario

Analyze and extract insights from customer interactions across the customer journey.

## Use Cases

* Unify customer interactions across desktop and mobile to analyze customer behavior and extract insights to optimize digital customer experiences.
* Unify customer interactions across channels, including digital and offline channels such as support interactions or in store purchases to better understand and optimize the customer journey. 

## Reference Architecture

![Scenario 1](assets/CJA.svg)

## Integration Patterns

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics


## Prerequisites

* Adobe Experience Platform
* Customer Journey Analytics


## Guardrails

Availability: Global

Sandbox support: Sandbox compliant (Org must be enabled for sandboxing) datasets from sandboxes can be selected in the CJA Connector configuration. One sandbox per connector.

Data Ingestion into CJA:

* Data Ingestion to Lake: API – 7GB/hr, Connector – 200GB/hr, streaming to lake ~15min, Analytics connector to lake ~45min
* Once data has been published to Data Lake, it can take up to 90 mins to ingest into CJA.
* Backfill data for loading historical data is also supported via the connection configuration.

## Implementation Steps and Considerations

* Data must be ingested into Platform prior to ingestion into CJA. Datasets and schemas configured and data ingested into Platform.
* Cross channel event datasets to be analyzed in union must have a common namespace id or be re-keyed through the field based stitching capability.  *Note that CJA does not utilize the AEP Profile or identity services for stitching today.
* Any custom data preparation or use of the field based identity stitching is performed on the data to insure a common key across time series datasets to be ingested into CJA.
* Lookup data must have a primary ID that can join to a field in the event data. Counts as rows in licensing.
Profile data must have the same primary ID as the primary ID of the event data.
* A data connection is configured to ingest data from AEP to CJA. Once data lands in the data lake it will process into CJA within 90 minutes.
* A data view is configured on the connection to select the specific dimensions and metrics to be included in the view. Attribution and allocation settings are also configured in the data view. These settings will then be computed at report time.
* A project is then created to configure dashboards and reports within Analysis Workspace.

Identity Stitching Considerations

* Timeseries data to be unioned must have the same id namespace on every record.
* The union process of unifying disparate datasets requires a common primary person/entity key across the datasets. 
* Secondary keys based unions are not supported at this time.
* The field based identity stitching process allows for re-keying identities in rows based on subsequent  transient id records, such as an authentication id. This allows for resolving disparate records to a single id for analysis at the person level vs. at the device or cookie level.
* Stitching happens once a week. With replay after the stitch.



## FAQs & Reference Documentation

What are the downstream impacts of data models in CJA?

* Objects and attributes of the same XDM field will merge into one dimension in CJA. To  merge multiple attributes from various datasets into the same CJA dimension, the datasets should reference the same XDM field or schema.


1. [Customer Journey Analytics Product Description](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)

2. [Customer Journey Analytics Product Documentation](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=en)

