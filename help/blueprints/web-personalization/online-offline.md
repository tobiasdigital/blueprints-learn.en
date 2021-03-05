---
title: Online/Offline Web Personalization Scenario
description: Synchronize web personalization with email and other known and anonymous channel personalization.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
---

# Online/Offline Web Personalization scenario

Synchronize web personalization with email and other known and anonymous channel personalization.

## Use Cases

* Landing page optimization
* Behavioral and offline profile targeting
* Personalization based on prior product/content views, product/content affinity, environmental attributes, third-party audience data, and demographics in addition to offline insights such as transactions, loyalty and CRM data, and modeled insights

## Applications

* Adobe Real-time Customer Data Platform
* Adobe Target
* Adobe Audience Manager (Optional) - Audience Manager adds the following: third-party audience data, co-op based device graph, ability to surface Platform segments in Adobe Analytics and Adobe Analytics segments in Platform.
* Adobe Analytics (Optional) - Analytics adds the ability to build segments based on historical behavioral data and fine grained segmentation from Adobe Analytics data.


## Architecture

<img src="assets/onoff.svg" alt="Reference architecture for the Online/Offline Web Personalization scenario" style="border:1px solid #4a4a4a" />

## Guardrails

* By default the segment sharing service allows a maximum of 75 audiences to be shared for each Analytics report suite. If the customer has an Audience Manager license, there is no limit on the number of audiences that can be shared between Adobe Analytics and Target or Audience Manager and Target.
* Batch segment sharing – once per day or manually initiated via API.
* Shared segments available in Target for next hit/page personalization.

## Implementation Prerequisites

1. Visitor ID service or Web SDK must be implemented to have synced Experience Cloud IDs across applications. It is recommended to use Experience Platform Launch to deploy the ID service to ensure that the ID is set before any application calls.

1. For Analytics integration, all Analytics tracking must have been converted to Regional Data Collection.

1. Minimum code versions:

    * Experience Cloud ID service – VisitorAPI.js 2.0 or higher
    * Analytics – AppMeasurement.js 1.6.4 or higher
    * Audience Manager – dil.js 5.0 or higher
    * Target – mbox.js 61, at.js .9.1. at.js is preferred as mbox.js is no longer being developed.
    * Mobile SDK – 4.11 for iOS and Android
    * Experience Platform Web SDK – 1.0, current Experience Platform SDK version has [various use cases not yet supported for the Experience Cloud applications](https://github.com/adobe/alloy/projects/5)

## Implementation Steps

1.  Implement Adobe Target
1.  Implement Audience Manager and/or Analytics (optional)
1.  Implement Experience Platform and Real-time Customer Profile
1.  Implement Visitor ID Service or Experience Platform Web SDK
1.  Provision People and Audience services
1.  Provision Audience Sharing between Experience Platform and Target

## Implementation Data Flow Diagram

The Web/Mobile personalization blueprint can be implemented using either traditional application-specific SDKs (for example, AppMeasurement.js), or by using the Platform Web SDK/Mobile SDK and Edge Network.

### Platform Web/Mobile SDK and Edge Approach

<img src="assets/websdkflow.png" alt="Reference architecture for the Platform Web SDK/Mobile SDK and Edge Network Approach" style="border:1px solid #4a4a4a" />


### Application-specific SDK Approach

<img src="assets/appsdkflow.png" alt="Reference architecture for the Application-specific SDK Approach" style="border:1px solid #4a4a4a" />

## Related Documentation

* [Experience Platform segment sharing with Audience Manager and other Experience Cloud solutions](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
* [Experience Platform Segmentation Overview](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Streaming Segmentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Experience Platform Segment Builder Overview](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html)
* [Audience Manager Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html)
* [Analytics Segment Sharing through AAM](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Cloud ID Service documentation](https://experienceleague.adobe.com/docs/id-service/using/home.html)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch/using/home.html)

## Related Blog Posts

* [Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [Build an Optimal Online Experience: Enrich Unified Profile with Query Service](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [Integrating Adobe Experience Platform Decisioning Engine with AEM Websites](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [How Adobe Experience Platform Predictive Audiences improves Personalized Experiences](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [Adobe Experience Platform Web SDK for Audience Management](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [Build an Optimal Online Experience: Enrich Unified Profile with Query Service](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)


