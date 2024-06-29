### EnergyDataTool
EnergyDataTool is a Python-based tool for managing and analyzing energy consumption data. It enables data import from CSV files, filtering based on thresholds, and storing the results in a MongoDB database.

### Features
- Data Import: Load energy consumption data from CSV files.
- Data Filtering: Filter data based on specified thresholds.
- Database Operations: Store, update, and retrieve data in MongoDB.

### Usage
## Data Import and Filtering
```Python
import pandas as pd

# Load data from CSV
file_path = "path_to_your_csv_file.csv"
columns_to_use = ["date", "hour", "store_id", "imwh"]
df = pd.read_csv(file_path, sep=",", header=None, names=columns_to_use, skiprows=1)

# Filter data for a specific store and threshold
store_id = 6193
upper_limit = 85

def getThresholds(store_id, upper_limit):
    magaza_data = df[df["store_id"] == store_id]
    magaza_data = magaza_data.sort_values(by="hour")
    threshold_data = magaza_data[magaza_data["imwh"] > upper_limit]
    return threshold_data

threshold_data = getThresholds(store_id, upper_limit)
print("Data exceeding the threshold:")
print(threshold_data)
```

## Database Operations
```Python
from pymongo import MongoClient

# Connect to MongoDB
client = MongoClient("your_mongodb_connection_string")
db = client.get_database('main_db')
records = db.main_records

# Insert data into MongoDB
new_data = {
    'date': '2022-06-05',
    'hour': 10,
    'store_id': 2831,
    'imwh': 55.8081
}
records.insert_one(new_data)

# Insert multiple records
new_datas = [
    {'date': '2022-06-05', 'hour': 10, 'store_id': 2832, 'imwh': 55.8081},
    {'date': '2022-06-05', 'hour': 10, 'store_id': 2833, 'imwh': 55.8081}
]
records.insert_many(new_datas)

# Query the database
print(list(records.find()))

```



