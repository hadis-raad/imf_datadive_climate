# Geospatial Building Type Predictor

## Introduction

OpenStreetMaps (OSM) serves as a valuable resource for retrieving structural types during geocoding. However, the project recognizes that limited coverage can diminish the reliability of results for geospatial analysis. To tackle this challenge, the objective is to develop a machine learning model capable of predicting structure types for any building footprint available in OSM. This project is based on the article ["Predicting building types using OpenStreetMap"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9676186/) and utilizes the associated [data](https://osf.io/3j46v/) and [code](https://github.com/heykuldip/osm_buildings_classification/tree/main).

This project is a part of my work at <a href="https://www.datakind.org/2023/09/12/tackling-big-questions-on-climate-and-gender-datakind-partners-with-international-monetary-fund-on-virtual-datadive-event"/>Datakind's DataDive® event</a>, which took place from September 14 to September 17, 2023. The event was a collaboration with the International Monetary Fund (IMF) and focused on critical climate and gender-related challenges. As a member of the Global Buildings Census project team, I contributed by developing a predictive model for classifying building structure types, which I share here. This model contributes to creating a mapping layer that helps assess climate-related risks in built-up areas.



## Setup

Install necessary packages using the following commands:
   ```bash
   pip install osmium
   pip install geopandas
   pip install graphviz
   pip install jenkspy
```

## How to Use

By using the provided processing notebook, you can preprocess OSM data in a way that is compatible with the model.

Here's a general overview of the process:

- Preprocess OSM data using the provided notebook 'osm_data_processing.ipynb' to be used as test data.
- Combine the OSM data with ground truth data from official sources for labeling using the 'osm_plus_official_data_processing.ipynb' notebook. This step can be used to generate data for either training or evaluating the model.
- Train the model using the data from step 2 and test it on the preprocessed test data. Feel free to explore the results and adapt the model to your specific use case.

### Model Evaluation
The model was trained using Fairfax County data and tested on preprocessed data from the City of Boulder, providing insights into its predictive capabilities.


<p align="center"> 
 <smaller> <i>Figure 1. confusion matrix</i></smaller>
</p>
<p align="center">
  <img src="https://github.com/hadis-raad/imf_datadive_climate/blob/main/images/Boulder_confusion_matrix.png" alt="axis of movement" width="450" />

</p>

|              | Precision | Recall  | F1-Score | Support |
|--------------|-----------|---------|----------|---------|
| Residential  | 0.89      | 0.58    | 0.70     | 2384    |
| Non-Residential | 0.95      | 0.99    | 0.97     | 20691   |
| Accuracy     |           |         | 0.95     | 23075   |
| Macro Avg    | 0.92      | 0.79    | 0.84     | 23075   |
| Weighted Avg | 0.95      | 0.95    | 0.94     | 23075   |


The provided confusion matrix showcases the model's strong performance in predicting building structure types. It achieves an accuracy of 95%, indicating a high level of correctness in its predictions. Specifically, the model excels in identifying residential buildings with a 99% recall rate, making it a reliable choice for risk management decisions. Additionally, it maintains a balanced precision and recall, reflected in an F1-Score of 0.97. This equilibrium between precision and recall minimizes false positives and false negatives, further underscoring the model's effectiveness.

<p align="center"> 
 <smaller> <i>Figure 2. AUC Curve </i></smaller>
</p>
<p align="center">
  <img src="https://github.com/hadis-raad/imf_datadive_climate/blob/main/images/Boulder_AUC.png" alt="axis of movement" width="450" />
</p>

The Area Under the Receiver Operating Characteristic Curve (AUC) of 97% is a testament to the model's performance in binary classification. This high AUC signifies its outstanding discriminative power, near-perfect separation between classes, and strong predictive abilities. The model's well-calibrated probabilities and robustness make it suitable for a wide range of applications, reinforcing its value in geospatial analysis and beyond.


