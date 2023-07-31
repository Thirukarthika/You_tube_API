# You_tube_API

YouTube Data Harvesting and Warehousing using MongoDB, SQL


MongoDB Connection and Sample Operation

This is a Python script that demonstrates how to connect to a MongoDB server and perform a simple operation using the PyMongo library. The script uses the MongoDB Atlas cloud service for connection.

## Prerequisites

Before running the script, make sure you have the following installed:

- Python 3.x
- PyMongo library (can be installed via pip: `pip install pymongo`)
- MySQL


This is a Python script that allows you to interact with the YouTube API to retrieve information about channels, videos, and comments. The script uses the pymongo library to connect and interact with a MongoDB Atlas cluster and the mysql-connector-python library to interact with a local MySQL database. You can use this script to store YouTube data in both MongoDB and MySQL databases and perform data analysis using SQL queries.

## Prerequisites

Before running the script, make sure you have the following:

1. YouTube Data API v3 Developer Key: Replace the `DEVELOPER_KEY` variable with your YouTube API key. You can obtain it by creating a project in the Google Developers Console and enabling the YouTube Data API v3.

2. MongoDB Atlas Connection String: Replace the `CONNECTION_STRING` variable with your MongoDB Atlas connection string. You should have a MongoDB Atlas account to get this connection string.

3. MySQL Database Credentials: Replace the `MYSQL_HOST`, `MYSQL_USER`, `MYSQL_PASSWORD`, and `MYSQL_DATABASE` variables with your MySQL database credentials.

## Functionality

### YouTube Data Retrieval

The script provides the following functions to retrieve YouTube data:

1. `get_channel_info(channel_id)`: Retrieves information about a channel with the specified `channel_id` from the YouTube API.

2. `get_channel_videos(channel_id)`: Retrieves video IDs uploaded by a channel with the specified `channel_id` from the YouTube API.

3. `get_video_details(video_ids)`: Retrieves detailed information about videos with the specified `video_ids` from the YouTube API.

4. `get_comments_details(video_id)`: Retrieves details of comments for a video with the specified `video_id` from the YouTube API.

### Data Storage

The script provides functions to store YouTube data in MongoDB and then migrate the required details into MySQL databases:

1. `create_collections(db)`: Creates collections for channels, videos, and comments in the MongoDB database.

2. `store_data_in_mongodb(channel_id)`: Retrieves channel, video, and comment data for the specified `channel_id` and stores it in MongoDB.

3. `create_mysql_tables()`: Creates tables for channels, videos, and comments in the MySQL database.

4. `migrate_data_to_mysql(channel_name)`: Migrates data from MongoDB to MySQL for the specified `channel_name`.

### Data Analysis with SQL Queries

After retrieving and storing the data, the script provides a simple CLI menu to perform data analysis using SQL queries on the MySQL database. You can execute various predefined SQL queries to get insights on the YouTube data, such as:

1. List all video titles and their corresponding channel names.
2. List channels with the most number of videos and their video counts.
3. List the top 10 most viewed videos and their respective channels.
4. List the number of comments on each video and their corresponding video names.
5. List videos with the highest number of likes and their corresponding channel names.
6. List the total number of likes and dislikes for each video and their corresponding video names.
7. List the total number of views for each channel and their corresponding channel names.
8. List the names of all channels that have published videos in the year 2022.
9. List the average duration of all videos in each channel and their corresponding channel names.
10. List videos with the highest number of comments and their corresponding channel names.

## Usage

1. Replace the necessary API keys and credentials as mentioned in the "Prerequisites" section.

2. Run the script in a Python environment.

3. The script will prompt you to enter YouTube channel IDs. You can enter up to 10 channel IDs.

4. For each channel, it will retrieve channel information, video IDs, video details, and comments and asks user whether to store them in MongoDB/not.

5. After storing the data in MongoDB, the script will prompt you to choose a channel name from the list to migrate to SQL database.

6. Enter the corresponding number of the query from the menu or type 'exit' to stop query execution.

7. View the query results to gain insights into the YouTube data.

Note: You can modify or add more SQL queries to the menu if you want to perform additional data analysis tasks.

## MongoDB Connection

To establish a connection to the MongoDB server, the script uses the `pymongo.MongoClient` class from the PyMongo library. It connects to a MongoDB Atlas cluster using the provided connection URI. The URI contains authentication credentials (username and password), the cluster address, and additional options. In this script, the connection URI is:

