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
* Adobe Audience Manager (optional): Adds third-party audience data, co-op based device graph, the ability to surface Real-time Customer Data Platform audiences in Adobe Analytics, and the ability to surface Adobe Analytics audiences in Real-time Customer Data Platform
* Adobe Analytics (optional): Adds the ability to build segments based on historical behavioral data and fine grained segmentation from Adobe Analytics data

## Use Case Scenarios

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
    <th class="tg-f7v4">Use Case Scenarios</th>
    <th class="tg-y6fn">Capability</th>
    <th class="tg-f7v4">Pre-Requisites</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
<td class="tg-73oq">Real-time segment evaluation on the Edge shared from Real-time Customer Data Platform to Target</td>
    <td class="tg-0lax">- Evaluate audiences in real-time for same or next page personalization on the Edge.<br>- In addition, any segments evaluated in streaming or batch fashion will also be projected to the Edge Network to be included in edge segment evaluation and personalization.</td>
    <td class="tg-73oq">- Implementation Pattern 1 described below.<br>- Web/Mobile SDK must be implemented.<br>- Note that the Mobile SDK and API based support for real-time segmentation is not currently available<br>- Datastream must be configured in Experience Edge with the Target and Experience Platform extension enabled, the Datastream ID will be provided in the Target destination configuration.<br>- Target destination must be configured in Real-time Customer Data Platform Destinations.<br>- Integration with Target requires the same IMS Org as the Experience Platform instance.</td> 
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Streaming and batch audience sharing from Real-time Customer Data Platform to Target via the Edge approach</td>
    <td class="tg-0lax">- Share streaming and batch audiences from Real-time Customer Data Platform to Target through the Edge Network. Audiences evaluated in real-time require the WebSDK and real-time audience evaluation outlined in integration pattern 1.<br>- This integration is typically leveraged to share streaming and batch audiences using traditional SDKs instead of migrating to the Edge Collection and WebSDK which powers real-time as well as streaming and batch audiences as outlined in integration patter 1.</td>
    <td class="tg-73oq">- Implementation Pattern 1 or 2 described below.<br>- Web/Mobile SDK is not required for sharing of streaming and batch audiences to Target though it is required to enable real-time edge segment evaluation as outlined in integration pattern 1. <br>- If using AT.js, only profile integration against the ECID identity namespace is supported. <br>- For custom identity namespace lookups on the Edge, the WebSDK deployment is required and each identity must be set as an identity in the identity map.<br>- Datastream must be configured in Experience Edge, the Datastream ID will be provided in the Target destination configuration.<br>- Target destination must be configured in Real-time Customer Data Platform Destinations.<br>- Integration with Target requires the same IMS Org as the Experience Platform instance.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Streaming and batch audience sharing from Real-time Customer Data Platform to Target and Audience Manager via the Audience Sharing Service Approach</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">- Share streaming and batch audiences from Real-time Customer Data Platform to Target and Audience Manager via the Audience Sharing service.<br> -This integration pattern can be leveraged when additional enrichment from 3rd party data and audiences in Audience Manager is desired. Otherwise integration pattern 1 and 2 are preferred. Audiences evaluated in real-time require the WebSDK and real-time audience evaluation outlined in integration pattern 1.</span></td>
    <td class="tg-73oq">- Implementation Pattern 1 or 2 described below.<br>- Web/Mobile SDK deployment is not required for this integration.<br>- Audience projection via audience sharing service must be provisioned.<br>- Integration with Target requires the same IMS Org as the Experience Platform instance.<br>- Identity must be resolved to ECID to share to the edge for Target to action upon.</td>
  </tr>
</tbody>
</table>

## Scenario 1 and 2 - Real-time, Streaming, and Batch Audience Sharing to Adobe Target

Architecture

<img src="assets/RTCDP+Target.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

Sequence Detail

<img src="assets/RTCDP+Target_flow.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

Overview Architecture for Use Case Scenario 1 and 2

<img src="assets/personalization_with_apps.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a"/>

