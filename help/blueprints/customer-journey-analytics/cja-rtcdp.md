---
title: Customer Journey Analytics with Real-time Customer Data Platform
description: Unify and analyze data and customer behaviors from across the customer journey in Customer Journey Analytics, publish audience from CJA to RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
---
# Customer Journey Analytics with Real-time Customer Data Platform

Create and publish audiences identified in Customer Journey Analytics (CJA) to Real-time Customer Profile in Adobe Experience Platform for customer targeting and personalization. Ideal for creating audiences using historical data or more refined audiences from granular filtering and computed fields in Customer Journey Analytics.

## Customer Journey Analytics Audience Publishing Guide

See the following documentation for guidance on implementation and configuration on publication of audiences from Customer Journey Analytics to Real-time Customer Data Platform. [Documentation](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html)

## Architecture for Customer Journey Analytics Blueprints

![Architecture diagram](assets/CJA_RTCDP.svg)

## Guardrail diagram for Customer Journey Analytics Blueprints

* For detailed guardrails and end to end latencies refer to the [deployment guardrails document](../experience-platform/deployment/guardrails.md)

![Guardrail diagram](../experience-platform/assets/CJA_guardrails.svg)

## Frequently asked Questions

* If a corresponding profile does not exist in RTCDP that CJA sent, will a new profile be created, or are audiences only recorded from CJA for profiles that are already present? Yes, a new profile will be created. As a result if your RTCDP implementation is for known customers only, the CJA audience rules should be written to filter for only profiles with known identities. This will ensure that the RTCDP Profile count does not increase from anonymous profiles if not desired.

* Does CJA send the audience data over as pipeline events or a flat file that also goes to data lake as well? CJA audiences are streamed over pipeline to RTCDP Profile Service, however the data is also stored in data lake as a dataset.

* What identities does CJA send over? CJA sends over whichever identities were configured as the "person ID" during CJA configuration.

* What is set as the primary identity? Whatever identity the user selected when they set up CJA as the primary "person" ID.

* Does the identity service process the CJA messages as well? i.e. can CJA add identities to a profile identity graph through audience sharing? No, identity service does not process the CJA messages.

## Related Blog Posts

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184)
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17)
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1)
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281)
* [[!DNL Demonstrating the Power of Adobe’s New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34)
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9)
