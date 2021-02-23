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

![Scenario 1](assets/personalization.svg)

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
| Experience Platform Web SDK | 1.0, current Experience Platform SDK version has a number of use cases not yet supported for the Experience Cloud applications as noted in the [Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)| |

## Guardrails

Availability: Global

Audience Sharing: By default the segment sharing service allows a maximum of 75 audiences to be shared for each Analytics report suite. If AAM is being used for audience sharing there is no limit on the number of audiences that can be shared. 

## Implementation Steps

* Implement Adobe Target
* Implement AAM or Analytics
* Implement Visitor ID service
* Provision People and Audience Sharing services

## Data Flow Implementation Diagram

The Web/Mobile personalization blueprint can be implemented using either traditional app specific SDKs, or by using the WebSDK and Experience Edge Network.

* WebSDK/MobileSDK and Experience Edge Approach

![Scenario 1](assets/websdkflow.png)




* Application Specific SDK Approach

![Scenario 1](assets/appsdkflow.png)



## FAQ & Reference Documentation

1. [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
2. [Integrate Audience Manager with Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
3. [Analytics Segment Sharing through AAM](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)