### Implementation Steps for Use Case Scenario 1, also supports Use Case Scenario 2

1. [Implement Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) for your web or mobile applications
1. [Implement Experience Platform and [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. Implement [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html). Experience Platform Web SDK is required for real-time Edge segmentation, but not required for sharing of streaming and batch audiences from Real-time Customer Data Platform to Target. Note that support for real-time segmentation via the Mobile SDK and API is not currently available.
1. [Configure the Edge Network with a Edge Datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
1. [Enable Adobe Target as a destination within Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)

<br>

## Scenario 3 - Streaming and Batch Audience Sharing through the Audience Sharing Service to Adobe Target and Audience Manager

Architecture

<img src="assets/audience_share_architecture.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

### Implementation Steps for Scenario 3, also supports scenario 2

1. [Implement Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) for your web or mobile applications
1. [Implement Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html) (optional)
1. [Implement Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)  (optional)
1. [Implement Experience Platform and [!UICONTROL Real-time Customer Profile]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. Implement [Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html)
1. [Request provisioning for Audience Sharing between Experience Platform and Adobe Target (Shared Audiences)](https://www.adobe.com/go/audiences) to share audiences from Experience Platform to Target.
1. (Optional) [Configure the Edge Network with a Edge Datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) (This is only required for integration pattern 2, where the audiences do not need to be shared to Audience Manager or enriched by Audience Manager audiences or data).
1. (Optional) [Enable Adobe Target as a destination within Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) to share streaming and batch audiences from Real-time Customer Data Platform directly to the Edge vs. through the audience sharing service and Audience Manager.

<br>

## Implementation Patterns

Online and Offline Personalization is supported via several implementation approaches.

### Implementation Pattern 1 - Supports Use Case Scenario 1 and 2. Edge Network with Web/Mobile SDK (Recommended Approach)

Using the Edge Network with the Web/Mobile SDK
<img src="assets/web_sdk_flow.png" alt="Reference architecture for the Application-specific SDK Approach" style="width:80%; border:1px solid #4a4a4a" />

Sequence Diagram

<img src="assets/RTCDP+Target_sequence.png" alt="Reference architecture for the Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Implementation Pattern 2 - Supports Use Case Scenario 2 and 3. Application specific SDKs

Using traditional application-specific SDKs (for example, AT.js and AppMeasurement.js)
<img src="assets/app_sdk_flow.png" alt="Reference architecture for the Application-specific SDK Approach" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Guardrails

[Refer to the guardrails on the Web and Mobile Personalization Blueprints Overview page.](overview.md)

## Implementation Considerations

Identity pre-requisites

* Any primary identity can be leveraged when utilizing implementation pattern 1 outlined above with the Edge network and WebSDK. First login personalization requires the personalization request set primary identity match the primary identity of the profile from Real-time Customer Data Platform. Identity stitching between anonymous devices and known customers is processed on the hub and subsequently projected to the edge.
* Sharing audiences from Adobe Experience Platform to Adobe Target requires the use of ECID as a identity when using the audience sharing service as outlined in use case scenario 3 above.
* Alternate identities can be used to share Experience Platform audiences to Adobe Target via Audience Manager as well. Experience Platform activates audiences to Audience Manager via the following supported namespaces: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Note that Audience Manager and Target resolve audience memberships via the ECID identity, so ECID is still required for the final audience sharing to Adobe Target.  

## Related Documentation

### SDK Documentation

* [Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Platform Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Experience Cloud ID Service documentation](https://experienceleague.adobe.com/docs/id-service/using/home.html)

### Connection Documentation

* [Adobe Target Connection for Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Edge Datastream Configuration](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
* [Experience Platform segment sharing with Audience Manager and other Experience Cloud solutions](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)

### Segmentation Documentation

* [Experience Platform Segmentation Overview](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Real-time Segmentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html)
* [Streaming Segmentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Adobe Analytics Segment Sharing through Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)

### Tutorials

* [Next-hit personalization with Real-time CDP and Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=en)

### Related Blog Posts

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
