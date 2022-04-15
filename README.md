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

2) As 'CERating' and 'ENERGY START Score' are correlated about 91%, We may consider removing 'ENERGY START Score' as they both carry almost same information. Moreover, According to changed Chicago Energy Benchmarking Rules properties started reporting in the format 0-4 instead of 0-100.

3) As 'Gross Floor Area - Buildings (sq ft)' and 'Electricity Use (kBtu)' are correlated about 75%, We might consider removing 'Electricity Use (kBtu)' as they both carry almost same information.

4) As 'Gross Floor Area - Buildings (sq ft)' and 'Total GHG Emissions (Metric Tons CO2e)' are correlated about 73%, We might consider removing 'Total GHG Emissions (Metric Tons CO2e)' as they both carry almost same information.

- From above graphs, It is eveident that the partcipation of stakeholders is explonentially growing by each year.









