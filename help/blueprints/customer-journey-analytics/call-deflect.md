---
title: Call Deflection Analysis Blueprint
description: Analyze customer behavior before they contact the call center.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
exl-id: 13593c1c-4c58-4b8a-aa6c-7530fd679a14
---
# Call Deflection Journey Analysis Blueprint

Analyze a customer's behavior across desktop and mobile before they contact the call center. Identify opportunities to improve the customer journey by understanding what actions your customers try to complete, what content they view, and what terms they search before they contact customer support. Determine the content and self-service tools that can be improved to help your customers resolve issues without needing to call in.

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

## Implementation Steps

1. [Create schemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) for data to be ingested.
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) for data to be ingested.
1. [Ingest data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) into Experience Platform.
    Data must be ingested into Platform before ingestion into Customer Journey Analytics. 
1.  Analyze cross-channel event datasets. 
    Datasets analyzed in union must have a common namespace ID or be rekeyed through the field based stitching capability of Customer Journey Analytics.    
 
    >[!NOTE]
    >
    >Customer Journey Analytics does not currently use the Experience Platform Profile or Identity services for stitching.

1. Perform any custom data preparation or use of the field-based identity stitching on the data, to ensure a common key across time series datasets to be ingested into Customer Journey Analytics.
1. Provide a primary ID for lookup data, which can join to a field in the event data. Counts as rows in licensing. 
1. Set the same primary ID on profile data as the primary ID of the event data.
1. Configure a data connection to ingest data from Experience Platform to Customer Journey Analytics. After data lands in the data lake, it processes into Customer Journey Analytics within 90 minutes.
1. Configure a data view on the connection to select the specific dimensions and metrics to be included in the view. Attribution and allocation settings are also configured in the data view. These settings are computed at report time.
1. Create a project to configure dashboards and reports within Analysis Workspace.

## Implementation Considerations

### Identity Stitching Considerations

* Time-series data to be unioned must have the same id namespace on every record. To connect call center data to anonymous device data, the digital ID must be tied to the calling ID. This tying can occur through several possible mechanisms:
    * The dial number being a unique dial number for that visitor for that time, along with a lookup table to track the relationship. 
    * Require the user to authenticate before requesting support and tie this authentication to an identifier determined by the call agent (for example, phone number or email).
    * Use an onboarding partner to help type online device identifiers with known identifiers tied to the support request.
* The union process of unifying disparate datasets requires a common primary person/entity key across the datasets. 
* Secondary key-based unions are not supported currently.
* The field-based identity stitching process allows for rekeying identities in rows based on subsequent transient ID records, such as an authentication ID. This process allows for resolving disparate records to a single ID for analysis at the person level rather than at the device or cookie level.
* Stitching happens once a week, with replay after the stitch.

## FAQs

* What are the downstream impacts of data models in Customer Journey Analytics?

    Objects and attributes of the same XDM field merge into one dimension in Customer Journey Analytics. To merge multiple attributes from various datasets into the same CJA dimension, the datasets should reference the same XDM field or schema.

## Related Documentation

* [Customer Journey Analytics Product Description](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics documentation](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Customer Journey Analytics tutorials](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
