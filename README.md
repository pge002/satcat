# satcat

"Satcat" is a project to visualise satellite payloads and historical space launch data.

Satellite payload and launch information is taken from two sources :

1.  Celestrak SATCAT Database - timestamped catalogue of all objects in space large enough to tracked from earth going back to the first launch in 1957. All entries are logged against unique NORAD identifier and contain date, orbit and basic country of origin information.<br>

2.  UCS (Union Of Concerned Scientists) Database - detailed listing of satellites currently orbiting earth including ownership, application and orbit.

3. Webscrapes of factual satellite information taken from satellite operator websites, satbeams and wiki (refer Part 1 Description for further details).

SATCAT data is read directly from the source URL into Mysql database. (to read directly from textfile instead use funtion given in the code section).
<br>

## notebook
Juypter Notebook imports the data and creates a collection of interactive visualisations using Plotly in offline mode within the notebook (without any further setup other than importing Plotly library). 

HTML version has all the same offline interactive visualisations! so it can be viewed in a webbrower. Kindly wait for the HTML to fully load (otherwise the dropdowns and interactive features will appear not to work).

## data source : satcat

Executing the main script will create Mysql tables and populate with the SATCAT database and associated annexes taken directly from the Celestrak website.<br>

**>> satcat_main.py**

To change Mysql login details edit satcat_main.<br>
<br>
Tables are created containing :
<br>
* satcat - full copy of the SATCAT,<br>
* launchsites - annex of launch site codes and full names used by SATCAT,<br>
* satcat sources - annex of Ownership codes and full names by SATCAT<br>

After initial run, subsequent runs will append any new entries to the existing tables. All tables are included (i.e. so new Owners and Launchsite are included).

Datasource : https://celestrak.com/pub/satcat.txt<br>

## data source : UCS 
UCS Database is available off the website in Excel format and is imported using Pandas read_excel().<br

Datasource : http://www.ucsusa.org/nuclear-weapons/space-weapons/satellite-database<br>

## data source : Webscrapes
webscraped data has been inserted into Mysql as tables for each website source. 
Tables are created and populated for Intelsat, SES and satbeams <br>

Datasource : various wesbites refer to Part 1 Description
<br>
## Folders
/data  : contains latest UCS Excel file<br>
/tests : contains Unittest .py script<br>
/sql   : contains latest dump from Mysql <br>
/Webscrapes : contains notebooks used to webscrape urls and insert into Mysql
<br>
## Versions
All files have been written in Python 3.5 with the exception of :<br>

Datasource 1 Pandas read_excel **requires xlrd library**<br>

**Plotly library required** <br>
**sqlalchemy library required** <br>

## Code
**satcat_main.py** - starting point includes configuration settings for db logins, source URLs and local file paths.<br>

**SATCAT.py** - library of custom functions for collecting and parsing SATCAT data<br>

includes :<br>

**request_fromURL(url)** - Get response from website using Request libray<br>
**parse_satcat(url)** - Get SATCAT formatted CSV data from website URL and parse into dictionary format<br>
**parse_satcat_annex(url)** - Get CSV textfile from website URL and parse into dictionary format<br>
**get_URL_table(url)** - Get tables from URL and parse into dictionary format<br>
<br>
**SATCAT_SQL.py** - library of custom function for creating and inserting data into MySQL dB<br>
<br>
includes :<br>

**sql_satcat_tables_init(config)** - creates MySQL tables<br>
**sql_satcat_update_tables(config, satcat_settings)** - updates table contents <br>
**sql_execute(config, sql_execute_cmds)** - excutes sql commands<br>
**sql_insert_satcat(config, satcat)** - insert SATCAT formatted data into table<br>
**sql_insert_satcat_LaunchSites(config, LaunchSites)** - insert SATCAT LaunchSite formatted data into table<br>
**sql_insert_satcat_Owners(config, Ownership)** - insert SATCAT Owners formatted data into table<br>
<br>
**read_parse_satcat_txtfile.py** - read and parse SATCAT from text file into dataframe

**MYSQL_DumpCmdLine.txt** - command line argument to dump db<br>

**Unittests.py** - unit test of python functions


## Author
created for Data Programming Assignment Part 2<br>
<br>
