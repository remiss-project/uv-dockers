# uv-dockers
The urls are only available by connecting to Esade VPN 
* Dashboard --> http://srvinv02.esade.es:8180/
* API --> http://srvinv02.esade.es:5005/
* METRICS --> http://srvinv02.esade.es:5006/
  
# Documentation for laiauv's "remiss-api" Docker Image

This Docker image contains an API for accessing and analyzing datasets stored in the Mongo database. The API provides various endpoints for retrieving data and generating visualizations using Plotly with R.


## Usage

### Downloading the Image from Docker Hub

To download the image from Docker Hub, execute the following command:

```bash
docker pull laiauv/remiss-api:latest
```

### Running the Downloaded Image

Once you have downloaded the image, you can run a container using this image. For example:

```bash
docker run --rm -p 5005:5005 laiauv/remiss-api:latest
```

This will run the image as a container and map port 5005 of the container to port 5005 on your local machine.
Note that laiauv is the username on Docker Hub and remiss-api is the image name.

You can modify the MONGO_URL environment variable when running the Docker container using the -e option followed by the name of the environment variable and its new value. By default is ENV MONGO_URL="mongodb://localhost/remiss".
```bash
docker run --rm -p 5005:5005 -e MONGO_URL="new_mongo_url_value" laiauv/remiss-api:latest
docker run --rm -p 5005:5005 -e MONGO_URL="mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.0.0" laiauv/remiss-api:latest
```

## API Endpoints

The API offers several endpoints for accessing data and generating visualizations. All endpoints accept the following arguments:

* name (string): Filters the data by dataset name. [ Andalucia_2022 , Barcelona_2019 , Castilla_Leon_2022, Generales_2019, Generalitat_2021, MENA_Agressions, MENA_Ajudes, Madrid_2021, Openarms ]
* window (integer): Specifies the time window for analyzing the data in a defined period.
* start (string): Defines the start of a specific date range.
* end (string): Indicates the end of the date range.

The format for start and end arguments is YYYY-MM-DD.

### /api/get_data

Retrieves the indicated information from the database.
Example:
```bash
GET /api/get_data?name=Castilla_Leon_2022&window=20
```

### /api/graph1

Get the JSON data to generate an emotion line graph per hour.
Example:
```bash
GET /api/graph1?name=Castilla_Leon_2022&start=2020-12-01&end=2021-02-28
```

### /api/graph2

Get the JSON data to generate an average emotion bar graph.
Example:
```bash
GET /api/graph2?name=Castilla_Leon_2022&window=30
```
### /api/graph3
Get the JSON data to generate a graph of top profiles.
Example:
```bash
GET /api/graph3?name=Castilla_Leon_2022
```
### /api/graph4
Get the JSON data to generate a graph of top hashtags.
Example:
```bash
GET /api/graph4?name=Castilla_Leon_2022
```
### /api/graph5
Get the JSON data to generate

Example:
```bash
GET /api/graph5?name=Castilla_Leon_2022
```
### /api/graph6
Get the JSON data to generate
Example:
```bash
GET /api/graph6?name=Castilla_Leon_2022&window=1
```

# Documentation for laiauv's "remiss-shiny" Docker Image
This Docker image contains the visualization tool for analyzing tweets and generating graphs based on various characteristics like syntactic information, emotions, sentiment, and the probability of fake news obtained by or Random Forest.

## Usage

### Downloading the Image from Docker Hub

To download the image from Docker Hub, execute the following command:

```bash
docker pull laiauv/remiss-shiny:latest
```

### Running the Downloaded Image

Once you have downloaded the image, you can run a container using this image. For example:

```bash
docker run --rm -p 8180:8180 laiauv/remiss-shiny:latest
sudo docker run --rm -d --name remiss-uv-dashboard -p 8180:8180 --link remiss-uv-api:remiss-uv-api laiauv/remiss-shiny:latest
```

This will run the image as a container and map port 8180 of the container to port 8180 on your local machine.
Note that laiauv is the username on Docker Hub and remiss-shiny is the image name.


# Documentation for laiauv's "remiss-metrics" Docker Image
The application can process CSV files containing text data and perform detailed analysis on that data

## Usage

### Downloading the Image from Docker Hub

To download the image from Docker Hub, execute the following command:

```bash
docker pull laiauv/remiss-metrics:latest
```

### Running the Downloaded Image

Once you have downloaded the image, you can run a container using this image. For example:

```bash
curl -X POST "http://127.0.0.1:5006/process?file_name=prueba.csv&db_name=test&col_name=textual&text_label=text"
```

## API Endpoint

### POST /process

This endpoint processes a CSV file containing text data and performs various metrics and analyses on that data, such as emotion analysis, linguistic feature extraction, authenticity prediction, etc. The required parameters for this endpoint include:
* file_name: The name of the CSV file containing the text data to be processed.
* db_name: The name of the database where the analysis results will be saved.
* col_name: The name of the collection (or table) within the database where the results will be stored.
* text_label: The text label to be used for analysis. This label identifies the column in the CSV file that contains the texts to be analyzed.

These parameters are necessary for the endpoint to perform the appropriate processing and analysis of the text data provided in the CSV file.

```bash
curl -X POST "http://127.0.0.1:5006/process?file_name=prueba.csv&db_name=test&col_name=textual&text_label=text"

```

## Authors
- [LAIA-UV](https://laia.uv.es/)
