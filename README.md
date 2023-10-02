# Data-Visualization-and-Dashboards-with-Tableau

Airbnb is a global online marketplace that connects travelers with hosts offering lodging in homes, apartments, or unique accommodations. Founded in 2008, it has revolutionized the way people book and experience accommodations, providing a diverse range of options in thousands of destinations worldwide. Airbnb has become a popular choice for both travelers seeking personalized stays and hosts looking to monetize their properties.

This Tableau Visualization and Dashboards project is based on the assumption that we're being hired by Airbnb's competitor company, as an independent consultant, to provide key insights via visualization and dashboards, into the New York City rental market of Airbnb. 

## Repository Structure:

Repository Link: [Data-Visualization-and-Dashboards-with-Tableau](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau)
* [Data](Data)
* [Image](Image)
* [TableauPresentationFileOption2NumberIIIDatasetAirbnbThanhNguyen.pdf](TableauPresentationFileOption2NumberIIIDatasetAirbnbThanhNguyen.pdf)
* [airbnb_nyc_EDA.twb](airbnb_nyc_EDA.twb)
* [airbnb_nyc_dashboard.twb](airbnb_nyc_dashboard.twb)
* [README.md](README.md)
* [assignment.md](assignment.md)

## Project/Goals

The high-level goal of this is to answer the client's main consultant brief:

* Helping a competitor company of Airbnb to provide key competitive analysis and insights into Airbnb’s existing market in the New York City area - using the historical data provided.

Main project output: [TableauPresentationFileOption2NumberIIIDatasetAirbnbThanhNguyen.pdf](TableauPresentationFileOption2NumberIIIDatasetAirbnbThanhNguyen.pdf)

The main goal of the project will be translated into finding the answers to these five themed questions:

* Question 1: How are Airbnb listings distributed in NYC? (To provide a high-level view)
* Question 2: How does neighborhood (location) impact Airbnb listings in NYC? (Perform Location Analysis)
* Question 3: Which type of property is most preferred by guests in NYC Airbnb? (Perform Property Type Analysis)
* Question 4: What is the customer preference when choosing an Airbnb room in NYC? (Perform Room Type Analysis)
* Question 5: What are some characteristics among NYC’s Airbnb hosts? (Perform Host Analysis)**

These questions above do not aim to be an extensive list of exploring and defining every pattern of the data, but more focused on the key aspects of competitive business insights.

## Process
### Part 1: Context & Data Connection

This dataset is a historical dataset provided from the public database Inside Airbnb initially contains 30,478 Airbnb listings in New York City. This raw data is provided to us and has been compiled from Inside Airbnb.

Output: [airbnb_nyc.xlsx](Data/airbnb_nyc.xlsx)

* Data Dictionary of dataset:

This data dictionary provides an overview of the columns in the Airbnb New York City dataset, including their data types and brief descriptions.

| Column Name                 | Data Type          |                             Description                                     |        
|-----------------------------|--------------------|-----------------------------------------------------------------------------|
| Host Id                     | Integer            | A unique numeric identifier for each host.                                  |
| Host Since                  | Date               | The date when the host joined Airbnb, from 2008 to 2015.                    |
| Name                        | String             | The name of the property listed on Airbnb.                                  |
| Neighbourhood               | String             | The neighborhood where the property is located.                             |
| Property Type               | String             | The type or category of the property.                                       |
| Review Scores Rating (bin)  | Integer            | Binned representation of the review scores rating.                          |
| Room Type                   | String             | The type of room or space being offered.                                    |
| Zipcode                     | Integer            | The five-digit postal code/zipcode of the property's location.              |
| Beds                        | Integer            | The number of beds available in the property.                               |
| Number of Records           | Integer            | The number of records associated with each listing.                         |
| Number Of Reviews           | Integer            | The total number of reviews that this property has received.                |
| Price                       | Number (Whole)     | The price of the property for a given stay.                                 |
| Review Scores Rating        | Number (Whole)     | The numeric rating score given to the property, likely on a scale over 100. |

Note that the timeline of the records inside is not indicated, as we have only column 'Host Since' indicating the time range of 2008 - 2015. However, this is accurate to treat this date variable as the actual date of the listing.


### Part 2: EDA & Data Cleaning

This step includes: treating missing values, and duplicates, detecting outliers and data mismatch, and exploring variables, relationships, and patterns; all by visualization techniques in Tableau.

The EDA and data cleaning process is a combination of using Tableau and Excel. We'll export clean data under a new Excel file at the end of this step and prior to building the dashboards.

Output: [airbnb-nyc-clean.xlsx](Data/airbnb-nyc-clean.xlsx)

A summary of all the steps taken in this EDA & Data Cleaning stage:

* Impute missing values in ‘Host Since’ with existing data (3 rows).
* Drop rows with missing values in zipcode (134 rows). Fix funky zipcode outside of NYC (6 rows). Fix mismatching zipcode vs. neighborhood (67 rows).
* Fill in null values in ‘Property Type’ (3 rows) with the most common type: ‘Apartment’.
* Fill in null values in ‘Beds’ (84 rows) with info from other columns: Apartment: Usually 1 bed - House: Usually 1 bed - Dorm: Usually 1 bed.
* Drop the Review Scores Rating (bin) column because it doesn’t have much meaning in the dataset.
* Do not drop the rows with null values in ‘Review Scores Rating’ (there are more than 8.3K rows like that). The majority of that is due to having ‘Number of Reviews’ = 0. 
Action taken: Drop 509 over 30,478 rows for those having >= 1 number of reviews but having no review rating. Choose to keep the rest of the missing values here  as ‘Null’, and add a ‘Zero Review’ clarification column with values 1 and 0 - 1 when there is a missing value in ‘Review Scores Rating’ when Number of Reviews’ = 0 and vice versa.
* Drop all duplicates after cleaning
* Use pair plots to study the relationship between numeric variables. 
Findings: There doesn’t seem to be a linear correlation between Beds, Price, Number of Reviews, Review Scores Rating. The relationships between the numerical variables somewhat resemble the log-linear trend line.
We removed an extreme outlier from the pair plot (1 row).
* Save the clean data results to a new Excel file named [airbnb-nyc-clean.xlxs](Data/airbnb-nyc-clean.xlxs)

