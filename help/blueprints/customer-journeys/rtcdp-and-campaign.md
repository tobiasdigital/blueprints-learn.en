---
title: Real-Time CDP with Adobe Campaign Blueprint
description: Showcases how the Adobe Experience Platform and its Real-Time Customer Profile and centralized segmentation tool can be utilized with Adobe Campaign to deliver personalized conversations.
solution: Experience Platform, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
---
# Real-Time CDP with Adobe Campaign Blueprint

Showcases how the Adobe Experience Platform and its Real-Time Customer Profile and centralized segmentation tool can be utilized with Adobe Campaign to deliver personalized conversations.

<br>

## Applications

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v7 or Campaign Standard

<br>

## Architecture

<img src="assets/rtcdp-campaign-architecture.svg" alt="Reference architecture for the Batch Messaging and Adobe Experience Platform Blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br> 

## Prerequisites

* Experience Platform and Campaign are recommended to be provisioned in the same IMS Org and be utilizing Adobe Admin Console for user access. This also ensures that customers can utilize the solution switcher from within the marketing UI

<br>

## Guardrails

### Adobe Campaign

* Only supports Adobe Campaign single organizational unit deployments
* Adobe Campaign is source of truth for all active profiles meaning profiles must exist in Adobe Campaign and new profiles should not be created based on Experience Platform segments.
* Campaign export workflows to run at most every 4hrs
* XDM schema and datasets for Adobe Campaign broadLog, trackingLogs and non-deliverable addresses are not out of the box and must be designed and built

### Experience Platform CDP segment sharing

* Recommendation of 20 segment limit
* Activation is limited to every 24hrs
* Only union schema attributes available for activation (no support for array/maps/experience events)
* Recommendation on no more than 20 attributes per segment
* One file per segment of all profiles with “realized” segment membership OR if segment membership is added as an attribute in the file both “realized” and “exited” profiles
* Incremental and full segment exports are supported
* File encryption is not supported

<br>

## Implementation Steps

### Adobe Experience Platform

#### Schema / Datasets

1. [Configure individual profile, experience event, and multi-entity schemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) in Experience Platform, based on customer-supplied data.
1. Create Adobe Campaign schemas for broadLog, trackingLog, non-deliverable addresses, and profile preferences (optional).
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) in Experience Platform for data to be ingested.
1. [Add data usage labels](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) in Experience Platform to the dataset for governance.
1. [Create policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) that enforce governance on destinations.

#### Profile / Identity

1. [Create any customer-specific namespaces](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Add identities to schemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Enable the schemas and datasets for Profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Set up merge policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) for differing views of [!UICONTROL Real-time Customer Profile] (optional).
1. Create segments for Adobe Campaign usage.

#### Sources / Destinations

1. [Ingest data into Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) using streaming APIs & source connectors.
1. Configure [!DNL Azure] blob storage destination for use with Adobe Campaign.

#### Adobe Campaign

1. Configure schemas for profile, lookup data, and relevant delivery personalization data.
    
>[!IMPORTANT]
>
>It's critical to understand at this point what the data model is within Experience Platform for profile and event data so you know what data will be required in Adobe Campaign.
    
#### Import workflows

1. Load and ingest simplified profile data onto Adobe Campaign sFTP.
1. Load and ingest orchestration and messaging personalization data onto Adobe Campaign sFTP.
1. Ingest Experience Platform segments from [!DNL Azure] blob via workflows.

#### Export workflows

1.  Send Adobe Campaign logs back to Experience Platform via workflows every four hours (broadLog, trackingLog, non-deliverable addresses).
1.  Send profile preferences back to Experience Platform via consulting-built workflows every four hours (optional).


### Mobile Push Configuration

* Two supported approaches for integrating with mobile devices for push notifications:
    * Experience Platform Mobile SDK
    * Campaign Mobile SDK
* Experience Platform Mobile SDK route:
    * Leverage Adobe Tags and the Campaign Classic extension for setting up your integration with the Experience Platform Mobile SDK
    * Need a working knowledge of Adobe Tags and data collection
    * Need mobile development experience with push notifications in both Android and iOS to deploy the SDK, integrate with FCM (Android) and APNS (iOS) to get push token, configure your app to receive push notifications and handle push interactions
* Campaign Mobile SDK
    * Please follow the [Campaign SDK documentation](Campaign Mobile SDK
Please follow the deployment documentation outlined here)

    >[!IMPORTANT]
    >If you deploy the Campaign SDK and are working with other Experience Cloud applications they will require the use of the Experience Platform Mobile SDK for data collection. This will create duplicate client side calls on the device.

## Related Documentation

* [Adobe Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classic documentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard documentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
