# MySQL normalized and ready-to-use tables of Countries, Regions (Provinces/States), Cities

## Installation

*The SQL file includes create statements with indexes, so simply follow the steps below to import the sql file.*

**Linux/OSX command line:**
    
    $ gunzip world.sql.gz
    $ mysql -u myusername -p mypassword
    mysql> use mydatabase;
    mysql> source world.sql;

**Windows**

- Install 7zip (so you can extract gzip files)
- Extract world.sql.gz and then use the same mysql command lines as Linux above on the `world.sql` file

## Data Structure

### Countries table

- Size (uncompressed, in database w/ indexes): 32 KB
- 230 records

| Column        | Type                                         | Description                      |
| ------------- |:---------------------------------------------| :--------------------------------|
| id            | SMALLINT(5) UNSIGNED NOT NULL AUTO_INCREMENT | Primary Key for a Country        |
| name          | VARCHAR(255) NOT NULL                        | Country name                     |
| code          | VARCHAR(10) NOT NULL                         | Country abbreviation             |

### Regions table (regions/provinces/states)

- Size (uncompressed, in database w/ indexes): 320 KB
- 3,888 records

| Column        | Type                                         | Description                            |
| ------------- |:---------------------------------------------| :--------------------------------------|
| id            | INT(11) UNSIGNED NOT NULL AUTO_INCREMENT     | Primary Key for a Region               |
| name          | VARCHAR(255) NOT NULL                        | Region name                            |
| code          | VARCHAR(10) NOT NULL                         | For USA: State/Territory abbreviation  |
| country_id    | SMALLINT(5) UNSIGNED NOT NULL                | Foreign key to Countries table         |

### Cities table

- Size (uncompressed, in database w/ indexes): 272 MB
- 2,790,951 records

| Column        | Type                                         | Description                                   |
| ------------- |:---------------------------------------------| :---------------------------------------------|
| id            | INT(11) UNSIGNED NOT NULL AUTO_INCREMENT     | Primary Key for a City                        |
| name          | VARCHAR(255) NOT NULL                        | City name                                     |
| region_id     | INT(11) UNSIGNED NOT NULL                    | Foreign key to Regions table (States for USA) |
| country_id    | SMALLINT(5) UNSIGNED NOT NULL                | Foreign key to Countries table                |
| latitude      | DECIMAL(10,8) NOT NULL                       | City Latitude                                 |
| longitude     | DECIMAL(11,8) NOT NULL                       | City Longitude                                |

<br><br>


# MongoDB collection created by joining of mysql tables listed above. 

#Description

*MongoDB supports query operations on geospatial data. You could get more information from https://docs.mongodb.com/manual/geospatial-queries *


## Installation

*Follow the steps below to import the collection.*

**Linux/OSX command line:**
    
    $ gunzip world.json.gz
    $ mongoimport --db mydatabase --collection mycollection --file world.json


**Windows**

- Install 7zip (so you can extract gzip files)
- Extract world.json.gz and then use the same mongoimport command lines as Linux above on the `world.json` file

## Data Structure of collection


| Field         | Type                                         | Description                                   |
| ------------- |:---------------------------------------------| :---------------------------------------------|
| _id           | ObjectId                                     | Unique key of collection                      |
| name          | String                                       | City name                                     |
| region        | String                                       | Region name                                   |
| country       | String                                       | Country name                                  |
| location      | GeoJSON Point                                | Location data                                 |

You could find more information about GeoJsonPoint on the https://docs.mongodb.com/manual/reference/geojson/#point

<br><br>


## License for MaxMind WorldCities Database

OPEN DATA LICENSE for MaxMind WorldCities and Postal Code Databases

Copyright (c) 2008 MaxMind Inc.  All Rights Reserved.

All advertising materials and documentation mentioning features or use of
this database must display the following acknowledgment:
"This product includes data created by MaxMind, available from
http://www.maxmind.com/"

Redistribution and use with or without modification, are permitted provided
that the following conditions are met:
1. Redistributions must retain the above copyright notice, this list of
conditions and the following disclaimer in the documentation and/or other
materials provided with the distribution. 
2. All advertising materials and documentation mentioning features or use of
this database must display the following acknowledgement:
"This product includes data created by MaxMind, available from
http://www.maxmind.com/"
3. "MaxMind" may not be used to endorse or promote products derived from this
database without specific prior written permission.

THIS DATABASE IS PROVIDED BY MAXMIND.COM ``AS IS'' AND ANY 
EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED 
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE 
DISCLAIMED. IN NO EVENT SHALL MAXMIND.COM BE LIABLE FOR ANY 
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES 
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; 
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT 
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS 
DATABASE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
