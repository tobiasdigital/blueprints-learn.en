---
title: Web/Mobile Personalization with online & offline data
description: Synchronize web personalization with email and other known and anonymous channel personalization.
landing-page-description: Synchronize web personalization with email and other known and anonymous channel personalization.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
---
# Web/Mobile Personalization with online & offline data

Synchronize web personalization with email and other known and anonymous channel personalization.

## Use Cases

* Landing page optimization
* Behavioral and offline profile targeting
* Personalization based on prior product/content views, product/content affinity, environmental attributes, third-party audience data, and demographics in addition to offline insights such as transactions, loyalty and CRM data, and modeled insights
* Share and target audiences defined in Real-time Customer Data Platform on websites and mobile apps using Adobe Target.

## Applications

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (optional): Adds third-party audience data, co-op based device graph, the ability to surface Platform segments in Adobe Analytics, and the ability to surface Adobe Analytics segments in Platform
* Adobe Analytics (optional): Adds the ability to build segments based on historical behavioral data and fine grained segmentation from Adobe Analytics data

## Integraion Patterns

<table class="tg" style="undefined;table-layout: fixed; width: 790px">
<colgroup>
<col style="width: 20px">
<col style="width: 276px">
<col style="width: 229px">
<col style="width: 265px">
</colgroup>
<thead>
  <tr>
    <th class="tg-y6fn">#</th>
    <th class="tg-f7v4">Integration Pattern</th>
    <th class="tg-y6fn">Capability</th>
    <th class="tg-f7v4">Pre-Requisites</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">RTCDP streaming and batch audience sharing to Target and Audience Manager via the Audience Sharing Service Approach</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">- Share streaming and batch audiences from RTCDP to Target and Audience Manager via the Audience Sharing service. Audiences evaluated in real-time require the WebSDK and real-time audience evaluation outlined in integration pattern 3.</span></td>
    <td class="tg-73oq">- Audience projection via audience sharing service must be provisioned.<br>- Integration with Target requires the same IMS Org as the Experience Platform instance.<br>- Identity must be resolved to ECID to share to the edge for Target to action upon. AAM has a separate list of approved identities to match against<br>- WebSDK deployment is not required for this integration.</td>
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">RTCDP streaming and batch audience sharing to Target via the Edge approach</td>
    <td class="tg-0lax">- Share streaming and batch audiences from RTCDP to Target via the Edge Network. Audiences evaluated in real-time require the WebSDK and real-time audience evaluation outlined in integration pattern 3.</td>
    <td class="tg-73oq"><span style="text-decoration:none">- Currently in beta</span><br>- Target destination must be configured in RTCDP Destinations.<br>- Integration with Target requires the same IMS Org as the Experience Platform instance.<br>WebSDK is not required. WebSDk and AT.js are supported. <br>- If using AT.js only profile lookup against the ECID is supported. <br>- For custom id namespace lookups on the Edge, the WebSDK deployment is required and each identity must be set as an identity in the identity map.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq">RTCDP real-time segment evaluation on the Edge shared to Target via the Edge Network using the WebSDK.</td>
    <td class="tg-0lax">- Evaluate audiences in real-time for same or next page personalization on the Edge.</td>
    <td class="tg-73oq"><span style="text-decoration:none">- Currently in beta</span><br>- Target destination must be configured in RTCDP Destinations.<br>- Integration with Target requires the same IMS Org as the Experience Platform instance.<br>- WebSDK must be implemented.<br>- Also supported via API.</td>
  </tr>
</tbody>
</table>


## Architecture

Overview Architecture

<img src="assets/RTCDP+Target.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

Process Flow Architecture

<img src="assets/RTCDP+Target_flow.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

Detailed Architecture

<img src="assets/personalization_with_apps.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a"/>

## Guardrails

[Refer to the guardrails on the Web and Mobile Personalization Blueprints Overview page.](overview.md)

## Implementation Patterns

The Web/Mobile personalization blueprint can be implemented via the following approaches as outlined below.

1. Using the [!UICONTROL Platform Web SDK] or [!UICONTROL Platform Mobile SDK] and [!UICONTROL Edge Network].
1. Using traditional application-specific SDKs (for example, AppMeasurement.js)

### 1. Platform Web/Mobile SDK and Edge Approach

[Refer to the Experience Platform Web and Mobile SDK Blueprint](../data-ingestion/websdk.md) 

### 2. Application-specific SDK Approach

<img src="assets/app_sdk_flow.png" alt="Reference architecture for the Application-specific SDK Approach" style="width:80%; border:1px solid #4a4a4a" />

## Implementation Prerequisites

Identity pre-requisites

* Sharing audiences from Adobe Experience Platform to Adobe Target requires the use of ECID as a identity.
* Alternate identities can be used to share Experience Platform audiences to Adobe Target via Audience Manager as well. Experience Platform activates audiences to Audience Manager via the following supported namespaces: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Note that Audience Manager and Target resolve audience memberships via the ECID identity, so ECID is still required for the final audience sharing to Adobe Target. 

| Application/Service | Required Library |  Notes | 
|---|---|---|
| Adobe Target | [!UICONTROL Platform Web SDK]*, at.js 0.9.1+, or mbox.js 61+ | at.js is preferred as mbox.js is no longer being developed. |
| Adobe Audience Manager (Optional) | [!UICONTROL Platform Web SDK]* or dil.js 5.0+ |  |
| Adobe Analytics (Optional) | [!UICONTROL Platform Web SDK]* or AppMeasurement.js 1.6.4+ | Adobe Analytics tracking must use Regional Data Collection (RDC). |
| Experience Cloud ID service | [!UICONTROL Platform Web SDK]* or VisitorAPI.js 2.0+ | (Recommended) Use Experience Platform Launch to deploy the ID service to ensure that the ID is set before any application calls |
| Experience Platform Mobile SDK (Optional) | 4.11 or higher for iOS and Android™ |  |
| Experience Platform Web SDK | 1.0, current Experience Platform SDK version has [various use cases not yet supported for the Experience Cloud applications](https://github.com/adobe/alloy/projects/5)| |




## Implementation Steps


1. [Implement Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) for your web or mobile applications
1. [Implement Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html) (optional)
1. [Implement Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)  (optional)
1. [Implement Experience Platform and [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. Implement [Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html) or [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
1. [Enable Adobe Target as a destination within Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) or for the audience sharing approach [Request provisioning for Audience Sharing between Experience Platform and Adobe Target (Shared Audiences)](https://www.adobe.com/go/audiences) to share audiences from Experience Platform to Target.
    >[!NOTE]
    >
    >When using the Audience Sharing service between RTCDP and Adobe Target, audiences must be shared using the Experience Cloud ID and be part of the same Experience Cloud Org. Support for identities other than ECID requires the use of the WebSDK and Experience Edge Network.


## Related Documentation

* [Experience Platform segment sharing with Audience Manager and other Experience Cloud solutions](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
* [Experience Platform Segmentation Overview](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Streaming Segmentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Adobe Target Connection for Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Experience Platform Segment Builder Overview](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html)
* [Audience Manager Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html)
* [Adobe Analytics Segment Sharing through Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Cloud ID Service documentation](https://experienceleague.adobe.com/docs/id-service/using/home.html)
* [Experience Platform Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)

## Related Blog Posts

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
