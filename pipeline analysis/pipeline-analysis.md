```python
import sqlite3
import pandas as pd

# Reading fires from SQLite
conn = sqlite3.connect("/Users/sharinir/Downloads/FPA_FOD_20221014.sqlite") 

# Checking what tables exist
tables = pd.read_sql("SELECT name FROM sqlite_master WHERE type='table'", conn)
print(tables)
```

                                      name
    0                      spatial_ref_sys
    1                   spatialite_history
    2                      sqlite_sequence
    3                     geometry_columns
    4               views_geometry_columns
    5               virts_geometry_columns
    6          geometry_columns_statistics
    7    views_geometry_columns_statistics
    8    virts_geometry_columns_statistics
    9         geometry_columns_field_infos
    10  views_geometry_columns_field_infos
    11  virts_geometry_columns_field_infos
    12               geometry_columns_time
    13               geometry_columns_auth
    14         views_geometry_columns_auth
    15         virts_geometry_columns_auth
    16                  sql_statements_log
    17                        SpatialIndex
    18          NWCG_UnitIdActive_20200123
    19                               Fires
    20                     idx_Fires_Shape
    21               idx_Fires_Shape_rowid
    22                idx_Fires_Shape_node
    23              idx_Fires_Shape_parent



```python
fires = pd.read_sql("SELECT * FROM Fires LIMIT 5", conn)
print(fires.columns.tolist())
```

    ['OBJECTID', 'Shape', 'FOD_ID', 'FPA_ID', 'SOURCE_SYSTEM_TYPE', 'SOURCE_SYSTEM', 'NWCG_REPORTING_AGENCY', 'NWCG_REPORTING_UNIT_ID', 'NWCG_REPORTING_UNIT_NAME', 'SOURCE_REPORTING_UNIT', 'SOURCE_REPORTING_UNIT_NAME', 'LOCAL_FIRE_REPORT_ID', 'LOCAL_INCIDENT_ID', 'FIRE_CODE', 'FIRE_NAME', 'ICS_209_PLUS_INCIDENT_JOIN_ID', 'ICS_209_PLUS_COMPLEX_JOIN_ID', 'MTBS_ID', 'MTBS_FIRE_NAME', 'COMPLEX_NAME', 'FIRE_YEAR', 'DISCOVERY_DATE', 'DISCOVERY_DOY', 'DISCOVERY_TIME', 'NWCG_CAUSE_CLASSIFICATION', 'NWCG_GENERAL_CAUSE', 'NWCG_CAUSE_AGE_CATEGORY', 'CONT_DATE', 'CONT_DOY', 'CONT_TIME', 'FIRE_SIZE', 'FIRE_SIZE_CLASS', 'LATITUDE', 'LONGITUDE', 'OWNER_DESCR', 'STATE', 'COUNTY', 'FIPS_CODE', 'FIPS_NAME']



```python
# Loading just CA and NV fires with specific columns (to match NOAA data)
fires = pd.read_sql("""
    SELECT FOD_ID, FIRE_NAME, STATE, COUNTY, FIRE_YEAR, DISCOVERY_DATE,
           NWCG_GENERAL_CAUSE, FIRE_SIZE, FIRE_SIZE_CLASS, LATITUDE, LONGITUDE
    FROM Fires
    WHERE STATE IN ('CA', 'NV')
""", conn)
conn.close()

print(f"Total fires: {len(fires)}")
print(fires.head())
```

    Total fires: 272091
       FOD_ID FIRE_NAME STATE COUNTY  FIRE_YEAR DISCOVERY_DATE  \
    0       1  FOUNTAIN    CA     63       2005       2/2/2005   
    1       2    PIGEON    CA     61       2004      5/12/2004   
    2       3     SLACK    CA     17       2004      5/31/2004   
    3       4      DEER    CA      3       2004      6/28/2004   
    4       5  STEVENOT    CA      3       2004      6/28/2004   
    
                               NWCG_GENERAL_CAUSE  FIRE_SIZE FIRE_SIZE_CLASS  \
    0  Power generation/transmission/distribution       0.10               A   
    1                                     Natural       0.25               A   
    2                     Debris and open burning       0.10               A   
    3                                     Natural       0.10               A   
    4                                     Natural       0.10               A   
    
        LATITUDE   LONGITUDE  
    0  40.036944 -121.005833  
    1  38.933056 -120.404444  
    2  38.984167 -120.735556  
    3  38.559167 -119.913333  
    4  38.559167 -119.933056  



