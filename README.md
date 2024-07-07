Q1. What is MongoDB? Explain non-relational databases in short. In which scenarios it is preferred to use MongoDB over SQL databases?
MongoDB is a NoSQL, document-oriented database that stores data in JSON-like, flexible documents with a dynamic schema. It is designed for scalability and flexibility, making it a popular choice for handling unstructured or semi-structured data.

Non-relational databases, also known as NoSQL databases, do not use the traditional table-based relational database structure. Instead, they use a variety of data models, including document, key-value, wide-column, and graph formats. These databases are designed to handle large volumes of diverse data and to provide horizontal scalability.

Scenarios where MongoDB is preferred over SQL databases:

Flexible Schema: When the data model is dynamic or evolving, and the structure is not fixed.
High Write Load: Applications that require high write throughput, such as logging and real-time analytics.
Big Data and Scalability: Applications that need to handle large volumes of data and require horizontal scalability.
Complex Data Structures: When data is naturally represented as nested or hierarchical documents.
Rapid Development: When development speed and agility are important, and schema changes are frequent.
Q2. State and Explain the features of MongoDB.
Flexible Schema: MongoDB allows for dynamic schemas, meaning documents in the same collection do not need to have the same set of fields, and data types for the fields can differ.
Scalability: MongoDB supports horizontal scaling through sharding, which distributes data across multiple servers.
Replication: Provides high availability and data redundancy through replica sets, which automatically failover if the primary server goes down.
High Performance: Optimized for read and write operations, especially with large datasets.
Indexing: Supports secondary indexes, geospatial indexes, and full-text search to improve query performance.
Aggregation Framework: Offers a powerful aggregation framework for data processing and analysis.
Ad Hoc Queries: Supports a rich query language to perform complex queries, including filtering, sorting, and projection.
File Storage: GridFS allows for efficient storage of large files, such as images and videos.
Transactions: Supports multi-document ACID transactions, ensuring data consistency and reliability.
Q3. Write a code to connect MongoDB to Python. Also, create a database and a collection in MongoDB.
python
Copy code
from pymongo import MongoClient

# Connect to MongoDB server
client = MongoClient('mongodb://localhost:27017/')

# Create a database
db = client['mydatabase']

# Create a collection
collection = db['mycollection']

print("Database and collection created successfully.")
Q4. Using the database and the collection created in question number 3, write a code to insert one record, and insert many records. Use the find() and find_one() methods to print the inserted record.
python
Copy code
from pymongo import MongoClient

# Connect to MongoDB server
client = MongoClient('mongodb://localhost:27017/')

# Access the database and collection
db = client['mydatabase']
collection = db['mycollection']

# Insert one record
record = {"name": "John Doe", "age": 30, "city": "New York"}
collection.insert_one(record)

# Insert many records
records = [
    {"name": "Jane Doe", "age": 25, "city": "Chicago"},
    {"name": "Alice Smith", "age": 27, "city": "Los Angeles"},
    {"name": "Bob Brown", "age": 35, "city": "San Francisco"}
]
collection.insert_many(records)

# Find one record
print("Find one record:")
print(collection.find_one({"name": "John Doe"}))

# Find all records
print("\nFind all records:")
for rec in collection.find():
    print(rec)
Q5. Explain how you can use the find() method to query the MongoDB database. Write a simple code to demonstrate this.
The find() method is used to query documents from a MongoDB collection. It can accept a query object to filter the documents returned and can also accept projection arguments to specify which fields to include or exclude.

python
Copy code
from pymongo import MongoClient

# Connect to MongoDB server
client = MongoClient('mongodb://localhost:27017/')

# Access the database and collection
db = client['mydatabase']
collection = db['mycollection']

# Find all documents where the age is greater than 25
query = {"age": {"$gt": 25}}

print("Documents where age is greater than 25:")
for doc in collection.find(query):
    print(doc)
Q6. Explain the sort() method. Give an example to demonstrate sorting in MongoDB.
The sort() method is used to sort the documents in the result set of a query. It takes one or more key-value pairs, where the key is the field name and the value is the sorting order (1 for ascending, -1 for descending).

python
Copy code
from pymongo import MongoClient

# Connect to MongoDB server
client = MongoClient('mongodb://localhost:27017/')

# Access the database and collection
db = client['mydatabase']
collection = db['mycollection']

# Sort documents by age in ascending order
print("Documents sorted by age in ascending order:")
for doc in collection.find().sort("age", 1):
    print(doc)

# Sort documents by age in descending order
print("\nDocuments sorted by age in descending order:")
for doc in collection.find().sort("age", -1):
    print(doc)
Q7. Explain why delete_one(), delete_many(), and drop() are used.
delete_one(): Removes a single document from a collection that matches the filter criteria.

python
Copy code
collection.delete_one({"name": "John Doe"})
Used when you want to delete only one document even if multiple documents match the criteria.

delete_many(): Removes all documents from a collection that match the filter criteria.

python
Copy code
collection.delete_many({"age": {"$gt": 30}})
Used when you need to delete multiple documents that meet the specified condition.

drop(): Removes the entire collection, including all documents and indexes.

python
Copy code
collection.drop()
Used when you want to completely delete a collection from the database, effectively clearing all its data.
