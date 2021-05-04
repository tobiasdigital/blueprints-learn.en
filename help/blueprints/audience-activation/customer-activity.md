---
title: Customer Activity Hub Blueprint
description: [!UICONTROL Real-time Customer Profile] lookups to provide context for agent-assisted support and sales.
solution: Experience Platform,Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c,4f15aa5d-9ee3-4d92-8012-3e2f0c0d615f
---
# Customer Activity Hub Blueprint

Customer Activity Hub Blueprint shows how external applications can access Adobe Experience Platform’s [!UICONTROL Real-time Customer Profile].

External applications can access profiles with an API GET request. Attributes, events, segment memberships, and model-driven features stored in the profile can then be used in these external, non-Adobe applications.

With this capability, you could surface rich context when a customer calls your call center. Support agents could have visibility into the customer's lifetime value, propensity to churn or exposure to marketing campaigns, for example. Sales agents can also benefit from more context or insight into their customer.

>[!NOTE]
>
>The current latency supported by the profile lookup API is approximately 500 milliseconds, making this approach unsuitable for integration of the profile with real-time decision engines such as same-page web or mobile personalization. 

## Use Cases

* Provide deeper consumer context to agent-supported interactions, such as support and sales experiences. Using the profile lookup into Experience Platform, agents can receive more context on the consumer, such as recent purchases, campaign interactions, propensities, audience memberships, and other attributes and insights that are stored in the real-time customer profile.

## Architecture

<img src="assets/customer_activity_hub.svg" alt="Reference Architecture for the Customer Activity Hub Blueprint" style="border:1px solid #4a4a4a" />


## Guardrails

* [Guardrails for [!UICONTROL Real-time Customer Profile] data](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementation Steps

1. Configure datasets and schemas.
1. Configure [!UICONTROL Real-time Customer Profile]: configure the schema and dataset for [!UICONTROL Real-time Customer Profile], and set up a merge policy and identities.
1. Ingest data into Platform and process it to [!UICONTROL Real-time Customer Profile].
1. Use the Entity API to look up a profile attribute, either from the record entity or the experience event entity.

## Related Documentation

* [Adobe Experience Platform Activation product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL Real-time Customer Profile] documentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Profile Lookup API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