```python
uri = "mongodb+srv://thirukarthikanadar21:oWwrPOs8XioZaSQd@cluster0.g3gasa2.mongodb.net/?retryWrites=true&w=majority"
```

Replace this URI with your own MongoDB Atlas connection URI.

## Ping the MongoDB Deployment

After establishing the connection, the script sends a ping request to the MongoDB server to confirm a successful connection. This is done using the `client.admin.command('ping')` method. If the connection is successful, the following message will be displayed:

```
Pinged your deployment. You successfully connected to MongoDB!
```

## Accessing a Sample Collection

Once the connection is confirmed, the script accesses a sample collection in the database. The database name is `youtube_db`, and the collection name is `youtube_collection`. You can modify these names to suit your own database and collection.

```python
# Access a sample collection
db = client.youtube_db  # Replace 'youtube_db' with your database name
collection = db.youtube_collection  # Replace 'youtube_collection' with your collection name
```

## Performing a Simple Operation

The script performs a simple operation to check the connection's functionality. It counts the number of documents in the collection using the `count_documents({})` method and prints the result:

```python
# Perform a simple operation to check the connection
document_count = collection.count_documents({})
print(f"Number of documents in the collection: {document_count}")
```

This will display the number of documents present in the `youtube_collection`.

## Handling Exceptions

The code is wrapped in a try-except block to handle exceptions gracefully. If any exception occurs during the connection process or the execution of the simple operation, it will be caught, and the corresponding error message will be displayed.

```python
except Exception as e:
    print(e)
```

## Running the Script

To run the script, simply execute it using a Python interpreter:

```bash
python your_script_name.py
```

Replace `your_script_name.py` with the name of the Python file containing the provided code.

Make sure that the required libraries (Python and PyMongo) are installed and that you have a working internet connection to connect to the MongoDB Atlas cluster.
Now let us proceed with migration of details from Mongodb to Mysql for **channel name** entered by user.

### Setting Up MySQL Tables

The script `create_mysql_tables()` creates three tables in the MySQL database to store data related to channels, videos, and comments. The tables are named `Channel`, `Video`, and `Comment`.

**Prerequisites:**

- Install the `mysql-connector-python` package using `pip install mysql-connector-python`.
- Make sure you have a MySQL database set up with the necessary credentials (database name, host, username, and password).

**Instructions:**

1. Open the Python script where you want to set up the MySQL tables.
2. Replace the placeholders `MYSQL_HOST`, `MYSQL_USER`, `MYSQL_PASSWORD`, and `MYSQL_DATABASE` with your actual MySQL credentials.
3. Run the script. The `create_mysql_tables()` function will be executed, connecting to your MySQL database and creating the required tables.
4. Check your MySQL database to verify that the `Channel`, `Video`, and `Comment` tables have been created successfully.

Note: If the tables already exist, running the script will drop them and recreate them.

### Migrating Data from MongoDB to MySQL

The script `migrate_data_to_mysql(channel_name)` migrates data from MongoDB to a MySQL database for a specified channel.

**Prerequisites:**

- Install the required packages `mysql-connector-python` and `pymongo`.
- Ensure you have a MongoDB Atlas cluster set up and connected to your MongoDB database.
- Make sure you have a MySQL database set up with the necessary credentials (database name, host, username, and password).

**Instructions:**

1. Open the Python script where you want to migrate the data.
2. Replace the placeholders `MYSQL_HOST`, `MYSQL_USER`, `MYSQL_PASSWORD`, and `MYSQL_DATABASE` with your actual MySQL credentials.
3. Replace the `CONNECTION_STRING` with your actual MongoDB connection string, including the database name.
4. Copy the `migrate_data_to_mysql(channel_name)` function to your script.
5. Replace the `channel_name` argument in the function call with the name of the channel for which you want to migrate the data.
6. Run the script. The function will connect to MongoDB, fetch the data for the specified channel, and insert it into the MySQL tables (`Channel`, `Video`, and `Comment`).
7. Check your MySQL database to verify that the data has been migrated successfully.
8. Write the appropriate SQL queries to get the useful insights.

That's it! You now have a basic understanding of how to connect to a MongoDB server and perform a simple operation using Python and PyMongo. Feel free to modify and expand the script based on your specific use case.

