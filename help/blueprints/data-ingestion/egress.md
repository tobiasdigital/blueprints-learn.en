---
title: Data Access and Export Blueprint
description: This blueprint provides and overview of all the methods by which data can be accessed and exported from Adobe Experience Platform and applications.
solution: 
thumbnail: 
---
# Data Access and Export Blueprint

The Data Access and Export Blueprint outlines all the possible methods whereby data can be accessed or exported from Adobe Experience Platform and Applications.

The Blueprint is broken up into two categories for data access from Experience Platform and applications. First, approaches for egressing data from Experience Platform and applications; this would be considered a push type method of data egress. Second, approaches for access data from Experience Platform and applications; this would be conssidered a pull type method of data access.

Data Access Approahces

* [Real-time Customer Profile Access API](#rtcp-profile-access-api)
* [Data Access API](#data-access-api)
* [Query Service](#query-service)

Data Export Approaches

* [Client Side Tags](#client-side-tags-extensions)
* [Event Forwarding](#event-forwarding)
* [Real-time Customer Data Platform Destinations](#RTCDP-destinations)
* [Journey Optimizer Custom Actions](#jo-custom-actions)

## Data Access and Export Overview Architecture

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Reference architecture for the Data Preparation and Ingestion Blueprint" style="width:90%; border:1px solid #4a4a4a" />

## Approaches for Data Access

### Real-time Customer Profile Access API {#rtcp-profile-access-api}

Customers can access single unified profiles from the Real-time Customer Profile store including all profile identities, audience memberships, attributes and experience events using the Real-time Customer Profile Access API.

Refer to the [Real-time Customer Profile Access API](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en) documentation for additional information.

#### Use Cases

* Lookup a single profile to add context to agent customer interaction such as a support interactions through chat and call center, or a sales interaction at the point of sale.
* Allow added context to a personalization descision made by an external system, for example a web personalization system or a offer decision system.

#### Considerations

* Real-time Customer Profile [guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) apply.
* Designed for single profile lookup at a time. Not used for bulk profile access or download of the entire profile population for the use of analysis or data science. 
* Profile lookup response time adhears to the profile guardrails. Low latency requirements - for example for same page personalization requirements should utilize the Edge Profile or customer personalization destinations for low latency profile access. [Documnetation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en).

### Data Access API {#data-access-api}

Using the data access API customers can directly access the raw dataset files that are stored in the Experience Platform data lake.

* For additional details on using the data access API please refer to the [documentation](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=en).

#### Use Cases

* Pull raw and processed data files from Experience Platform for storage and evaluation in enterprise environments.

#### Considerations 

* As data is accessed in a batch asynchronous fashion the access to the data will be inherently latent as compared to streaming data egress approaches such as utlitizing Tags, Event Forwarding, or RTCDP Destinations.
* Data files when processed into Experience Platform are stored as collections of files in batches and are compressed and stored in parquet format. As such when accessing and downloading the files to a different environment they must be systematically accessed by their batch and file as oppossed to an entire dataset and any operations on the data must account for the files being compressed in parquet format. 

### Query Service {#query-service}

Using the experience platform Query Service customers can query datasets within Experience Platform and persist the results of the query. A SQL Client can be utilized to query and persist the query response in the desired storage destination that the SQL client can support. The Query Service UI can be used to store the SQL result in a target dataset in the Experience Platform or the results can be saved to the local machine.

* For additional details on connectin to SQL clients to persist SQL results from Experience Platform Query Service see the following [documentation](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=en).

#### Use Cases

* Query raw data from the Experience Platform datasets and persist the query results.
* Query the profile snapshot dataset to extract insights on the Real-time Customer Profile. [Documentation](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets). 
* Store query results into a separate dataset for access or into a profile enabled dataset which can later be egressed through RTCDP and other Experience Cloud applications which access the Real-time Customer Profile. 

#### Considerations

* As data is queried in a batch asynchronous fashion the access to the data will be inherently latent as compared to streaming data egress approaches such as utlitizing Tags, Event Forwarding, or RTCDP Destinations.
* Only data that is available in the Experience Platform data lake can be queried using the Query Service. The Real-time Customer Profile store, the identity graph, Customer Journey Analytics can not be directly queried using the Query Service. Only when datasets are exported to the data lake can these datasets be queried, as in the example of the profile snapshot dataset.
* Note that guardrails for the number of query results and the query timeout apply as outlined in the [Query Services guardrails](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en) documentation.

## Approaches for Data Export

### Client Side Tags Extensions {#client-side-tags-extensions}

Extensions can be deployed using Adobe's Tags solution. Once an extension is deployed data requests are deployed directly on a client browser or application and a request can be invoked to send data and requests to the desired destination.

Refer to the [Tags Overview](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en) documentation for additional information.

#### Use Cases

* Collect raw streaming information directly from client side environments using tagging.

#### Considerations

* No direct access to any server side information such as the Experience Platform Real-time Customer Profile and audience memberships. 
* Adding additional data collection tags to the page may increase page load times.
* Ability to set up rules to only request data when certain criteria are met. 
* Data is collected directly from the client, limiting the types of transformations and enrichment that can be performed prior to collecting the data.

### Event Forwarding {#event-forwarding}

Data collection requests are collected directly to Adobe's Edge Network. From the Edge Network requests to external RESTful endpoints can ba configured to forward these requests on to the external destination. 

Refer to the following [Event Forwarding](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en) documentation for additional information.

#### Use Caseas

* Collect raw streaming information directly from client side environments to a enterprise endpoint using Adobe's server side event forwarding.

#### Considerations

* To use Event Forwarding, data must be sent to the Edge Network using the WebSDK or MobileSDK.
* Event forwarding approach reduces the page load time and weight due to additional tags being added on the page.
* No enrichment from the edge profile or other data sources is currently supported. 
* Limited data filtering and simple mapping transformations are supported.

### Real-time Customer Data Platform Destinations {#RTCDP-destinations}

Profile attribute data and audience membership data can be activated to enterprise and advertising destinations. This means the data egressed must be ingested into the Experience Platform Real-time Customer Profile. 

Refer to the [Real-time Customer Data Platform Destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en) documentation for additional information.

#### Use Cases

* Activate profile attibute information including audience membership to a interl enterprise data store, analytsis tool, email system, or support system.
* Activate profile audience membership to a external advertising vender to target and personalize content to the profile. 

#### Considerations

* Profile attributes and audience memberships can be activated. Raw experience events can not currently be activated as part of RTCDP Destinations. 
* Activations happen in streaming or batch depending on the nature of the segment evalution and the nature of the ingestion protocal that the destination accepts.

### Journey Optimizer Custom Actions {#jo-custom-actions}

Using Journey Optimizer customers can invoke a custom action from the journey canvas to send a payload or message to a external API endpoint that is configured. An action can be configured to any service from any provider that can be called through a REST API with a JSON-formatted payload. This payload can include event information, profile attributes and prior event data, transformations and enrichments that are configured in the journey.

Refer to the [Journey Optimizer custom actions](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en) documentation for additional information.

#### Use Cases

* Activation events from Experience Platform and Journey Optimizer that include additional information from the Real-time Customer Profile.
* Notify external systems when a customer has reached a specific point of a journey. 

#### Considerations

* Guardrails on the throughput supported by [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en) and enrichments supported by the [Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) apply.
* Custom actions can be performed in a streaming one by one fashion for each event or profile in a journey. Bulk operations or bulk data egress in the form of files or aggregated requests across customer journeys can not be performed. 
* Streaming access to Real-time Customer Profile attributes and experience events which can be included in the activation payload.
* Event data can be filtered and simple mapping transformations applied before sending events to external destinations. 










