---
title: Profile Lookup Blueprint
description: Real-time Customer Profile lookups to provide context for agent-assisted support and sales.
solution: Experience Platform, Data Collection
kt: 7195
thumbnail: 
---

# Profile Lookup Blueprint

Profile Lookup Blueprint details the ability for external applications to access Adobe Experience Platform’s Real-time Customer Profile. This is performed by the external application performing an API GET request of a single or multiple profiles within Experience Platform’s profile store.

The result of the GET request is the full profile as represented in Experience Platform's Real-time Customer Profile system. This means that attributes, events, segment memberships, and model driven features that are stored in the profile can then be accessed and utilized by applications external to Adobe.

A good example is to use the profile lookup capability to surface richer context about a customer when they call into the call center for support. Support agents could then have visibility into the customer's lifetime value, propensity to churn or exposure to marketing campaigns, for example. 

You could also use the profile lookup during an agent-supported sales process, so the sales agent can have additional context or insight into the customer they are selling to.

Note that the current latency supported by the profile lookup API is ~ 500ms, making this approach not suitable for integration of the profile with real-time decision engines. For this capability the Edge Profile which has a latency <100ms must be utilized. Note that the Edge Profile capability is still in development.

## Architecture

<img src="assets/cah.svg" alt="Reference Architecture for the Profile Lookup Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

* [Standard Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementation Steps

1. Datasets and schemas configured
1. Profile configured – schema and dataset configured for profile, merge policy and identities configured
1. Data collected into platform and processed to profile
1. Entity API leveraged to lookup profile attribute – either from the record entity or the experience event entity

## FAQs & Documentation

* [Adobe Experience Platform Activation product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [Real-time Customer Profile documentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Profile Lookup API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
