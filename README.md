# Agenda:

Under the Chicago Energy Benchmarking Ordinance, the City reports annually on energy findings and trends, and the ordinance authorizes the City to share building-specific data with the public. Energy benchmarking continues to provide the foundation for increasing energy aptitude, saving energy, reducing utility costs, and supporting clean energy jobs throughout the City.

To support the efforts of the city, We are building a model that predicts the Energy Rating for the building based on its usage over the years 2018-20 based on various parameters which might help the goverments to plan the budgets for energy rebates and take measures to ensure poorely performing stakeholders perform better in future. 


Data Source :

https://data.cityofchicago.org/Environment-Sustainable-Development/Chicago-Energy-Benchmarking/xq83-jr8c/data

Feature description :

- Data Year: Reporting Year
- ID: Indetifier to uniquily indenfy the property
- Property Name: Property Name       
- Reporting Status: Reporting Status (Whether the property reporting it's energy usage to authorities or not)                            
- Address: Address of the Property                                      
- ZIP Code: ZIP Code of the Property                                    
- Chicago Energy Rating: 0-4 Rating                       
- Exempt From Chicago Energy Rating: Whether the property taken exemption in reporting the energy usage           
- Community Area: Community Area where the property located                              
- Primary Property Type: Property Catagory                       
- Gross Floor Area - Buildings (sq ft): Total Are in SqFt    
- Year Built : Year in which construction was completed                                  
- #of Buildings: Number of buildings in the property
- Water Use (kGal): Water usage in kGal
- ENERGY STAR Score: 0-100        
- Electricity Use (kBtu): Electricity Utilization                   
- Natural Gas Use (kBtu): Natural Gas Utilization  
- District Steam Use (kBtu): District Steam Use (kBtu)                
- District Chilled Water Use (kBtu): District Chilled Water Use (kBtu)          
- All Other Fuel Use (kBtu): All Other Fuel Use (kBtu)                  
- Site EUI (kBtu/sq ft): Site EUI (kBtu/sq ft)                       
- Source EUI (kBtu/sq ft): Source EUI (kBtu/sq ft)                     
- Weather Normalized Site EUI (kBtu/sq ft): Weather Normalized Site EUI (kBtu/sq ft)    
- Weather Normalized Source EUI (kBtu/sq ft): Weather Normalized Source EUI (kBtu/sq ft)  
- Total GHG Emissions (Metric Tons CO2e) : Total GHG Emissions (Metric Tons CO2e)      
- GHG Intensity (kg CO2e/sq ft): GHG Intensity (kg CO2e/sq ft)               
- Latitude: Latitude                                    
- Longitude: Longitude                                   
- Location: (Latitude, Longitude)                                    
- Row_ID: Row_ID


# Exploratory Data Analysis

The report analysis depicts that :
The dataframe has 17728  rows and each row represents a housing project.
The dataframe has 30 features(columns).
info() method hepls in knowing the quick description about the dataframe.


# Data Cleaning and Feature Engineering

EDA Observations:

- Renaming the below columns for readability

1) 'Data Year': 'Year'
     
2) '# of Buildings': 'NumberOfBuildings'
    
3) 'Chicago Energy Rating': 'CERating'

- Dropping below columns as they contain less values or after careful observation and research I thought, they have no value in yeilding the target varaible through model.


'Property Name', 'Address', 'ZIP Code', 'Water Use (kGal)'

'District Steam Use (kBtu)', 'District Chilled Water Use (kBtu)'

'All Other Fuel Use (kBtu)', 'Site EUI (kBtu/sq ft)'

'Source EUI (kBtu/sq ft)', 'Weather Normalized Site EUI (kBtu/sq ft)'

'Weather Normalized Source EUI (kBtu/sq ft)', 'Location', 'Row_ID', 'Latitude', 'Longitude' 

- Changing the column 'Exempt From Chicago Energy Rating' type as boolean but not executing this statement as boolean values are generating errors while generating Correlation Matrix

- A significant of properties reported their Energy usages for Years 2018, 19 and 20. Hence, Considering the data for the years 2018, 19 and 20.

- Some of the properties have Exempt From Chicago Energy Rating status as True not reported Energy usage as they either claim 'Not eligible' or 'Not Submitted'. We may remove them in future while training the model.

- According the Energy Rating Distibution below is the energy scores breakdown for each year ,

1) In 2018, Highest number of Properties are reported between 2-4

2) In 2019, The trend has been dropped as many number of properties have either not reported or not efficiently utilized energy.

3) In 2020, The trend came back to normal with increasing participation from the stakeholders.

