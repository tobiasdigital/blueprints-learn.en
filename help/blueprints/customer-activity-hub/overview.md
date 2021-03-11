---
title: Customer Activity Hub Blueprint
description: Real-time Customer Profile lookups to provide context for agent-assisted support and sales.
solution: Experience Platform, Data Collection
kt: 7195
thumbnail: 
---

# Customer Activity Hub Blueprint

Customer Activity Hub Blueprint shows how external applications can access Adobe Experience Platform’s Real-time Customer Profile. 

External application can access Real-time Customer Profiles with an API GET request. Attributes, events, segment memberships, and model-driven features stored in the profile can then be used in these external, non-Adobe applications.

With this capability, you could surface rich context when a customer calls your call center. Support agents could have visibility into the customer's lifetime value, propensity to churn or exposure to marketing campaigns, for example. Sales agents could also benefit from more context or insight into the customer they are selling.

>[!NOTE]
>
>The current latency supported by the profile lookup API is ~ 500 ms, making this approach not suitable for integration of the profile with real-time decision engines such as for same page web or mobile personalization. 

## Use Cases

* Provide deeper consumer context to agent supported interactions such as support and sales experiences. Via the profile lookup into Experience Platform agents can be provided with additional context on the consumer such as recent purchases, campaign interactions, propensities, audience memberships, and other attributes and insights that are stored in the real-time customer profile.

## Architecture

<img src="assets/cah.svg" alt="Reference Architecture for the Customer Activity Hub Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

* [Guardrails for Real-time Customer Profile data](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementation Steps

1. Configure datasets and schemas
1. Configure Real-time Customer Profiles – schema and dataset configured for Real-time Customer Profile, merge policy and identities configured
1. Ingest data into Platform and process to Real-time Customer Profile
1. Use Entity API to look up profile attribute – either from the record entity or the experience event entity

## Related Documentation

* [Adobe Experience Platform Activation product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [Real-time Customer Profile documentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Profile Lookup API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
