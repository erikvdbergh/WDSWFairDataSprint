# Linked data Part 2: Food Fraud data

## Introduction

In this part we will use some actual data of food fraud to train with the possibilities of linked data. First download the data file [here](rasff_processed_adulteration_fraud.csv). Have a look at the file (using a spreadsheet program), you will find the following columns:

|Column name| Description|
|---|---|
|Reference|	Unique identifier for each fraud reported|
|DistributionStatus|	Countries that are distribution centers of food products|
|wdDistributionStatusCountryCode|	Country code of Distribution Status as in wikidata|
|CountryOrigin|	Country from where the product originates from|
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

1.	Create a repository for Food Fraud data: http://graphdb.ontotext.com/documentation/free/quick-start-guide.html#create-a-repository
In short, go to your local instance (often accessible via http://localhost:7200). Click on setup on the left -> then on repositories -> Create new repository -> Give it a name and leave the rest as default.
Once created, go to setup -> repositories -> connect to your created repository if you not already did that.
2.	Enable Autocompletion. This is an autocomplete feature that will help searching for variable names.
       Left panel of GraphDB click on Setup -> Autocomplete -> Switch the button to "on"
3.	Load your data [from your downloaded file](rasff_processed_aulteration_fraud.csv).
Country codes specific for wikidata are within this csv file.
To load your data: Import -> Tabular (OntoRefine) -> Create Project -> Get data from: This computer and load the CSV file.
4.	In several columns there are dates. We can update these columns using “Edit cells -> Common transforms -> to date”. What happens? Why?
5.	Now we will generate an RDF of linked data. Click on the “RDF” button at the top right of the screen. A new screen appears.
6.	Explore all different queries that exist in this screen.
7.	At the top right, select “Data -> Generate CONSTRUCT” and press “Run” (bottom left). What do you see represented in the window that appears below?
8.	Press the “Data” button on the top left again, and select “Open in main SPARQL editor”. Perform the next assignment in the new window that appears.
9.	Now we will link our data with URI from wikidata (https://www.wikidata.org/wiki/) using BIND statements. First, insert these below the lines starting with PREFIX so that the top of your query looks as follows:

```
PREFIX mydata: <http://example.com/resource/>
PREFIX spif: <http://spinrdf.org/spif#>
PREFIX wd: <http://www.wikidata.org/wiki>
```

Next, edit the only the first line that reads
```
mydata:wdCountryOriginCountryCode ?wdCountryOriginCountryCode
```
By adding IRI, so that it reads
```
mydata:wdCountryOriginCountryCode ?wdCountryOriginCountryCodeIRI
```
Last, add a line below the existing BIND statement so that the two statements read as follows:
```
BIND(IRI(spif:buildString("http://example.com/resource/{?1}", ENCODE_FOR_URI(?Reference))) AS ?myRowId)
BIND(IRI(spif:buildString("http://www.wikidata.org/entity/{?1}", ENCODE_FOR_URI(?wdNotificationFromCountryCode))) AS ?wdNotificationFromCountryCodeIRI
```
Test your constructed query by pressing “Run”. Especially check the wdNotificationFromCountryCodeIRI field. What has happened?
10.	If everything was correct, insert these data into the project: replace the CONSTRUCT word in the query editor with an INSERT tag and remove the LIMIT 100 at the bottom of this query. Then press RUN. Your statements are inserted.

