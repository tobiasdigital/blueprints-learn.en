---
title: Activation to Google Customer Match
description: Activation to FGoogle Customer Match.
solution: Real-time Customer Data Platform, Data Collection
kt: 7086
exl-id: 32bdc04d-b101-4b17-af27-329e5c71d888
---

# Activation to Google Customer Match

Ingest customer data from multiple sources to build a single profile view of the customer, segment these profiles to built audiences for marketing and personalization, share these audiences to Social Ad Networks such as Google Customer Match to target and personalization campaigns against those audiences. Google Customer Match lets you use your online and offline data to reach and re-engage with your customers across Google’s owned and operated properties, such as: Search, Shopping, Gmail, and YouTube.

## Use Cases

* Audience targeting for known audiences on social and advertising destinations.
* Online personalization with online and offline attributes.

## Applications

* Real-time Customer Data Platform

## Architecture

<img src="../assets/gcm.svg" alt="Reference architecture for Google Customer Match Activation" style="width:90%; border:1px solid #4a4a4a" />

## Implementation Steps

1. Configure Identity Namespaces to be used in Profile data sources.
    * Use out of the box namespaces such as Email, Email SHA256 Hash, where available.
    * Google Customer Match has a list of supported identities. In order to activate to Google Customer Match, one of the supported identities must be present in the profiles to be activated.
    * The following identities are currently supported by Google Customer Match: GAID, IDFA, phone_sha256_e.164, email_lc_sha256, user_id.
    * For additional details see the [Google Customer Match Destination Guide](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-customer-match.html).
    * Create custom namespaces where out of the box namespaces are not available for the applicable identities.
1. Configure Profile data source schemas and datasets.
    * Create Profile Record schemas for all profile record source data.
        * Specify the primary identity and secondary identities for each schema.
        * Enable the schema for profile ingestion.
    * Create Profile Record datasets for all profile record source data, assigning the associated schema.
        * Enable the dataset for profile ingestion.
    * Create Profile Experience Event schemas for all profile time series based source data.
        * Specify the primary identity and secondary identities for the schema.
    * Enable the schema for profile ingestion.
    * Create Profile Experience Event datasets for all profile experience event source data, assigning the associated schema.
        * Enable the dataset for profile ingestion.
1. Ingest the source data using a source connector into the associated dataset configured above.
    * Configure the source connector account with credentials.
    * Configure a dataflow to ingest the data from the source file or folder location at a specified schedule to the specified dataset.
    * Map any fields from the source data to the target schema.
    * Transform any fields to the correct format for ingestion into Experience Platform.
        * Date transformations
        * Transform to lowercase where appropriate - such as email address
        * Pattern transformations (phone number for example)
        * Add unique records IDs for experience event records if not present in the source data.
        * Transform arrays and map type fields to ensure correct mapping and modeling of arrays and maps for segmentation in Experience Platform.
1. Configure the Profile Merge Policy to ensure the correct configuration of the identity graph and which datasets should be included in the merging of profiles.
1. After dataflows have executed, ensure the profile data ingestion was successful with no errors.
    * Inspect the identity graph of several profiles to ensure correct processing of identity relationships.
    * Inspect the attributes and events of several profile to ensure correct ingestion of attributes and events to the profiles.
1. Author segments to create profile audiences
    * Build segments in the segment builder using rules against attributes and events.
    * Save the segment for evaluation. Segments will evaluate at the specified schedule once a day.
        * If the segment rules are eligible for streaming segmentation the segment will be evaluated as new streaming data is ingested for the profiles. Streaming segments will also be evaluated once per day during the scheduled batch segmentation.
1. Ensure the segment results are as expected.
    * Review the segment results count for the given segments.
    * Investigate the profile that should be included in the segment to verify the segment membership is included in the segment membership portion of the profile.
1. Configure the delivery of the audience to the destination in the Destination configuration.
    * See the [Google Customer Match Destination Guide](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-customer-match.html) for further details on configuring the Facebook Destination.
    * When configuring a destination, select which audience you would like to activate to the destination.
    * Determine the scheduled start date you would like the destination dataflow to begin delivering the audience to the destination.
    * Each destination has required and optional attributes that will be sent.
        * For Google Customer Match one of the required identities must be included and is used to match the profiles in the audiences within Experience Platform to a profile that is targetable by Google Customer Match.
    * Each destination also has a specified delivery type, whether streaming or batch, file based or JSON payload.
        * For Google Customer Match, audience memberships are delivered in streaming fashion to a Google Customer Match endpoint in JSON format.
        * Audience memberships will be delivered in streaming fashion subsequent to the streaming or batch segmentation evaluation in Experience Platform.
1. Ensure the destination flow has delivered the audience to the destination as expected. 
    * Check the monitoring interface to confirm the audience was delivered with the number of profiles expected. The audience size should be reflective of the expected number of profiles activated, noting that specific destination such as Google Customer Match will require certain fields, such as an email hash identity, and if not present in the profile that is a member of the audience, it will not be activated to the destination.
    * Check for any skipped profiles for profile identities missing or attributes missing that were mandatory.
    * Check for any other errors that may need to be resolved.
1. Verify the audience was activated to the end destination with the expected number of audience memberships.
    * After completing the activation flow, switch to your Google Ads account. The activated segments are shown in your Google account as customer lists. Please note that depending on your segment size, some audiences do not populate unless there are over 100 active users to serve.

## Guardrails

[Profile & Segmentation Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

## Related Documentation

Activation to Google Customer Match - [Destination Configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-customer-match.html)