The clean dataset now contains 29,816 rows after the EDA & data-cleaning process. 

A detailed explanation of the process, with at least corresponding graphs, can be found in this output: 

[TableauPresentationFileOption2NumberIIIDatasetAirbnbThanhNguyen.pdf](TableauPresentationFileOption2NumberIIIDatasetAirbnbThanhNguyen.pdf)

### Part 3: Insights & Dashboard

In this part, we investigate into several key questions about Airbnb listings in New York City with key findings about the data patterns and relevant dashboards.

Output: [airbnb_nyc_dashboard.twb](airbnb_nyc_dashboard.twb)

***Question 1: How are Airbnb listings distributed in NYC?**

Key Findings: 
The dataset comprises 29,816 Airbnb listings, with 55.86% being entire homes/apartments, 41.40% private rooms, and 2.75% shared rooms. Listings are found in Manhattan, Brooklyn, Queens, and Staten Island.

![Q1 Dashboard 1](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q1%20Dashboard%201.png)

***Question 2: How does neighborhood (location) impact Airbnb listings in NYC?**

Key Findings:
Manhattan and Brooklyn, particularly the trendy Williamsburg neighborhood in Brooklyn and the Lower East Side in Manhattan (linked by a bridge), boast the highest density of Airbnb listings in NYC, offering proximity to attractions, activities, restaurants, and nightlife. Manhattan's Airbnb options are generally pricier than those in Brooklyn. Neighborhoods partially influence listing clusters and pricing, as Manhattan's limited space and high cost of living contribute to its expense.

![Q2 Dashboard 1](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q1%20Dashboard%201.png)

![Q2 Dashboard 2](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q2%20Dashboard%201.png)

***Question 3: Which type of property is most preferred by guests in NYC Airbnb?**

Key Findings:
The top 5 preferred Airbnb property types in New York City are Apartment, House, Loft, Bed & Breakfast, and Condominium. Apartments dominate all neighborhoods, but Manhattan has fewer houses due to its high cost of living and proximity to major attractions. Manhattan's popularity for lofts suggests wealthy guests seeking convenience. In contrast, Brooklyn offers more affordable options.

![Q3 Dashboard 1](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q3%20Dashboard%201.png)

![Q3 Dashboard 2](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q3%20Dashboard%202.png)

![Q3 Dashboard 3](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q3%20Dashboard%203.png)

***Question 4: What is the customer preference when choosing an Airbnb room in NYC?**

Key Findings:
Customers prefer either entire places or private rooms within the Apartment property type, depending on guest count and bed availability. Manhattan attracts those seeking more comfort and larger spaces at higher prices. Brooklyn visitors are split between entire places and private rooms, possibly due to family or solo traveler preferences. Staten Island, with fewer listings, stands out for high-priced entire places with 3-16 beds.

![Q4 Dashboard 1](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q4%20Dashboard%201.png)

![Q4 Dashboard 2](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q4%20Dashboard%202.png)

***Question 5: What are some characteristics among NYC’s Airbnb hosts?**

Key Findings:
On average, hosts in New York City have 1.24 listings, with some having up to 32. Most hosts prefer renting entire places in Manhattan. Since 2015, there's been a decline in new hosts, mainly in Manhattan and Brooklyn. In 2015, a law restricted full-apartment Airbnb rentals to 30+ days, despite over 50% of listings offering shorter stays.

The impact of the mentioned regulation on new hosts since 2015 is uncertain due to the unpredictable external environment. Historical data suggests potential recovery, assuming continued demand for vacation rentals in NYC. More data on short-term and long-term attributes would enhance forecasting.

![Q5 Dashboard 1](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q5%20Dashboard%201.png)

![Q5 Dashboard 2](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q5%20Dashboard%202.png)

![Q5 Dashboard 3](https://github.com/TeeNguyenDA/Data-Visualization-and-Dashboards-with-Tableau/blob/main/Image/Q5%20Dashboard%203.png)

## Challenges 

* Limited time for conducting EDA, data cleaning, outlier detection, and visualization.
* The dataset lacks a clear timeline, except for 'Host Since' data, making it challenging to pinpoint its specific time range. Assuming it covers only the 2008-2015 period may not be entirely accurate.
* Additional time would be valuable for exploring intriguing aspects beyond this project's scope, like examining the relationship between Review Scores and other variables.
* If accessible, it could be beneficial to obtain more insights into the dataset's short-term and long-term rental characteristics.

## Future Goals

* Explore external sources or metadata to narrow down the dataset's timeline and establish a more accurate temporal context.
* Allocate dedicated time for in-depth analysis of Review Scores and their correlations with various factors, potentially uncovering valuable insights.
* Seek out or collect supplementary data on short-term and long-term rental dynamics to enhance the dataset's comprehensiveness for future analyses.
