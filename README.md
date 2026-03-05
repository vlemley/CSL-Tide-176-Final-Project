# The Effect of Tide Height on Branded California Sea Lion Abundance at Ano Nuevo Island 

##Background

This project is looking at how tide heights impact the number of branded sea lions on Ano Nuevo Island. While Ano Nuevo is famous for its elphant seal, the island about a mile off of the coast is an important haul out zone for California Sea Lions (CSL). CSL can be at sea for weeks but heavily realy on haul outs to rest, molt, regulate body temperature. Their insulating fur is maintiend by oils in the skin and the most effective way for them to maintain their coat is by thuroughly drying off. This is most effectivley acomplished on dry land. 

Large amounts of dry land are most accessable during low tide. Not only is it less energetically expensive for CSL to jump from the water to the land during low tide, but it also exposes more viable land for them to occupy. A greater amount of available space allows room for larger groups of animals to gather and reduces competition. 

While this study is specifically looking at branded CSL, we hope that the relationship that this study establishes can be more widley applicable to all CSL. The observed individuals are branded by NOAA and are part of the West Coast Pinniped Branding program. They are captured, branded, released, and ideally never handeled by humans again. The idea of permanent branding is that it is a one time event that will not alter their permanent behavior. That being said, the branded CSL individuals should be a representative subset of how CSL would react to tide height. Analying this relationship will hopefully provide insight on the severity of the impact of tide height on CSL abundance. Ano Nuevo is an ideal location for this question because it has a well monitored popualtion of CSL and also has a dedicated NOAA tide site. 


## Data Collection
 
More information on the different data types used is below:

Number of Branded Sea Lions: This data is based off of drone imagrey taken on Ano Nuevo Island. As part of a long-term monitoring project, aerial surveys of the California Sea Lion populations on Ano Nuevo Island are taken 1-4 times a month (largley dependent on weather conditions). In 2025, surveys were conducted from May-August. Each survey contains around 100 images that capture a birds eye view of the entire island. Violet worked with Ano Nuevo last summer and manually went through the images for branded CSL. The date of the survey and the number of observed branded individual was recorded on a spreadsheet (Backup Copy DO-NOT-EDIT Zc_Data Entry RAW_2025_V1.0). This is the spreadshset that we started with for this project. 

Tide Height: We used NOAA tide charts from the Ano Nuevo Island monitoring location. We extracted the low and high tides for each day from May-August 2025 onto a seperate spreadsheet (127 Final Tides.csv). 

## Project Set Up

Branded CSL:

1. We first had to extract the relevant infromation from the number of branded CSL raw data. We used the date of the survey and number of individual observations of branded sea lions per date.

2. We also needed the time of each survey. This information was embeded in the photos in each survey and was extracted manually. 

3. The date, time, and number of observed individuals per survey were compilled into a spreadsheet called 176 Final Project Surveys.csv.


Tides:

1) Low and high tide and time data from May-August 2025 was extracted from the NOAA tides website.

2) Filtered all of the dates to only contain the days that surveys were conducted.

3) Calculated the slope (tide height changed/time) for each day to find the exact tide height at the time of the survey. We assumed linear tide changes and this formula was applied to every date that a survey was conducted. 


## File Information (file, whats in it, units, how it was modified, columns)

Backup Copy DO-NOT-EDIT Zc_Data Entry RAW_2025_V1.0.csv: Raw data file of survey date and number of observed branded CSL individuals

127 Final Tides.csv: Extracted NOAA tide data from 05/01/2025-09/01/2025






