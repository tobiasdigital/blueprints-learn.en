---
title: Call Deflection Analysis scenario
description: Analyze customer behavior before they contact the call center.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
---

# Call Deflection Journey Analysis scenario

Analyze a customer's behavior across desktop and mobile before they contact the call center. Identify opportunities to improve the customer journey by understanding what actions your customers were trying to complete,  what content they viewed, and what terms they searched before they contact customer support. What content and self-service tools can be improved to help your customers resolve issues without needing to call in?

## Use Cases

* Analyze customer behavior before customers contact support 
* Discover opportunities to improve self-service capabilities

## Applications

* Adobe Experience Platform
* Customer Journey Analytics

## Integration Patterns

* Adobe Experience Platform → Customer Journey Analytics

## Architecture

<img src="assets/CJA.svg" alt="Reference architecture for the Customer Journey Analytics Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

Data Ingestion into Customer Journey Analytics:

* Data ingestion to lake: API ~ 7 GB/hr, source connector ~ 200 GB/hr, streaming to lake ~ 15 min, Analytics source connector to lake ~ 45 min.
* Once data has been published to the data lake, it can take up to 90 mins to process into Customer Journey Analytics.

## Implementation Steps

1. Configure datasets and schemas
1. Ingest data into Platform.
1. Data must be ingested into Platform before ingestion into Customer Journey Analytics. 
1.  Cross channel event datasets to be analyzed in union must have a common namespace id or be rekeyed through the field based stitching capability of Customer Journey Analytics.    
 
    >[!NOTE]
    >
    > Customer Journey Analytics does not utilize the Experience Platform Profile or Identity services for stitching today.

1. Any custom data preparation or use of the field-based identity stitching is performed on the data to insure a common key across time series datasets to be ingested into Customer Journey Analytics.
1. Lookup data must have a primary ID that can join to a field in the event data. Counts as rows in licensing. 
1. Profile data must have the same primary ID as the primary ID of the event data.
1. A data connection is configured to ingest data from Experience Platform to Customer Journey Analytics. Once data lands in the data lake, it processes into Customer Journey Analytics within 90 minutes.
1. A data view is configured on the connection to select the specific dimensions and metrics to be included in the view. Attribution and allocation settings are also configured in the data view. These settings are computed at report time.
1. A project is then created to configure dashboards and reports within Analysis Workspace.

## Implementation Considerations

### Identity Stitching Considerations

* Time-series data to be unioned must have the same id namespace on every record. To connect call center data to anonymous device data, the digital ID must be tied to the calling ID. This tying can occur through several possible mechanisms:
    1. The dial number being a unique dial number for that visitor for that time, along with a lookup table to track the relationship. 
    1. Require the user to authenticate before requesting support and tie this authentication to an identifier determined by the call agent - phone number or email as example.
    1. Use an onboarding partner to help type online device identifiers with known identifiers tied to the support request.
* The union process of unifying disparate datasets requires a common primary person/entity key across the datasets. 
* Secondary key-based unions are not supported currently.
* The field-based identity stitching process allows for rekeying identities in rows based on subsequent transient id records, such as an authentication id. This allows for resolving disparate records to a single id for analysis at the person level vs. at the device or cookie level.
* Stitching happens once a week. With replay after the stitch.

## FAQs

* What are the downstream impacts of data models in Customer Journey Analytics?

    Objects and attributes of the same XDM field merge into one dimension in Customer Journey Analytics. To merge multiple attributes from various datasets into the same CJA dimension, the datasets should reference the same XDM field or schema.

## Related Documentation

* [Customer Journey Analytics Product Description](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics documentation](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Customer Journey Analytics tutorials](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
