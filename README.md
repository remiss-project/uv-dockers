# uv-dockers
# Documentation for laiauv's "remiss-api" Docker Image

This Docker image contains an API for accessing and analyzing datasets stored in a database. The API provides various endpoints for retrieving data and generating visualizations using Plotly with R.

## Usage

### Downloading the Image from Docker Hub

To download the image from Docker Hub, execute the following command:

```bash
docker pull laiauv/remiss-api:v3
```

### Running the Downloaded Image

Once you have downloaded the image, you can run a container using this image. For example:

```bash
docker run --rm -p 5005:5005 laiauv/remiss-api:v3
```

This will run the image as a container and map port 5005 of the container to port 5005 on your local machine.
Note that laiauv is the username on Docker Hub and remiss-api is the image name.

## API Endpoints

The API offers several endpoints for accessing data and generating visualizations. All endpoints accept the following arguments:

* name (string): Filters the data by dataset name.
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
