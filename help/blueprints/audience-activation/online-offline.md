---
title: Behavioral Web Personalization Scenario
description: Personalize based on online behavior and audience data.
solution: Experience Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 
thumbnail: thumb-web-personalization-scenario1.jpg
---

# Behavioral Web Personalization scenario

Personalize based on online behavior and audience data.

## Use Cases

* Landing page optimization
* Behavioral Targeting
* Personalization based on prior product/content views, product/content affinity, environmental attributes, 3rd party audience data and demographics

## Reference Architecture

![Scenario 1](assets/web-personalization-scenario1.png)

## Prerequisites

| Application/Service | Required Library |  Notes | 
|---|---|---|
| Adobe Target | Platform Web SDK*, at.js 0.9.1+ or mbox.js 61+ | at.js is preferred as mbox.js is no longer being developed. |
| Adobe Audience Manager (Optional) | Platform Web SDK* or dil.js 5.0+ |  |
| Adobe Analytics (Optional) | Platform Web SDK* or AppMeasurement.js 1.6.4+ |  |
| Experience Cloud ID service | Platform Web SDK* or VisitorAPI.js 2.0+ |  |
| Experience Cloud Audiences (Optional) | n/a |  |
| Launch Edge Configuration <br> (if using Experience Platform Web SDK) | n/a |  |
| Mobile SDK (Optional) | 4.11 or higher for iOS and Android |  |

* Experience Platform Web SDK – 1.0, current Experience Platform SDK version has a number of use cases not yet supported for the Experience Cloud applications as noted in the [Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
  
<!--
1. Provisioning
   1. Adobe Target
   1. Adobe Audience Manager (Optional)
   1. Adobe Analytics (Optional)
   1. Experience Cloud Shared Audiences (Optional)
   1. Launch Edge Configuration if using Experience Platform Web SDK

1. Visitor ID service must be implemented to have synced Experience Cloud IDs across applications. It is strongly recommended to leverage Experience Platform Launch to deploy the ID service to ensure the ID is set prior to any application calls.
1. For Analytics integration, all Analytics tracking must have been converted to Regional Data Collection. RDC.
1. Minimum code versions are as follows
   1. Experience Cloud ID service – VisitorAPI.js 2.0 or higher
   1. Analytics – AppMeasurement.js 1.6.4 or higher
   1. Audience Manager – dil.js 5.0 or higher
   1. Target – mbox.js 61, at.js .9.1. at.js is preferred as mbox.js is no longer being developed.
   1. Mobile SDK – 4.11 for iOS and Android
   1. Experience Platform Web SDK – 1.0, current Experience Platform SDK version has a number of use cases not yet supported for the Experience Cloud applications as noted in the [Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
-->

## Guardrails

By default the audience sharing service allows a maximum of 75 audiences to be shared for each Analytics report suite. If the customer has an AAM license, there is no limit on the number of audiences that can be shared between AA and Target or AAM and Target.

## Data Flow & Latencies

See Implementation Architecture diagram

Two versions: 

1. With legacy client code libraries.
1. With Web SDK and Launch

## Implementation Steps

* Implement Adobe Target
* Implement AAM or Analytics
* Implement Visitor ID service
* Provision People and Audience services

## FAQ & Reference Documentation

1. [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
1. [Integrate Audience Manager with Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
1. [Analytics Segment Sharing through AAM](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)















