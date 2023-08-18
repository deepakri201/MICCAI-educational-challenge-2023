# MICCAI Educational Challenge 2023: Exploring AI-derived annotations in Imaging Data Commons (IDC)

This repository accompanies the Medium article [Exploring AI-derived annotations in Imaging Data Commons (IDC)](https://medium.com/@deepa.krishnaswamy2/exploring-ai-derived-annotations-in-imaging-data-commons-idc-e60b030eca17), in submission for the [MICCAI Educational Challenge 2023](https://miccai-sb.github.io/challenge). 

One of the issues with AI model development is how to validate you results when you do not have expert annotations. In this article, we demonstrate how to interact with segmentation results in multiple ways: 
- How to use a dashboard to interact with and explore segmentation results
- How to query for data and features of interest using both a console and python code, and analyze distributions of features using the bokeh package 
- How to download segmentation objects and view/interact with them using the ITKWidgets package

Along the way, we introduce Imaging Data Commons, a cloud-based platform for cancer imaging data, as well as features of Google Cloud Platform that enable interactive analysis using dashboard and retrieving/querying of data. 

--- 

## Use a dashboard to interact with your data 

In the dashboard [here](https://lookerstudio.google.com/u/0/reporting/a9ead556-4f23-4139-a008-1135772b358a/page/p_wsm498cc3c?s=idUgo-ggtN0), you can interact with AI-derived annotations that we generated for two lung cancer CT imaging collections, for approximately 1,000 patients. We used publicly available methods to automatically generate segmentations for thoracic organs including the heart, trachea, aorta and esophagus, and also extracted shape features from these regions. We also used methods to automatically generate landmarks and body part regions for transverse slices. 

Watch the gif below to learn how to interact with the dashboard.

![nlst_dashboard_usage](https://github.com/deepakri201/MICCAI-educational-challenge-2023/assets/59979551/35ec2edf-11f9-4c6e-98f2-93bbcb72c6e3)


## Feature comparison of different regions for NLST

We focus on the segmentation results in [this paper](https://arxiv.org/abs/2306.00150), where we focused on enhancing annotations of patients in lung cancer computed tomography (CT) datasets. We analyzed the National Lung Screening Trial (NLST) and NSCLC-Radiomics datasets, where only NSCLC-Radiomics has some expert annotations provided. We used a pre-trained nnU-Net model to segment thoracic organs-at-risk, which include the heart, aorta, trachea and esophagus. 

Since we did not have expert annotations to compare to for NLST, we needed a way to quickly and efficiently examine the results of segmentations, and investigate any outliers. For this we extracted shape features from each of the regions, and looked at distributions of these values. 

Here we pick a single feature (sphericity), and look at the distribution of this feature across all four regions. We show how to:

- Query metadata in IDC using BigQuery (similar to SQL) to get the data we need 
- Use the python package bokeh to create an interactive plot that will open up the IDC portal where you can view the data

Click on this figure to open up an interactive plot! Here you can click on points which will open up a link to the IDC portal.

[![](https://github.com/deepakri201/MICCAI-educational-challenge-2023/blob/main/bokeh_figure_new.png | width=100px)](https://htmlpreview.github.io/?https://github.com/deepakri201/MICCAI-educational-challenge-2023/blob/main/bokeh_figure_new.html)

## Use ITKWidgets to display the AI-derived segmentations

Now, what if you want to actually access one of these segmentations? Here we show you how to:

- Use `BigQuery` to pick a patient in NLST that has a segmentation
- How to download this segmentation object using `gsutil`
- How to find the corresponding ID for the raw CT data
- How to query and download the raw CT data
- How to use `ITKWidgets` to plot the CT data overlaid with the segmentation!

Here's an example of using ITKWidgets: 

![itkwidgets_downsized_optimized](https://github.com/deepakri201/MICCAI-educational-challenge-2023/assets/59979551/ae3920ba-fd2f-4312-a004-af0ca86a1b02)
