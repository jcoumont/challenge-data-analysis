# Challenge data analysis
- Duration: `3 days`
- Deadline: `7/12/2020 13:30`
- Team challenge : 3
## Contributors
- [Jérôme Coumont](https://githib.com/jcoumont)
- [Ousmane Diop](https://githib.com/Nooreyni)
- [Guillaume Gémis](https://githib.com/guigem)

## Summary
Our goal is to clean and do a complete analysis and interpretation of the dataset.

#### The Mission
The real estate company "ImmoEliza" wants to establish itself as the biggest one in all of Belglium. To pursue this goal, it needs to create a machine learning model to predict prices on Belgium's sales. That way, they can pick out the properties that are the most valuable to them.

But for this, it needs to do a preliminary analysis to gather some information. Having no in-house data scientist, they are looking for talented people to do it for them.

Since your last encounter with them went great, they reached out to you to do this job. Everything is in your hands now!

Take the dataset previously scraped to do the analysis. *(If you were in different groups, decide together which dataset you are going to use.)*

#### Objectives
- Be able to use `pandas`.
- Be able to use Data visualisation libraries.(`matplotlib` or `seaborn`)
- Be able to clean a dataset for analysis
- Be able to establish conclusions about a dataset.
- Be able to find and answer creative questions about data
- Be able to think outside the box

## The dataset
The initial dataset scraped during the previous challenge contains 10.006 entries.

After a first cleaning we identified a serious problem : *Some province have less than 10 entries*
So we decided to increase the initial dataset with a new version of the scraping tool.
Rather than use the "whole belgian result pages" we splitted the scaping by "whole province result pages".

This small change allows us to bypass the result page limitation sets by default to 333 pages of 30 results (+/- 10 .000 different entries). After a new scraping run the dataset contains not less than **53.730 real estates entries**.

The shape is (53.730, 18)

#### Structure
[Acces to the dataset](data/immoweb_scrapped_2.csv) 
 0   locality             int     zip code  
 1   type_of_property     str     type of property (house/appartment) 
 2   subtype_of_property  str     subtype of property (villa/studio/mansion/loft/...) 
 3   price                int     price
 4   type_of_sale         str     type of sale 
 5   nr_of_rooms          int     number of room
 6   area                 int     area in m2
 7   equiped_kitchen      str     type of kitchen 
 8   furnished            bool    is furnished? 
 9   open_fire            bool    has an open fire?   
 10  terrace              bool    has a terrace? 
 11  terrace_area         int     terrace area in m2 if existing
 12  garden               bool    has garden? 
 13  garden_area          int     garden area in m2 if existing
 14  total_land_area      int     total land area in m2
 15  nr_of_facades        int     number of facades
 16  swimming_pool        bool    has a swimming pool?
 17  building_condition   str     state of the building (new/good/to be renovated/ ...) 
 
#### Data cleaning
This phase is very important to process the analysis phase.
So we identified our goals and the data's needed to reach them.

We need to be able to give the price by cities/provinces/regions.
This price can be expressed in term of global price or price/m2.
And we have also to identify which parameters can influence it.

##### Data quality
 0   locality             53730 non-null  100%
 1   type_of_property     53730 non-null  100%
 2   subtype_of_property  53730 non-null  100%
 3   price                50400 non-null   94%
 4   type_of_sale         53730 non-null  100%
 5   nr_of_rooms          50569 non-null   94%
 6   area                 42463 non-null   79%
 7   equiped_kitchen      33156 non-null   62%
 8   furnished            26978 non-null   50%
 9   open_fire            53730 non-null   100%
 10  terrace              28758 non-null   54%
 11  terrace_area         17376 non-null   32%
 12  garden               14340 non-null   27%
 13  garden_area           8129 non-null   15%
 14  total_land_area      28377 non-null   53%
 15  nr_of_facades        35474 non-null   66%
 16  swimming_pool        21580 non-null   40%
 17  building_condition   35860 non-null   67%

On the global dataset, we only have 904 rows with all informations filled.
So we have to process some correction and cleaning to achieve our goals.

##### Raw data cleaning
In this first step, we have removed :
- duplicated entries (no data found :-))
- blank space at the start and the end of string values
- price error (1€)
- area error (1m2)

##### Empty value cleaning
Due the important missing information in the whole dataset, we decided to refine these missing values by:
* Removing rows that have one of these conditions :
- empty price
- empty number of rooms
- empty area
* Filling some missing values :
- equiped_kitchen : UKN 
- furnished : False
- terrace : False
- terrace_area : -1
- garden : True if total_land_area > area + terrace_area
- garden_area : total_land_area - area - terrace_area
- total land area : area + terrace_area + garden_area
- swimming_pool : False
- nr_of_facades : -1
- building_condition : UKN

##### Adding useful information
To allow us to explore more efficiently the raw data, we added some columns:
- kitchen - bool : True if equiped_kitchen != 'UNK','NOT_INSTALLED', 'USA_UNINSTALLED'
- region - str : based on zip code
- province - str : based on zip code
- sq_m_price - float : price / area
- sq_m_land_price - float : price / total_land_area

##### Data conversion
To be able to have a good correlation map, we converted all non numeric data to numeric data.
- bool : int (0 or 1)
- str : int (based on dictionnary of string)
And rounded float values to 2 decimals

##### Removing non relevant columns
After a first analysis we identified few columns without any added value and removed them from the dataset :
- type_of_sale : Only 'FOR_SALE'
- furnished : less than 50% of filled value and most of them are False



## Usage
- Usage

## Installation
- Installation
- What, Why, When, How, Who.
## To do's
- Pending things to do
