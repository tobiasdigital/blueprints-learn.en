---
title: Custom Data Science for Profile Enrichment Blueprint
description: This blueprint shows how Adobe Experience Platform's Data Science Workspace can use data within Experience Platform to train, deploy, and score models to provide machine learning insights from the data.
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
---
# Custom Data Science for Profile Enrichment Blueprint

Custom Data Science for Profile Enrichment Blueprint illustrates how data in Adobe Experience Platform can be used in [!UICONTROL Data Science Workspace] to train, deploy, and score models to provide machine learning insights. These models can directly output to a dataset enabled for [!UICONTROL Real-time Customer Profile] to further enrich customer profiles. These insights can then be actioned for personalization. Examples of machine learning insights include lifetime value scoring, product and category affinity, propensity to convert, or propensity to churn. 

## Use Cases

* Extract insight and discover patterns from customer data in Experience Platform. Train and score models from this data.
* Enrich the [!UICONTROL Real-time Customer Profile] with model driven insights and attributes for more granular personalization and optimized journeys.
* Train and Score models to determine customer insights such as customer lifetime value, propensity to convert or churn, product and content affinities, and engagement scores. 

## Architecture

<img src="assets/datascience.svg" alt="Reference Architecture for the Custom Data Science for Profile Enrichment Blueprint" style="border:1px solid #4a4a4a" />

## Implementation Steps

1. Create schemas and datasets.
1. Ingest data into Experience Platform.
1. Create a DSW notebook.
1. Choose a language. Python and PySpark are supported.
1. Author model in notebook.
1. Train the model.
1. Score the model to generate predictions with the target data.
1. Enable the model results dataset for profile, if pushing model results to the [!UICONTROL Real-time Customer Profile].

## Related Documentation

* [Adobe Experience Platform Intelligence product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Data Science Workspace] documentation](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [[!UICONTROL Data Science Workspace] tutorials](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## Related Blog Posts

* [!DNL Simplifying the Data Science Lifecycle with Adobe Platform Experience](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [!DNL Gaining a Deeper Understanding of Churn Using Data Science Workspace](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [!DNL Understanding Data Science In Adobe Experience Platform](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [!DNL Reimagining Jupyter Notebooks for Enterprise Scale](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [!DNL Accelerate Intelligent Insights with Adobe Experience Platform Data Science Workspace](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [!DNL A Preview of Time Series Forecasting with Adobe Experience Platform](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
