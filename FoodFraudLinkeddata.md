# Linked data Part 2: Food Fraud data

## Introduction

In this part we will use some actual data of food fraud to train with the possibilities of linked data. First download the data file [here](rasff_processed_adulteration_fraud.csv). Have a look at the file (using a spreadsheet program), you will find the following columns:

|Column name| Description|
|---|---|
|Reference|	Unique identifier for each fraud reported|
|DistributionStatus|	Countries that are distribution centers of food products|
|wdDistributionStatusCountryCode|	Country code of Distribution Status as in wikidata|
|CountryOrigin|	Crountry from where the product originates from|
|wdCountryOriginCountryCode|	Country code of Country Origin as in wikidata|
|NotificationFrom|	Crountries that raise alarm for actual food  fraud|
|wdNotificationFromCountryCode|	Country code of NotificationFrom as found in wikidata|
|DataOfCase|	Date when this incident was notified|
|LastUpdate|	Date when it this incident was updated|
|Classification|	Type of Notification (Border Rejection, Alert.etc)|
|ActionTaken|	What action was taken by the authorities|
|Product|	Type of food product (peppers, chilli powder etc)|
|ProductCategory|	Category of food (meat or vegetables)|
|RiskDecision|	Type of Risks (serious, not serious etc)|
|HazardSubstance|	Chemical substance that was found|
|HazardAnalyticalResult|	The level of this chemical substance if its acceptable or not.|
|HazardUnits|	Units of measurement for this chemical substance|
|HazardSamplingDate|	Date when this product was sampled|
|Subject.Description|	Additional information about this incidence|
