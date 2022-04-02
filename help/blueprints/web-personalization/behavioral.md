---
title: Behavioral Web Personalization Blueprint
description: Personalize based on online behavior and audience data.
landing-page-description: Learn to personalize based on online behavior and audience data.
solution: Experience Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7085thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
---
# Behavioral Web/Mobile Personalization Blueprint

Personalize based on online behavior and audience data.

## Use Cases

* Landing page optimization
* Behavioral targeting
* Personalization based on prior product/content views, product/content affinity, environmental attributes, third-party audience data, and demographics

## Applications

* Adobe Target
* Adobe Analytics (optional)
* Adobe Audience Manager (optional)
* Adobe Real-time Customer Data Platform (optional)

## Architecture

<img src="assets/behavioral_personalization.svg" alt="Reference architecture for the Behavioral Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />


## Implementation Patterns

The Web/Mobile personalization blueprint can be implemented via the following approaches as outlined below.

1. Using the [!UICONTROL Platform Web SDK] or [!UICONTROL Platform Mobile SDK] and [!UICONTROL Edge Network]. [Refer to the Experience Platform Web and Mobile SDK Blueprint](../data-ingestion/websdk.md)
1. Using traditional application-specific SDKs (for example, AppMeasurement.js). [Refer to the application specific SDK Blueprint](../data-ingestion/appsdk.md)

## Implementation Steps

1. [Implement Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) for your web or mobile applications.

### Implementation Steps - Audience Manager or Adobe Analytics

1. [Implement Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)
1. [Implement Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
1. [Implement Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html) 

    >[!NOTE]
    >
    >Each application must use the Experience Cloud ID and be part of the same Experience Cloud Org to allow audience sharing between applications.

1. [Request provisioning for the People and Audience Sharing services (Shared Audiences)](https://www.adobe.com/go/audiences)
1. Build segments in [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) or [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html) and [configure those audiences for sharing to the Experience Cloud](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)  (if using Audience Manager or Adobe Analytics)
1. Once the audiences are available in Adobe Target, they can be used for [targeting experiences with Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)

### Implementation Steps - Real-time Customer Data Platform

1. [Create schemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) for data to be ingested.
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) for data to be ingested.
1. [Configure the correct identities and identity namespaces](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) on the schema to be sure that ingested data can stitch into a unified profile.
1. [Enable the schemas and datasets for profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html). 
1. [Ingest data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) into Experience Platform.
1. [Provision [!UICONTROL Real-time Customer Data Platform] segment sharing](https://www.adobe.com/go/audiences) between Experience Platform and Audience Manager for audiences defined in Experience Platform to be shared to Audience Manager.
1. [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) in Experience Platform. The system automatically determines whether the segment is evaluated as batch or streaming.
1. [Configure destinations](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html) for sharing of profile attributes and audience memberships to desired destinations.


## Related Documentation

* [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrate Audience Manager with Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Analytics Segment Sharing through Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [[!UICONTROL Real-time Customer Data Platform] overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [[!UICONTROL Real-time Customer Data Platform] Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and segmentation guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Blog Posts

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
