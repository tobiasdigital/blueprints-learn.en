---
title: Real-Time CDP with Adobe Campaign v8 Integration Pattern
description: Showcases how the Adobe Experience Platform and its Real-Time Customer Profile and centralized segmentation tool can be utilized with Adobe Campaign v8 to deliver personalized conversations.
solution: Real-time Customer Data Platform, Campaign
---
# Real-Time CDP with Adobe Campaign v8 Integration Pattern

Showcases how the Adobe Experience Platform and its Real-Time Customer Profile and centralized segmentation tool can be utilized with Adobe Campaign to deliver personalized conversations.

<br>

## Applications

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v8

<br>

## Architecture

<img src="assets/rtcdp-campaignv8-architecture.svg" alt="Reference architecture for the Batch Messaging and Adobe Experience Platform Integration Pattern" style="width:100%; border:1px solid #4a4a4a" />

<br> 

## Prerequisites

* Customer must be provisioned for Experience Cloud with a valid IMS Org 
* Adobe Experience Platform and Campaign are recommended to be provisioned in the same IMS Org for single login URL
* Customer must be provisioned V8 instance of Campaign
* Customer must be eligible and have access for RTCDP, Sources, Destinations.
* Adobe Campaign product context must exist
<br>

## Implementation Steps

Refer to the following documentation on configuring the Campaign v8 source connector to Adobe Experience Platform and the Real-time Customer Data Platform destination connector to Campaign v8.
[Campaign and AEP Connectors](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=en)

## Guardrails

### Adobe Campaign

* Refer to the Campaign source connector documentation - [Campaign Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=en)
* Only supports Adobe Campaign single organizational unit deployments
* Adobe Campaign is source of truth for all active profiles meaning profiles must exist in Adobe Campaign and new profiles should not be created based on Experience Platform segments.


### Experience Platform Real-time Customer Data Platform segment sharing

* Refer to the RTCDP Campaign Destination connector - [RTCDP Campaign Connection](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html)
* Recommendation of 50 segment limit
* Note that segment membership realization from AEP is latent for both batch (1 per day) and streaming (~5 min) and based on segment evaluation schedule.
* The activation latency is 3 hours minimum
* Only union schema attributes available for activation (no support for array/maps/experience events)
* Recommendation on no more than 20 attributes per segment
* One file per segment of all profiles with “realized” segment membership OR if segment membership is added as an attribute in the file both “realized” and “exited” profiles
* Incremental and full segment exports are supported
* File encryption is not supported
* See profile and data ingestion guardrails for AEP - [Link](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)