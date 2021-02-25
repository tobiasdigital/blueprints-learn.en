---
title: Multi-channel Message Orchestration Blueprint
description: Deliver individual, just-in-time customer experiences across screens.
solution: Experience Platform
kt: 
thumbnail: 
---

# Multi-channel Message Orchestration Blueprint

## Description

Multi-channel message orchestration addresses the ability for brands to proactively engage and communicate with their customers through channels such as email, SMS, and mobile alerts. Orchestration tools can also be integrated with other interaction channels such as with inbound channels for web/mobile personalization by sharing audience state with the other channel specific decision engines. A number of factors go into what applications and deployment options should be used for multi-channel message orchestration, including whether the customer interaction will be trigger based or scheduled, as well as what data will be necessary for the required targeting and personalization of the interactions. This results in a number of possible scenarios and deployment options when building out message orchestration capability.

## Scenarios


| Scenario | Description |  Experience Cloud Applications | 
|---|---|---|
| **Batch & Transactional Messaging**  | <ul><li>Author and execute scheduled and batch outbound campaigns</li><li>Delivery transactional messages</li></ul> | <ul><li>Adobe Campaign Classic and Managed Services</li><li>Adobe Campaign Standard</li></ul>| 
| **[Batch Messaging & Adobe Experience Platform](aepmessaging.md)** | <ul><li>Execute scheduled and batch messaging campaigns using Adobe Experience Platform as a central hub for customer profiles and segmentation.</li></ul> | <ul><li>Adobe Real-time Customer Data Platform</li><li>Adobe Campaign Classic, Managed Services, or Campaign Standard</li><li>Supported 3rd party Messaging Provider</li></ul> |
| **[Triggered Messaging & Adobe Experience Platform](triggered.md)** | <ul><li>Execute triggered and streaming messaging using Adobe Experience Platform as a central hub for streaming data, customer profiles and segmentation, with Adobe Journey Orchestration for streaming journey orchestration and message delivery.</li></ul> | <ul><li>Adobe Experience Platform</li><li>Adobe Journey Orchestration</li><li>Adobe Campaign or other 3rd party application for message delivery</li></ul> |