Note: 
    
    0 - Not Efficient Energy Consumer/Not Reported
    4 - Effiicient Energy Consumer
 
 - According to the correlation the following are being considered,

1) As 'Total GHG Emissions (Metric Tons CO2e)' and 'Electricity Usage (kBtu)' are correlated about 94%, We may consider removing 'Total GHG Emissions (Metric Tons CO2e)' as they both carry almost same information. 

2) As 'CERating' and 'ENERGY START Score' are correlated about 91%, We may consider removing 'CERating' as they both carry almost same information. Moreover, According to changed Chicago Energy Benchmarking Rules properties started reporting in the format 0-4 instead of 0-100.

3) As 'Gross Floor Area - Buildings (sq ft)' and 'Electricity Use (kBtu)' are correlated about 75%, We might consider removing 'Electricity Use (kBtu)' as they both carry almost same information.

4) As 'Gross Floor Area - Buildings (sq ft)' and 'Total GHG Emissions (Metric Tons CO2e)' are correlated about 73%, We might consider removing 'Total GHG Emissions (Metric Tons CO2e)' as they both carry almost same information.



**Feature Engineering:**


1) Imputed Null values in Numerical Features with median values.
2) Imputed Null values in Categorical Features with Most Frequently listed Item
3) As the classes are imbalanced, class_weight parameter configured as 'balanced' to help the model in assigning relavant weights.
**
Final Feature Set:**

**Target:**
     ERating
**
Features:**
     CommunityArea
     PrimaryPropertyType
     GrossFloorArea
     NumberOfBuildings
     ElectricityUse
     NaturalGasUse
     SiteEUI
     WeatherNormSiteEUI
     GHGIntensity


Training examples: 10,293
Test examples: 2,574
**Modeling:
Logistic Regression - Grid Search:**

1) Proceeded for logistic regression with C Values:0.01, 0.1, 1, 10, 100
1) Proceeding to Secondary Grid Search around the C Value(100) received from Primary Grid Search to compare model performance.
2) The GridSearch returned the same C Values even if tried Changing Hyper Parameter Value(C) range with in the vicinity of 100. Hence sticking with the C = 100 for linear regression.
3) The Precision, ReCall and F1-Score indicates no significant improvement over previous run as the C Value remain the same.
4) The ROC Curves and AUC Suggests, Model Performance is better for both Class 'A' & 'C' as the model has 90% chance that it will be able to distinguish between positive class and negative class compared to the Class 'B'(67%).
5) With Average AUC Score of 82% Model performed considerably well.


**Decision Tree - GridSearch**

1) Proceeded for model with hypermeteres: 'model__max_depth': [1, 3, 6, 9, 13, 15], 'model__min_samples_split' : [0.1, 0.2, 0.5, 0.7]
2) Proceeding to Secondary Grid Search to see if it can propose better hyperparameters.
3) The Recall and F1-Scores for Class 'B' has been considerably improved while remaining combinations show significant improvements.
4) Recall Macro Avg Accuracy of the model also improved from 59% to 66%.
5) Hence fixating on below hyperparameters this model for future reference. max_depth=16, min_samples_split=0.01
6) Above ROC Curves and AUC Suggests, Model Performance is better for both Class 'A' & 'C' as model has 90% chance that it will be able to distinguish between positive class and negative class compared to the Class 'B' (76%).
7) With Averga AUC Score of 85% Decision Tree Model relatively out-performed Logistic Regression.

**Gradient Boosting Classifier - GridSearch**

1) Proceeded for model with hypermeteres: 'gb__max_depth': [1, 2, 3], 'gb__n_estimators': [50, 100, 200]
2) The Precsion, Recall and F1-Scores for all the classes seen significant improvement.
3) Recall Macro Avg Accuracy of the model also improved from 68% to 70%.
4) Hence fixating on below hyperparameter and this model for future reference. 
   n_estimators=400
5) Above ROC Curves and AUC Suggests, Model Performance is better for both Class 'A' & 'C' as model has 94% chance that it will be able to distinguish between positive    class and negative class compared to the Class 'B' (81%).
6) With Averga AUC Score of 90% Gradient Booting Classifier Model relatively out-performed Logistic Regression & Decision Tree.

**Conclusion:**

We can choose Gradient Boosting Classifier model to generalize the population for following reasons. 

1) The Recall Macro Avg Score has been 70% compared to 63% and 66% of logistic regression and Decision Tree Respectively.
2) Precision, Recall & F1-Scores are better than both logistic regression and Decision Tree.
3) Model Accuracy has been 75% which is relatively better in Comparision.