```python
# Reading in NOAA daily summary data
weather = pd.read_csv("daily_weather_west.csv")
print(weather.columns.tolist())
print(weather.head())
```

    ['STATION', 'NAME', 'DATE', 'AWND', 'PRCP', 'SNOW', 'TAVG', 'TMAX', 'TMIN', 'WT01', 'WT02', 'WT03', 'WT04', 'WT05', 'WT06', 'WT07', 'WT08', 'WT09', 'WT10', 'WT11', 'WT13', 'WT14', 'WT15', 'WT16', 'WT18', 'WT19', 'WT21', 'WT22']
           STATION                         NAME        DATE  AWND  PRCP  SNOW  \
    0  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-01   NaN   NaN   NaN   
    1  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-02   NaN   NaN   NaN   
    2  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-03   NaN   NaN   NaN   
    3  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-04   NaN   NaN   NaN   
    4  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-05   NaN   NaN   NaN   
    
       TAVG  TMAX  TMIN  WT01  ...  WT10  WT11  WT13  WT14  WT15  WT16  WT18  \
    0  35.0  38.0  33.0   NaN  ...   NaN   NaN   NaN   NaN   NaN   NaN   NaN   
    1  32.0  34.0  29.0   NaN  ...   NaN   NaN   NaN   NaN   NaN   NaN   NaN   
    2  29.0  34.0  27.0   NaN  ...   NaN   NaN   NaN   NaN   NaN   NaN   NaN   
    3  36.0  45.0  27.0   NaN  ...   NaN   NaN   NaN   NaN   NaN   NaN   NaN   
    4  36.0  43.0  29.0   NaN  ...   NaN   NaN   NaN   NaN   NaN   NaN   NaN   
    
       WT19  WT21  WT22  
    0   NaN   NaN   NaN  
    1   NaN   NaN   NaN  
    2   NaN   NaN   NaN  
    3   NaN   NaN   NaN  
    4   NaN   NaN   NaN  
    
    [5 rows x 28 columns]



```python
# Removing unnecessary columns 
weather = weather.drop(columns=[col for col in weather.columns if col.startswith("WT")])
print(weather.head())
```

           STATION                         NAME        DATE  AWND  PRCP  SNOW  \
    0  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-01   NaN   NaN   NaN   
    1  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-02   NaN   NaN   NaN   
    2  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-03   NaN   NaN   NaN   
    3  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-04   NaN   NaN   NaN   
    4  USR0000NBUF  BUFFALO CREEK NEVADA, NV US  1992-01-05   NaN   NaN   NaN   
    
       TAVG  TMAX  TMIN  
    0  35.0  38.0  33.0  
    1  32.0  34.0  29.0  
    2  29.0  34.0  27.0  
    3  36.0  45.0  27.0  
    4  36.0  43.0  29.0  



```python
# Extract state from NAME column (last 2 chars before "US")
weather["state"] = weather["NAME"].str.extract(r',\s(\w{2})\sUS')
weather["year"] = pd.to_datetime(weather["DATE"]).dt.year
weather["month"] = pd.to_datetime(weather["DATE"]).dt.month

# Monthly averages per state
weather_avg = weather.groupby(["state", "year", "month"]).agg(
    avg_temp=("TAVG", "mean"),
    avg_tmax=("TMAX", "mean"),
    avg_tmin=("TMIN", "mean"),
    avg_precip=("PRCP", "mean"),
    avg_snow=("SNOW", "mean"),
    avg_wind=("AWND", "mean")
).reset_index()

print(weather_avg.head())
print(f"States found: {weather_avg['state'].unique()}")
```

      state  year  month   avg_temp   avg_tmax   avg_tmin  avg_precip  avg_snow  \
    0    CA  1992      1  32.531017  48.234767  27.985663    0.045533       0.0   
    1    CA  1992      2  35.609756  51.678988  33.241245    0.147480       0.0   
    2    CA  1992      3  37.178660  53.896057  33.817204    0.084491       0.0   
    3    CA  1992      4  45.987179  63.551852  38.901852    0.022077       0.0   
    4    CA  1992      5  55.375622  72.457810  45.141831    0.012605       0.0   
    
        avg_wind  
    0   6.621613  
    1   7.440805  
    2   7.942151  
    3   9.877000  
    4  10.138280  
    States found: ['CA' 'NV']



