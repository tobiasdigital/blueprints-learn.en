---
title: Journey Optimizer - Triggered Messaging and Adobe Experience Platform Blueprint
description: Execute triggered messages and experiences using Adobe Experience Platform as a central hub of streaming data, customer profiles, and segmentation.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
---
# Journey Optimizer

Adobe Journey Optimizer is a purpose built system for marketing teams to react in real-time to customer behaviors and meet them where they are at. Data management capabilities have been moved to the Adobe Experience Platform allowing marketing teams to focus on what they do best: which is creating world class customer journey's and personalized conversations.  This blueprint outlines the technical capabilities of the application and provides a deep dive into the various architectural components that make up Adobe Journey Optimizer. 

## Use Cases

* Triggered messages
* Registration confirmations
* Shopping cart and application form abandons
* Location triggered messages

## Architecture

<img src="assets/journey-optimizer.png" alt="Reference architecture for the Triggered Messaging and Adobe Experience Platform blueprint" style="border:1px solid #4a4a4a" />

## Integration Patterns

* Adobe Experience Platform -> Journey Optimizer

## Prerequisites

1. Customer must be provisioned for Experience Cloud with a valid IMS Org
1. Mobile Push

* Customer must have a mobile developer available to build the app 
* Adobe Experience Platform Mobile SDK
* Data Collection
   * Mobile tags property
      * Extensions: 
        * Adobe Journey Optimizer Extension
        * Adobe Experience Platform Edge Network
        * Identity
        * Mobile Core
        * Profile
    * App Configurations
    * Datastreams
        * Enabled for Experience Platform
        * Event Dataset - used for collecting general mobile behavior
        * Profile Dataset - AJO Push Profile Dataset (cannot be different)

## Guardrails

* See link for more details on guardrails for Journey Optimizer [LINK](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)
* Batch segments – need to ensure you understand the daily volume of qualified users and ensure the destination system can handle the burst throughput per journey and across all journeys
* Streaming segments – need to ensure the initial burst of profile qualifications can be handled along with the daily streaming qualifying volume per journey and across all journeys
* Profile update activity - the Real-Time Customer Profile can be updated natively from within a journey.  There is a delay of up to 1min on processing the update into the profile store
* Business events - a read segment based journey can be triggered to start based on an external call into the JO system
* Natively supports Offer Decisioning in messages only. Future support via native action
* Channels Supported:
  * Email
  * Push (FCM / APNS)
  * Rest API Endpoints
* Processes 5k events per second with horizontal scaling (wallet is limitation)
* A/B testing is done by using two deliveries and determining results using QS or CJA
* Litmus Integration – must have an account with Litmus to leverage integration

## Implementation Steps

### Adobe Experience Platform

#### Schema/Datasets

1. [Configure individual profile, experience event, and multi-entity schemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) in Experience Platform, based on customer-supplied data.
1. Create Adobe Campaign schemas for broadLog, trackingLog, non-deliverable addresses, and profile preferences (optional).
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) in Experience Platform for data to be ingested.
1. [Add data usage labels](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) in Experience Platform to the dataset for governance.
1. [Create policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) that enforce governance on destinations.

#### Profile/Identity

1. [Create any customer-specific namespaces](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Add identities to schemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Enable the schemas and datasets for Profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Set up merge policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) for differing views of [!UICONTROL Real-time Customer Profile] (optional).
1. Create segments for campaign usage.

#### Sources/Destinations

1. [Ingest data into Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) using streaming APIs & source connectors.1. Configure [!DNL Azure] blob storage destination for use with Adobe Campaign.

#### Mobile app deployment

1. Implement Adobe Campaign SDK for Adobe Campaign Classic or Experience Platform SDK for Adobe Campaign Standard. If Experience Platform Launch is present, the recommendation is to use Adobe Campaign Classic or Adobe Campaign Standard extension with Experience Platform SDK.


### Journey Orchestration

1. Streaming data used to initiate a customer journey must be configured within Journey Optimizer first to get an orchestration ID. This orchestration ID is then supplied to the developer to use with ingestion.
1. Configure external data sources.
1. Configure custom actions.

## Related Documentation

* [Adobe Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Optimizer documentation](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
