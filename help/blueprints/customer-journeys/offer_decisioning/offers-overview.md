---
title: Decision Management Overview
description: Deliver personalized offers across customer journeys.
solution: Experience Platform, Journey Optimizer
---
# Journey Optimizer - Decision Management Overview

To learn more about Decision Management refer to the product documentation [HERE](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

Adobe Decision Management is a service provided as part of Adobe Journey Optimizer. This blueprint outlines the use cases and technical capabilities of the application and provides a deep dive into the various architectural components and considerations that make up Decision Management.

Journey Optimizer is used to deliver the best offer and experience to your customers across all touch points at the right time. Decision Management makes personalization easy with a central library of marketing offers and a decision engine that applies rules and constraints to rich, real-time profiles created by Adobe Experience Platform to help you send your customers the right offer at the right time.

The Decision Management capability consists in two main components:

* The Centralized Offer Library which is the interface where you create and manage the different elements that compose your offers, and define their rules and constraints.
* The Offer Decision Engine which leverages Adobe Experience Platform data and Real-time Customer profiles, along with the Offer Library, in order to select the right time, customers and channels to which offers will be delivered.

<img src="../assets/offers_overview.png" alt="Decision Management" style="width:100%; border:1px solid #4a4a4a" />

Decision Management can be deployed in one of two ways, on the edge or via the hub. Each of these methods has a specific set of interfaces and protocols for operating the service as outlined in the respective blueprints referenced below. Additional details can also be obtained in the Decision Management Documentation [HERE](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## Decision Management on the hub

The first is via the Adobe Experience Platform hub, which is a central data center architecture. In the "hub" approach offers are executed, personalized, and delivered in >500ms latency. Thus the hub architecture is best suited for customer experiences that do not demand sub-second latency, examples include offer decisions which are provided for kiosks or agent assisted experiences such as in call centers or in person interactions. Offers that are inserted into emails, SMS messages, or push notifications and other outbound campaigns are also powered by the hub approach. To learn more about Decision Management on the hub refer to the [Decision Management on the hub](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-hub.html?lang=en) blueprint.

* Offer eligibility can operate agains the full real-time customer profile, including all attributes and experience events

### Use Cases for Decision Management on the hub

* Personalized offers on kiosks and in store experiences.
* Personalized offers via agent assisted experience such as to call centers or sales intereactions.
* Offers included in email, SMS, or other outbound interactions.
* Cross channel journey execution - offer consistency across web, mobile, email, and other interaction channels through Adobe Journey Optimizer.

### Decision Management on the hub technical considerations

* Requests per second = 2000.
* Latency of response < 500ms.
* Access to full real-time customer profile including audience memberships, attributes and experience events.

## Decision Management on the edge

The second approach is via the Experience Edge Network, which is a globally distributed geographically located infrastructure to serve fast sub-second and millisecond experiences. The end consumer experience being executed by the edge infrastructure closest to the consumers geo-location to minimize latency. Decision Management on the Edge is designed to serve real-time consumer experiences such as web or mobile inbound personalization requests. To learn more about Decision Management on the Edge refer to the [Decision Management on the edge](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html?lang=en) blueprint.

### Use Cases for Decision Management on the edge

* Online personalization via web or mobile inbound experiences.
* Cross channel journey execution - offer consistency across web, mobile, email, and other interaction channels through Adobe Journey Optimizer.

### Decision Management on the edge technical considerations

* Requests per second = 5000.
* Latency of response < 250ms.
* Access to edge real-time profile. Only edge projected audiences and profile attributes will be available in the profile. 
* If personalization is required in first time experiences, hub will be ideal as the full profile is available. The edge profile must sync from the hub for the first time edge experience. Hence the very first experience from the edge will not include prior uploaded profile data to the hub.

## Related Documentation

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer Decision Management](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html) 
* [Adobe Journey Optimizer Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe Decision Management Product Description](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)