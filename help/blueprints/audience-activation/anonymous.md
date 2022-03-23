---
title: Anonymous Audience Activation Blueprint
description: Learn to target audiences across web and advertising channels based on anonymous and behavioral customer data. This ability enables personalized and consistent real-time customer experiences across devices.
landing-page-description: Learn to target audiences across web and advertising channels based on anonymous and behavioral customer data.
solution: Experience Platform, Audience Manager
kt: 7211
thumbnail:
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
---
# Anonymous Audience Activation Blueprint

Anonymou audience activation is the ability to target and personalize to audiences across web, mobile, and advertising channels based on anonymous device and behavioral data. 

## Use Cases

* Perform anonymous digital audience targeting and personalization on the website, mobile app, or on supported advertising channels.
* Optimize landing page and pre-authentication experiences based on known device and behavioral characteristics.
* Leverage the Audience Manager third party data network to further refine and expand your audiences for targeting.


## Applications

* Audience Manager
* Real-time Customer Data Platform

Both Audience Manager and Real-time Customer Data Platform can be leveraged to power Anonymous Audience Activation for onsite and advertising destinations. Note that Real-time Customer Data Platform supports only a subset of advertising destinations with anonymous device identifiers as cataloged in the [destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en).

Microsoft Bing, Google DV360, and TradeDesk are the primary supported Real-time Customer Data Platform advertising destinations for anonymous device based targeting. Beyond these, Real-time Customer Data Platform supports numerous known customer based destinations as cataloged in the [destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en) and as described in the [known customer activation blueprint](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Architecture

<img src="assets/anonymous_activation.svg" alt="Reference architecture for the Anonymous Audience Activation Blueprint" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Implementation Steps

1. [Implement Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=en#implementation-integration-guides).
1. Collect data to Audience Manager.
1. Configure signals and traits for use in segment definitions.
1. Create segments in Audience Manager.
1. Configure destinations in Audience Manager to share audiences.

For implementation steps of Real-time Customer Data Platform please refer to the [known customer activation blueprint](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Related Documentation

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=en)
* [Experience Cloud [!UICONTROL Audiences]](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrate Audience Manager with Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Analytics Segment Sharing through Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Known Customer Activation Blueprint](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).
* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html)
