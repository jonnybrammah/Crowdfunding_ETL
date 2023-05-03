# Crowdfunding_ETL

<p align="center">
<img src="https://www.sec.gov/files/crowdfunding-v5b-2016.jpg">
</p>

Image Taken from [sec.gov](https://www.sec.gov/securities-topics/crowdfunding).

## Project Description

The goal of this project was to practice extracting and transforming data using the python library pandas in a jupyter notebook ([ETL_Mini_Project_Team_1.ipynb](https://github.com/jonnybrammah/Crowdfunding_ETL/blob/main/ETL_Mini_Project_Team_1.ipynb)) and then loading that information into a SQL database ([SQL Data Schemas](https://github.com/jonnybrammah/Crowdfunding_ETL/blob/main/SQL%20Data%20Schemas)).

-----

### Extracting and Transforming Data

Crowdfunding data was collected from an Excel file (crowdfunding.xlsx) with the following columns:
- Crowdfunding id
- Condtact id
- Company Name
- Description
- Crowdfunding goal ($)
- Pledged donations ($)
- Outcome of the campaign
- The number of backers
- Country
- Currency
- When the campaign was launched
- The campaign deadline
- Whether this campaign was designated a "staff pick"
- Whether this campaign was "spotlighted"
- The category and subcategory of the campaign

To clean the data for eventual loading, the campaign category and subcategory had to be extracted separately and then given associated ids so they could be tracked. This was done by splitting the category/subcategory column information and then searching for unique values. 
These ids were then saved as separate csv files (categories.csv and subcategories.csv).

Other columns also had to have their data types changed to make them usable. This included changing some values from strings to numbers, and changing the dates to datetime objects rather than UTC. Once this was completed, this data was then saved as a campaign.csv file.

Finally, one last Excel file was read in (campaign.xlsl) with the contact id, name and email address of each contact stored as a string of a dictionary in each row. Two methods were used to extract this information:
1. Each row of the data was read in as a json and then the value from each key value pair was extracted. Some rudimentary data cleaning took place (like extracting first and last names from the name columns" and this was then written to another csv file (contacts.csv)
2. Information was extracted straight from the string using Regex strings. Similar data cleaning took place as in option 1, and this too was written to another csv file (contacts_option2.csv)
Only one of these csv files was needed for the next section.

-----

### Loading Data

The four csv files that we had gathered during our Extract and Transform sections were now available to us:
- campaign.csv
- categories.csv
- subcategories.csv
- contacts_option2.csv

SQL queries were written to create necessary tables in pgAdmin, including identifying the primary key and linking these together with appropriate foreign keys. The data was then The ERD for these tables is shown below:

<p align="center">
<img src="https://raw.githubusercontent.com/jonnybrammah/Crowdfunding_ETL/main/ERD.png">
</p>