```python
# Extract year and month from fires
fires["year"] = pd.to_datetime(fires["DISCOVERY_DATE"]).dt.year
fires["month"] = pd.to_datetime(fires["DISCOVERY_DATE"]).dt.month

# Merge fires with weather averages on state, year, month
merged = fires.merge(weather_avg, left_on=["STATE", "year", "month"], right_on=["state", "year", "month"], how="left")

print(f"Total fires: {len(merged)}")
print(f"Fires with matched weather: {merged['avg_temp'].notna().sum()}")
print(merged.head())
```

    Total fires: 272091
    Fires with matched weather: 272091
       FOD_ID FIRE_NAME STATE COUNTY  FIRE_YEAR DISCOVERY_DATE  \
    0       1  FOUNTAIN    CA     63       2005       2/2/2005   
    1       2    PIGEON    CA     61       2004      5/12/2004   
    2       3     SLACK    CA     17       2004      5/31/2004   
    3       4      DEER    CA      3       2004      6/28/2004   
    4       5  STEVENOT    CA      3       2004      6/28/2004   
    
                               NWCG_GENERAL_CAUSE  FIRE_SIZE FIRE_SIZE_CLASS  \
    0  Power generation/transmission/distribution       0.10               A   
    1                                     Natural       0.25               A   
    2                     Debris and open burning       0.10               A   
    3                                     Natural       0.10               A   
    4                                     Natural       0.10               A   
    
        LATITUDE   LONGITUDE  year  month state   avg_temp   avg_tmax   avg_tmin  \
    0  40.036944 -121.005833  2005      2    CA  38.566316  50.151093  31.471173   
    1  38.933056 -120.404444  2004      5    CA  52.981025  66.258065  40.779570   
    2  38.984167 -120.735556  2004      5    CA  52.981025  66.258065  40.779570   
    3  38.559167 -119.913333  2004      6    CA  60.807466  74.745826  46.935065   
    4  38.559167 -119.933056  2004      6    CA  60.807466  74.745826  46.935065   
    
       avg_precip  avg_snow   avg_wind  
    0    0.114698       0.0   5.328839  
    1    0.031985       0.0  10.146129  
    2    0.031985       0.0  10.146129  
    3    0.002821       0.0  10.740917  
    4    0.002821       0.0  10.740917  



```python
from dotenv import load_dotenv
import os
from pymongo import MongoClient

load_dotenv()

# Connect to Atlas and target the wildfires database
client = MongoClient(os.getenv("MONGO_URI"))
db = client["wildfires"]
collection = db["fires"]

# Build one document per fire, embedding matched weather data inside it
documents = []
for _, row in merged.iterrows():
    doc = {
        "fire_id": int(row["FOD_ID"]),
        "name": row["FIRE_NAME"],
        "state": row["STATE"],
        "county": row["COUNTY"],
        "year": int(row["year"]),
        "month": int(row["month"]),
        "cause": row["NWCG_GENERAL_CAUSE"],
        "size_acres": float(row["FIRE_SIZE"]),
        "size_class": row["FIRE_SIZE_CLASS"],
        # Nested location sub-document
        "location": {
            "latitude": float(row["LATITUDE"]),
            "longitude": float(row["LONGITUDE"])
        },
        # Nested weather sub-document, averaged across stations by state and month
        "weather": {
            "avg_temp_f": round(float(row["avg_temp"]), 2),
            "avg_tmax_f": round(float(row["avg_tmax"]), 2),
            "avg_tmin_f": round(float(row["avg_tmin"]), 2),
            "avg_precip_in": round(float(row["avg_precip"]), 2),
            "avg_snow_in": round(float(row["avg_snow"]), 2),
            "avg_wind_mph": round(float(row["avg_wind"]), 2),
            "match_method": "state_month_average"  # documents how weather was joined
        }
    }
    documents.append(doc)

# Insert in batches to avoid hitting Atlas request size limits
batch_size = 10000
for i in range(0, len(documents), batch_size):
    collection.insert_many(documents[i:i+batch_size])
    print(f"Inserted {min(i+batch_size, len(documents))} / {len(documents)}")

print("Done!")
```

    Inserted 10000 / 272091
    Inserted 20000 / 272091
    Inserted 30000 / 272091
    Inserted 40000 / 272091
    Inserted 50000 / 272091
    Inserted 60000 / 272091
    Inserted 70000 / 272091
    Inserted 80000 / 272091
    Inserted 90000 / 272091
    Inserted 100000 / 272091
    Inserted 110000 / 272091
    Inserted 120000 / 272091
    Inserted 130000 / 272091
    Inserted 140000 / 272091
    Inserted 150000 / 272091
    Inserted 160000 / 272091
    Inserted 170000 / 272091
    Inserted 180000 / 272091
    Inserted 190000 / 272091
    Inserted 200000 / 272091
    Inserted 210000 / 272091
    Inserted 220000 / 272091
    Inserted 230000 / 272091
    Inserted 240000 / 272091
    Inserted 250000 / 272091
    Inserted 260000 / 272091
    Inserted 270000 / 272091
    Inserted 272091 / 272091
    Done!

