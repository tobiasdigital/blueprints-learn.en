---
title: Data Science and Profile Enrichment Blueprint
description: AI/ML driven insights
solution: Experience Platform
kt: 
thumbnail: 
---

# Data Science and Profile Enrichment blueprint

## Description

Data Science & AI/ML Profile Enrichment details the ability to utilize Adobe Experience Platform's Data Science Workspace to train, deploy, and score models on data within Experience Platform's Data Lake to provide machine learning insights from the data. These insights and models can directly output to a dataset enabled for profile, enabling machine learning insights to further enrich the real-time customer profile.

Examples can include determining customer lifetime value, product and category affinity, propensity to convert or propensity to churn as a few examples. 

## Scenarios

| # | Scenario                                  | Description                                                                                                                                                                                                           | Experience Cloud Apps                      |
|---|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|
| 1 | Exploratory Data Science                  | Exploratory data science – discover signal, completeness, correctness of data<br>Discover new insights using data science tooling                                                                                     | AEP Intelligence                           |
| 2 | Profile enrichment with AI/ML<br> - batch | Discover, author, train, deploy, score model - output – in batch<br>Push model prediction to profile or to data lake for batch based activation<br>Score – runs a job via orchestration service. Writes to a dataset. | AEP Intelligence |

## Architecture

![Data Science](assets/datascience.svg)

## Implementation Steps

* Data loaded/ingested to AEP – schema, datasets created and data loaded.
* Create a DSW notebook.
* Choose a language - support for Python and PySpark.
* Author model in notebook.
* Train the model.
* Score the model to generate predictions with the target data.
* If pushing model results to the Real-time Customer Profile the model results dataset is enabled for Profile and the machine learned attributes are ingested to Profile.

## FAQs & Reference Documentation

* [Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Product Documentation](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)

