---
title: Behavioral Web Personalization Blueprint
description: Personalize based on online behavior and audience data.
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

## Architecture

<img src="assets/behavioral_personalization.svg" alt="Reference architecture for the Behavioral Web Personalization Blueprint" style="border:1px solid #4a4a4a" />


## Guardrails

By default, the segment sharing service allows a maximum of 75 audiences to be shared for each Adobe Analytics report suite. If Audience Manager is being used for audience sharing, there is no limit on the number of audiences that can be shared. 

## Implementation Patterns

The Web/Mobile personalization blueprint can be implemented via the following approaches as outlined below.

1. Using the [!UICONTROL Platform Web SDK] or [!UICONTROL Platform Mobile SDK] and [!UICONTROL Edge Network].
1. Using traditional application-specific SDKs (for example, AppMeasurement.js)

### 1. Platform Web/Mobile SDK and Edge Approach

<img src="assets/websdkflow.svg" alt="Reference architecture for the [!UICONTROL Platform Web SDK] or [!UICONTROL Platform Mobile SDK] and [!UICONTROL Edge Network] Approach" style="border:1px solid #4a4a4a" />

### 2. Application-specific SDK Approach

<img src="assets/appsdkflow.png" alt="Reference architecture for the Application-specific SDK Approach" style="border:1px solid #4a4a4a" />

## Implementation Prerequisites

| Application/Service | Required Library |  Notes | 
|---|---|---|
| Adobe Target | [!UICONTROL Platform Web SDK]*, at.js 0.9.1+, or mbox.js 61+ | at.js is preferred as mbox.js is no longer being developed. |
| Adobe Audience Manager (Optional) | [!UICONTROL Platform Web SDK]* or dil.js 5.0+ |  |
| Adobe Analytics (Optional) | [!UICONTROL Platform Web SDK]* or AppMeasurement.js 1.6.4+ |  |
| Experience Cloud Identity Service | [!UICONTROL Platform Web SDK]* or VisitorAPI.js 2.0+ |  |
| Experience Platform Mobile SDK (Optional) | 4.11 or higher for iOS and Android™ |  |
| Experience Platform Web SDK | 1.0, current Experience Platform SDK version has [various use cases not yet supported for the Experience Cloud applications](https://github.com/adobe/alloy/projects/5)| |

## Implementation Steps

1. [Implement Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) for your web or mobile applications.

    If using Audience Manager or Adobe Analytics:

1. [Implement Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)
1. [Implement Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
1. [Implement Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html) 

    >[!NOTE]
    >
    >Each application must use the Experience Cloud ID and be part of the same Experience Cloud Org to allow audience sharing between applications.

1. [Request provisioning for the People and Audience Sharing services (Shared Audiences)](https://www.adobe.com/go/audiences)
1. Build segments in [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) or [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html) and [configure those audiences for sharing to the Experience Cloud](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)  (if using Audience Manager or Adobe Analytics)
1. Once the audiences are available in Adobe Target, they can be used for [targeting experiences with Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)

## Related Documentation

* [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrate Audience Manager with Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Analytics Segment Sharing through Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)


## Related Blog Posts

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
