# certifications
A collection of my professional certifications

## Web Scraping

We use the R package 'rvest' to scrape the COVID-19 hiring data from the following sources:
1. Hiring2020 GitHub repository: https://github.com/gcreddy42/hiring2020
2. Startups Actively Hiring During COVID-19: https://docs.google.com/spreadsheets/u/1/d/15vTgoKSDjOsyvyh_MMHyPN1kUBdkUlZFV_mQCmfF89Y/htmlview?fbclid=IwAR2CtoiX6RiYk_u0KNndiW4hR5DblB2argc-znX5rJxGszE04SLbtbxBd6o&lor=0&utm_source=mass_mailer&utm_medium=email&utm_content=579575&utm_campaign=uni_targeted_emails#

In addition, since Hiring2020 does not contain an 'Industry' column, we further scrape corresponding industries for the companies from Crunchbase.com. However, Crunchbase blocks direct scraping attempts, which is why we use a scraping software called Octoparse instead. The reason we chose Octoparse is that it contains a premade scraping script for Crunchbase, simplifying our job. 

Lastly, since some companies are missing from the Crunchbase database, we navigate to LinkedIn.com to manually find the industry data for those. 

After the web scraping, we end up with the following columns for our two data tables:
1. _hiring_data_: "Company", "Country", "Job_Type", "Position", "Industry", "URL"
2. _startup_data_: "Company Name", "Company Website", "Sector Classification", "Brief Company Description", "HQ Location" + 49 more columns (mostly in non-tidy format and will be cleaned/removed later on).

## Data Cleaning

The major changes made to the _hiring_data_ table during the cleaning stage are:
* Removing the 'Country' column
* Removing non-descriptive words from the 'Job_Type' column
* Removing non-descriptive words from the 'Position' column.

As for _startup_data_, we make the following adjustments:
* Removing all empty rows/columns
* Setting the correct header row
* Reindexing the rows
* Adding a proper column for Job Type
* Converting columns 4-45 to tidy format
* Filtering out positions that are no longer open
* Reordering the columns to match those of hiring_data.

The next step is to merge the two datasets. The resulting dataset, also called _hiring_data_, contains 3,967 observations across 5 columns: "Company", "Job_Type", "Position", "Industry", "URL". 

We further add an additional column, "Function", mapping all job positions to a set of predefined job functions: 
* "Research"            
* "Engineering"         
* "Applied Science"     
* "Other"              
* "Analytics"           
* "Operations"          
* "Sales & Marketing"   
* "Product Development"
* "Design"              
* "Quant Trading"       
* "Project Management"  
* "Legal".

As such, the final dataset contains 3,967 observations across 6 columns - the aforementioned 5 plus the "Function" column. The corresponding data table can be found under this tab.



