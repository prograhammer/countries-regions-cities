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
| ------------- |:---------------------------------------------| :-------------------------------:|
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

