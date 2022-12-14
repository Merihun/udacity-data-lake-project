# Sparkify Data Lake Project with Apache Spark

## Introduction

A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

This project is intended to build an ETL pipeline for a data lake hosted on S3. Your ETL should accomplish the belwo steps: 
* Extracts their data from S3, 
* process the data into analytics tables using Spark, and 
* loads the data back into S3 as a set of dimensional tables. 
* deploy this Spark process on a cluster using AWS.

Once the data is loded to dimensional tables, analytics team utilize it to continue finding insights in what songs their users are listening to.

You'll be able to test your database and ETL pipeline by running a set queries given to you by the analytics team from Sparkify and compare your results with their expected results.

## Project Description
In this project, you'll apply what you've learned on Spark and data lakes to build an ETL pipeline for a data lake hosted on S3. To complete the project, you will need to load data from S3, process the data into analytics tables using Spark, and load them back into S3. You'll deploy this Spark process on a cluster using AWS.

## AWS - Launch EMR Cluster and Notebook 
**Step -1: Configure your cluster with the following settings:**
* Release: emr-5.20.0 or later
* Applications: Spark: Spark 2.4.0 on Hadoop 2.8.5 YARN with Ganglia 3.7.2 and Zeppelin 0.8.0
* Instance type: m3.xlarge
* Number of instance: 3
* EC2 key pair: Proceed without an EC2 key pair or feel free to use one if you'd like
* You can keep the remaining default setting and click "Create cluster" on the bottom right.

**Step -2: Wait for Cluster "Waiting" Status**

Once you create the cluster, you'll see a status next to your cluster name that says Starting. Wait a short time for this status to change to Waiting before moving on to the next step.

**Step -3: Create Notebook**
Now that you launched your cluster successfully, let's create a notebook to run Spark on that cluster.

Select "Notebooks" in the menu on the left, and click the "Create notebook" button.

**Step -4: Configure your notebook**
* Enter a name for your notebook
* Select "Choose an existing cluster" and choose the cluster you just created
* Use the default setting for "AWS service role" - this should be "EMR_Notebooks_DefaultRole" or "Create default role" if you haven't done this before.
You can keep the remaining default settings and click "Create notebook" on the bottom right.

**Step 5: Wait for Notebook "Ready" Status,then Open**

Once you create an EMR notebook, you'll need to wait a short time before the notebook status changes from Starting or Pending to Ready. Once your notebook status is Ready, click the "Open" button to open the notebook.

**Start Coding!**
Now you can run Spark code for your project in this notebook, which EMR will run on your cluster. On the next pages, you'll find instructions about the dataset and processing you will be doing.

## Project Datasets
You'll be working with two datasets that reside in S3. Here are the S3 links for each:
```
Song data: s3://udacity-dend/song_data
Log data: s3://udacity-dend/log_data
```
## Song Dataset
The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.
```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```
And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.
```
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```
## Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.
```
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json

```
And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.

https://video.udacity-data.com/topher/2019/February/5c6c3f0a_log-data/log-data.png

## Schema for Song Play Analysis
Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.

### Fact Table
songplays - records in log data associated with song plays i.e. records with page NextSong
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
### Dimension Tables
**users** - users in the app
**user_id**, first_name, last_name, gender, level
**songs** - songs in music database
**song_id**, title, artist_id, year, duration
**artists** - artists in music database
**artist_id**, name, location, lattitude, longitude
**time** - timestamps of records in songplays broken down into specific units
start_time, hour, day, week, month, year, weekday


## Getting Started

To have a copy of the project up and running locally, the following should be done. 

### Prerequisites

* Python 2.7 or greater.

* AWS Account.

* Set your AWS access and secret key in the config file (dl.cfg).
```
AWS_ACCESS_KEY_ID = <your aws key>
AWS_SECRET_ACCESS_KEY = <your aws secret>

```
*** The project can be executed step-by-step using jupyter notebook coneected to sparck session after launching EMR Cluster and creating Notebook which is connected to the cluster.
### Installation

* Make a new directory and clone/copy project files into it.

* Download and install Apache Spark here https://spark.apache.org/downloads.html. 
* Ensure you have Java jdk8 installed locally.

Create a virtualenv that will be your development environment. Use the below terminal command.

```
$ virtualenv <you project name>
$ source <you project name>/bin/activate

```
Install the following packages in your virtual environment:

   - pyspark
   - Jupyter Notebook installed and setup   
Alternatively you can install the requirements in the requirements.txt that's in this project by running the terminal command:

```
$ pip install -r requirements.txt
```

Execute the ETL pipeline script by running:
$ python3 etl.py



