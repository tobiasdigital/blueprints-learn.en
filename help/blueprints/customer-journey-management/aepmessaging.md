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

## Reference Architecture

<img src="assets/aepbatch.svg" alt="Reference architecture for the Batch Messaging and Adobe Experience Platform scenario" style="border:1px solid #4a4a4a" />

## Integration Patterns

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## Prerequisites

* Adobe Experience Platform
* Adobe Campaign Classic or Standard

## Guardrails

* Supports Campaign single organizational unit deployments only
* Campaign is source of truth for all active profiles meaning profiles must exist already in Campaign and new profiles should not be created based on Experience Platform segments.
* Note that segment membership realization from Experience Platform is latent for both batch (1 per day) and streaming (~5 min)

### Real-time Customer Data Platform segment sharing to campaign:

* Recommendation of 20 segment limit
* Activation is limited to every 24hrs
* Only union schema attributes available for activation (no support for array/maps/experience events). 
* Recommendation on no more than 20 attributes per segment
* 1 file per segment of all profiles with “realized” segment membership OR if segment membership is added as an attribute in the file both “realized” and “exited” profiles
* Incremental or full segment exports are supported
* File encryption is not supported
* Campaign export workflows to run at most every 4hrs
* See [profile and data ingestion guardrails for Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementation Steps and Considerations

### Adobe Experience Platform

*  Schema / Datasets
    1.  Individual profile, experience event and multi-entity schemas are configured in Experience Platform based on customer supplied data
    1.  Campaign schemas are created for all of the following: broadLog / trackingLog / non-deliverable addresses / profile preferences (optional)
    1.  Dataset labels are added for governance
    1.  Policies are created for enforcing governance on destination

*  Profile / Identity
    1.  Any customer-specific namespaces are created for datasets
    1.  Identities are added to schemas
    1.  Schema and datasets are enabled for profile
    1.  Merge rules are setup if differing views of real-time customer profile (optional)
    1.  Segments are created for campaign usage

*  Sources / Destinations
    1.  Data is ingested into Experience Platform leveraging streaming API’s & source connectors
    1.  Azure blob storage destination is configured for use with Campaign

*  Mobile app deployment
    1.  Implement Campaign SDK for ACC or Experience Platform SDK for ACS.  If Launch is present recommendation is to use ACC/ACS extension with Experience Platform SDK.

*  Campaign
    1.  Schemas configured for profile, lookup data and relevant delivery personalization data
    1.  Critical to understand at this point what the data model is within Experience Platform for profile and event data so you know what data will be required in Campaign
    1.  Import workflows
        1.  Simplified profile data is loaded onto Campaign sFTP and ingested
        1.  Orchestration and messaging personalization data is loaded onto Campaign sFTP ingested
        1.  Experience Platform segments are ingested from Azure blob via workflows

*  Export workflows
    1.  Campaign logs are sent back to Experience Platform via workflows every 4hrs (broadLog, trackingLog, non-deliverable addresses)
    1.  Profile preferences are sent back to Experience Platform via consulting-built workflows every 4hrs (optional)


## FAQs & Reference Documentation

* [Adobe Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classic documentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard documentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
