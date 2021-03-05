---
title: Batch Messaging and Adobe Experience Platform
description: Execute scheduled and batch messaging campaigns using Adobe Experience Platform as a central hub for customer profiles and segmentation.
solution: Experience Platform, Campaign
kt: 7196
thumbnail: 
---

# Batch Messaging and Adobe Experience Platform scenario

Execute scheduled and batch messaging campaigns using Adobe Experience Platform as a central hub for customer profiles and segmentation.

## Use Cases

* Scheduled email campaigns
* Onboarding and re-marketing campaigns

## Applications

* Adobe Experience Platform
* Adobe Campaign Classic or Standard

## Integration Patterns

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## Architecture

<img src="assets/aepbatch.svg" alt="Reference architecture for the Batch Messaging and Adobe Experience Platform scenario" style="border:1px solid #4a4a4a" />

## Guardrails

* Supports Campaign single organizational unit deployments only
* Campaign is source of truth for all active profiles meaning profiles must exist in Campaign and new profiles should not be created based on Experience Platform segments.
* Segment membership realization from Experience Platform is latent for both batch (1 per day) and streaming (~5 min)

### Real-time Customer Data Platform segment sharing to campaign:

* Recommendation of 20 segment limit
* Activation is limited to every 24 hrs
* Only union schema attributes available for activation (no support for array/maps/experience events). 
* Recommendation on no more than 20 attributes per segment
* One file per segment of all profiles with “realized” segment membership OR if segment membership is added as an attribute in the file both “realized” and “exited” profiles
* Incremental or full segment exports are supported
* File encryption is not supported
* Campaign export workflows to run at most every 4 hrs
* See [profile and data ingestion guardrails for Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

### Adobe Experience Platform

*  Schema / Datasets
    1.  Configure individual profile, experience event, and multi-entity schemas in Experience Platform based on customer-supplied data
    1.  Create Campaign schemas for the following: broadLog / trackingLog / non-deliverable addresses / profile preferences (optional)
    1.  Add data usage labels to the dataset for governance
    1.  Create policies to enforce governance on destinations

*  Profile / Identity
    1.  Create any customer-specific namespaces
    1.  Add identities to schemas
    1.  Enable schemas and datasets for profile
    1.  Set up merge rules for differing views of Real-time Customer Profile (optional)
    1.  Create segments for campaign usage

*  Sources / Destinations
    1.  Ingest data into Experience Platform using streaming APIs & source connectors
    1.  Configure Azure blob storage destination for use with Campaign

*  Mobile app deployment
    1.  Implement Campaign SDK for Campaign Classic or Experience Platform SDK for Campaign Standard.  If Experience Platform Launch is present recommendation is to use Campaign Classic/Standard extension with Experience Platform SDK.

*  Campaign
    1.  Configure schemas for profile, lookup data, and relevant delivery personalization data
    
        >[!IMPORTANT]
        >
        > It's critical to understand at this point what the data model is within Experience Platform for profile and event data so you know what data will be required in Campaign.
    
    1.  Import workflows
        1.  Load and ingest simplified profile data onto Campaign sFTP
        1.  Load and ingest orchestration and messaging personalization data onto Campaign sFTP
        1.  Ingest Experience Platform segments from Azure blob via workflows

*  Export workflows
    1.  Send Campaign logs back to Experience Platform via workflows every 4 hrs (broadLog, trackingLog, non-deliverable addresses)
    1.  Send profile preferences back to Experience Platform via consulting-built workflows every 4 hrs (optional)


## Related Documentation

* [Adobe Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classic documentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard documentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
