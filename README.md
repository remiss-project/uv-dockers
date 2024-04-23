# uv-dockers
# Documentation for laiauv's "remiss-api" Docker Image

This Docker image contains an API for accessing and analyzing datasets stored in the Mongo database. The API provides various endpoints for retrieving data and generating visualizations using Plotly with R.
* Dashboard --> http://srvinv02.esade.es:8180/
* API --> http://srvinv02.esade.es:5005/

## Usage

### Downloading the Image from Docker Hub

To download the image from Docker Hub, execute the following command:

```bash
docker pull laiauv/remiss-api:v3
```

### Running the Downloaded Image

Once you have downloaded the image, you can run a container using this image. For example:

```bash
docker run --rm -p 5005:5006 laiauv/remiss-api:v3
```

This will run the image as a container and map port 5006 of the container to port 5005 on your local machine.
Note that laiauv is the username on Docker Hub and remiss-api is the image name.

You can modify the MONGO_URL environment variable when running the Docker container using the -e option followed by the name of the environment variable and its new value. By default is ENV MONGO_URL="mongodb://localhost/remiss".
```bash
docker run --rm -p 5005:5006 -e MONGO_URL="new_mongo_url_value" laiauv/remiss-api:v3
docker run --rm -p 5005:5006 -e MONGO_URL="mongodb://127.0.0.1:27017/remiss?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.0.0" laiauv/remiss-api:v3
```

## API Endpoints

The API offers several endpoints for accessing data and generating visualizations. All endpoints accept the following arguments:

* name (string): Filters the data by dataset name. [catalunya, madrid, andalucia, castleon, violacions, bcn15, bcn19, ajudes]
* window (integer): Specifies the time window for analyzing the data in a defined period.
* start (string): Defines the start of a specific date range.
* end (string): Indicates the end of the date range.

The format for start and end arguments is YYYY-MM-DD.

### /api/get_data

Retrieves the indicated information from the database.
Example:
```bash
GET /api/get_data?name=castleon&window=20
```

### /api/graph1

Get the JSON data to generate an emotion line graph per hour.
Example:
```bash
GET /api/graph1?name=castleon&start=2020-12-01&end=2021-02-28
```

### /api/graph2

Get the JSON data to generate an average emotion bar graph.
Example:
```bash
GET /api/graph2?name=castleon&window=30
```
### /api/graph3
Get the JSON data to generate a graph of top profiles.
Example:
```bash
GET /api/graph3?name=castleon
```
### /api/graph4
Get the JSON data to generate a graph of top hashtags.
Example:
```bash
GET /api/graph4?name=castleon
```
### /api/graph5
Get the JSON data to generate

Example:
```bash
GET /api/graph5?name=castleon
```
### /api/graph6
Get the JSON data to generate
Example:
```bash
GET /api/graph6?name=castleon&window=1
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
