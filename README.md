# Data Loading and Preprocessing Test

## Description

In the `import_data` directory, you will find two files: a CSV file and a JSON file.

These files are downloaded from [https://uk-cri.org/](https://uk-cri.org/) and, in this instance, contain climate average temperature data for the UK.

This type of data is commonly used by 3Adapt within Landarna, and this task reflects the type of work expected in the role.

## Task

Load the data into PostgreSQL for use in Landarna, as well as to create or serve tiles for the web application.

You have been provided with a PostgreSQL database connection string unique to you. Use this to connect to the database and load the data. Do not worry about breaking anything; the database provided is a test database specifically created for this task and will be destroyed once testing is complete.

If at any point you cannot connect to the database or have any further questions, please contact us for assistance.

## Goals

- Load the data into one or more tables defined by you within the PostgreSQL `results` database, under the `cca` schema.
- Ensure the tables include a PostGIS geometry column to enable data use in Landarna and tile generation in the EPSG:4326 projection.
- You may use any tools you prefer to load the data, but clearly document your process and be ready to explain your tool choices.
- Your process should be repeatable, as updating data will be a regular requirement. Tools such as Python, QGIS, or FME are acceptable.
- Provide an example query demonstrating how, for a given polygon and year, intersecting data can be extracted from the tables you created.

## Considerations

- The data files are relational; this must be accounted for during data loading.
- Future datasets that are also relational will need to be loaded into the database, so design your schema accordingly.
- For this test, we've chosen the lowest resolution dataset, but higher resolution datasets exist. Your solution should be scalable and capable of handling higher-resolution data.

## Documentation Requirements

Your submitted solution must clearly document:

- The process used to load the data.
- The structure of the table(s) you created.
- An example query demonstrating how to extract intersecting data from your tables.

## 3ADAPT Task Setup

We have initialized the database with the following:

```postgresql
CREATE EXTENSION postgis;
CREATE EXTENSION postgis_topology;
SELECT PostGIS_version();

CREATE TABLE cca.locations
(
    id   SERIAL PRIMARY KEY,
    name VARCHAR(100),
    geom GEOMETRY(Point, 4326)
);

INSERT INTO cca.locations (name, geom)
VALUES ('My Location', ST_GeomFromText('POINT(-71.060316 48.432044)', 4326));
```

To confirm your connection to the database, please run this query:

```postgresql
SELECT * FROM cca.locations;
```

You should see a single row returned with the name 'My Location' and its corresponding point geometry.

