---
title: Profile Lookup Blueprint
description: Real-time Customer Profile lookups to provide context for agent-assisted support and sales.
solution: Experience Platform, Data Collection
kt: 7195
thumbnail: 
---

# Profile Lookup Blueprint

Profile Lookup Blueprint how external applications can access Adobe Experience Platform’s Real-time Customer Profile. 

External application can access Real-time Customer Profiles with an API GET request. Attributes, events, segment memberships, and model-driven features stored in the profile can then be used in these external, non-Adobe applications.

With this capability, you could surface rich context when a customer calls your call center. Support agents could have visibility into the customer's lifetime value, propensity to churn or exposure to marketing campaigns, for example. 

Sales agents could also benefit from more context or insight into the customer they are selling.

>[!NOTE]
>
>The current latency supported by the profile lookup API is ~ 500ms, making this approach not suitable for integration of the profile with real-time decision engines. For this capability the Edge Profile which has a latency <100ms must be utilized. Note that the Edge Profile capability is still in development.


## Architecture

<img src="assets/cah.svg" alt="Reference Architecture for the Profile Lookup Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

* [Guardrails for Real-time Customer Profile data](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementation Steps

1. Datasets and schemas configured
1. Real-time Customer Profile configured – schema and dataset configured for Real-time Customer Profile, merge policy and identities configured
1. Data collected into Platform and processed to Real-time Customer Profile
1. Entity API leveraged to lookup profile attribute – either from the record entity or the experience event entity

## Related Documentation

* [Adobe Experience Platform Activation product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [Real-time Customer Profile documentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Profile Lookup API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
