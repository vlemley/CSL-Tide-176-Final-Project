# The Effect of Tide Height on Branded California Sea Lion Abundance at Ano Nuevo Island 
## Contributors

### Veronika Watkins
Email: vwatkins@ucsc.edu

### Piper Miller
Email: pianmill@ucsc.edu

### Violet Lemley
Email: vlemley@ucsc.edu

# SHARING/ACCESS INFORMATION

All data is publically available through Ano Nuevo Natural Reserve, NOAA Tide Charts, and UC Nature DENDRA websites.

Date of Data Collection: 2025-05-01 to 2025-08-31

Geographic Location of Data Collection: Ano Nuevo Island, Pescadero CA

# DATA & FILE OVERVIEW

This entire project is in folder CSL-Tide-176-Final-Project. It contains:

data

output

README.md

CSL176Final.qmd

CSL176Final.Rproj

## File List

### data: Contains three raw csv files:


SolarRadiation.csv (imported from UC Nature DENDRA)

surveys.csv (manually compiled from UC Natural Reserves UAS Surveys)

tides.csv (imported from NOAA Tides)

### output: Contains two types of information:


**Scatterplot (saved as png in folder Scatterplots)**


radiation.plot.png

tide.plot.png

**Models (relevantly labled in output folder)**

m.CSL.Tide.rds

m.CSL.Tide2.rds

m.CSL.Solar.rds

m.CSL.Solar.Tide.Additive.rds


# METHODOLOGICAL INFORMATION

## Data Collection/Generation 

**CSL Count**: This data is based off of drone imagrey taken on Ano Nuevo Island. As part of a long-term monitoring project, aerial surveys of the California Sea Lion populations on Ano Nuevo Island are taken 1-4 times a month (largley dependent on weather conditions). In 2025, surveys were conducted from May-August. Each survey contains around 100 images that capture a birds eye view 30 feet above the entire island. Violet worked with Ano Nuevo last summer and manually went through the images, recording the number of branded CSL. The date of the survey, the number of observed branded individuals, and the embeded time from each photograph was recorded.

**Tide Height**: We used [NOAA tide charts]([url](https://tidesandcurrents.noaa.gov/noaatidepredictions.html?id=9413878)) from the Ano Nuevo Island monitoring location. We extracted the low and high tides for each day from May-August 2025. 

**Solar Radiation**: We used data from the [UC Nature DENDRA station at Ano Nuevo]([url](https://dendra.science/orgs/ucnrs/datastreams?faceted=true&scheme=dq&selectStationId=630ffc7fbcd7f8d98fe03a37)). It collects a wide variety of meteorelogical data every 10 minutes and we extracted the average solar radiation levels from May-August 2025.


## Data Processing Methods 

We included all of the raw data in our data file. The following is how we manipulated it to use in our study. The data in parenthesis is the result of these manipulations:

**CSL Count**: Combined date and time into DateTime column (survey_CSL). 

**Tide Height**: The imported file included two high and two low tides for every day in our selected time frame. We created a vector of our survey dates to only include relevant tide information (survey_tides). We also applied a linear aproximation formaula to estimate the tide height at the time of survey. Combined date and time into DateTime column to combine CSL count and Tide Height data (survey_table_complete)

**Solar Radiation**: The imported file included average solar radiation every 10 minutes in our selected time frame. We used the same survey date vector so the data only included relvant days (survey_solar). Because the times in the solar radiaiton data were rounded, we merged all three data sets together by date, not time. This involved us seperating date and time in (survey_table_complete) and (survey_solar) and then recombining them into (merged_complete). 


## Software Information 

All analysis done in **R version 4.5.2 (2025-10-31)**

Packages:
library(here)
library(brms)
library(hms)
library(tidyverse)
library(ggplot2) 
library(ggeffects)
library(dplyr)
library(lubridate)

# DATA-SPECIFIC INFORMATION (RAW DATA)

## surveys.csv

Number of variables: 3

Number of rows: 14

### Variable list:

#### Date

Description: Date of tide observation

Units: YYY-MM-DD


#### Time

Description: Time of tide height measurement

Units: HH:MM:SS

#### Observed

Description: Number of branded CSL individuals observed during the survey

Units: count


### Specialzied formats

CSL: california sea lion

Count is the number of observed individuals during each survey


## Solar Radiation.csv

Number of variables: 2

Number of rows: 17,712

### Variable list:

#### Time

Description: Date and time when solar radiation was recorded

Units: YYYY-MM-DD HH:MM:SS

#### Ano Nuevo Total Solar Radiation Avg

Description: Average Solar Radiation recorded at Ano Nuevo every

Units: Watts per square meter (W/m^2)

### Specialzied formats

Measurements are recorded at 10-minute intervals

W/m^2: watts per square meter


## tides.csv

Number of variables: 5

Number of rows: 947

### Variable list:

#### Date

Description: Date of tide observation

Units: YYY-MM-DD

#### Day

Description: Day of the week

#### Time

Description: Time of tide height measurement

Units: HH:MM:SS

#### Pred

Description: Predicted tide height

Units: meters

#### High/Low

Description: Indicates wheater tide is high or low

Units: H=high tide, L=low tide

### Specialzied formats

Tide heights are predicted values, not direct measurements

H: high tide

L: low tide

# DATA-SPECIFIC INFORMATION (PROCESSED DATA)
This is information on the most relevant processed data tables.





## Background

This project is looking at how tide heights impact the number of branded sea lions on Ano Nuevo Island. While Ano Nuevo is famous for its elphant seal, the island about a mile off of the coast is an important haul out zone for California Sea Lions (CSL). CSL can be at sea for weeks but heavily realy on haul outs to rest, molt, regulate body temperature. Their insulating fur is maintiend by oils in the skin and the most effective way for them to maintain their coat is by thuroughly drying off. This is most effectivley acomplished on dry land. 

The first variable that we decided to look at was tide height. Not only is it less energetically expensive for CSL to jump from the water to the land during low tide, but it also exposes more viable land for them to occupy. Large amounts of dry land are most accessable during low tide and a greater amount of available space allows room for larger groups of animals to gather and reduces competition. 

The second variable we looked at was solar radiaiton levels. Because sea lions rely on haul outs to dry their fur and solar radiation can contribute to drying rate, we wanted to see how solar radiation levels impacted the abundnace of branded inviduals. Our assumption is that there would be more individuals when the solar radiation levels are higher. 

While this study is specifically looking at branded CSL, we hope that the relationship that this study establishes can be more widley applicable to all CSL. The observed individuals are branded by NOAA and are part of the West Coast Pinniped Branding program. They are captured, branded, released, and ideally never handeled by humans again. The idea of permanent branding is that it is a one time event that will not alter their permanent behavior. That being said, the branded CSL individuals should be a representative subset of how CSL would react to tide height. Analying this relationship will hopefully provide insight on the severity of the impact of tide height on CSL abundance. Ano Nuevo is an ideal location for this question because it has a well monitored popualtion of CSL and also has a dedicated NOAA tide site. 

Our main question was: **How do tide height and solar radiation levels impact abundance of branded CSL on Ano Nuevo Island?** The target audience for this study are people who are doing CSL research and want to consider how environmental factors could be impacting the number of observed individuals. Obviously we are only looking at two envirnoemental factors but this methodology (using branded individuals as a subset of the total population) could be applied to other factors to get a sense of how they impact population data. 




