# How to connect a Data Product to DigiSpine

IMPORTANT: WORK IN PROGRESS

## Goal 
- Prototype to demonstrate how to connect a streaming database to DigiSpine

## Used Technology 
- Used technology for data product: RisingWave(https://docs.risingwave.com/docs/current/intro/)
- Reasoning: 
  - Streaming database to allow stream processing
  - Native Kafka connector included in official docker image
  - postgres compatible 
  - Zookeeper is not required 
  - Open source 

## Setup 
- Deploy DigiSpine [digispine-compose-production.yml](../DigiSpine/digispine_production.yml) 
- Deploy [kconnect-console-producer.yml](../DigiSpine/kafka-connect-clients/kconnect-console-producer.yml)
- Deploy [dataproduct.yml](dataproduct.yml) (NOT PRODUCTION READY!!!)
- Docu: https://docs.risingwave.com/docs/current/get-started/

### Validate RisingWave installation
- Use some postgres-compatible client (dbvisualizer)

- Connection information: 
  - \<IP of docker with deployed dataproduct.yml\>:4566 
  - database: `dev`
  - User: `root`
  - PW: not required

- create a table (postgres like) 
    ```sql
    CREATE TABLE website_visits (
    timestamp timestamp with time zone,
    user_id varchar,
    page_id varchar,
    action varchar
    );
    ``` 
- insert data (postgres like)
    ```sql
    INSERT INTO website_visits (timestamp, user_id, page_id, action) VALUES
    ('2023-06-13T10:00:00Z', 'user1', 'page1', 'view'),
    ('2023-06-13T10:01:00Z', 'user2', 'page2', 'view'),
    ('2023-06-13T10:02:00Z', 'user3', 'page3', 'view'),
    ('2023-06-13T10:03:00Z', 'user4', 'page1', 'view'),
    ('2023-06-13T10:04:00Z', 'user5', 'page2', 'view');
    ``` 

- Query data 
    ```sql
    SELECT * FROM website_visits;
    ``` 
- Result should be:
    ```
    2023-06-13 12:01:00	user2	page2	view
    2023-06-13 12:03:00	user4	page1	view
    2023-06-13 12:02:00	user3	page3	view
    2023-06-13 12:00:00	user1	page1	view
    2023-06-13 12:04:00	user5	page2	view
    ```

## Connect to DigiSpine

- Create a source stream in RisingWave that connects to DigiSpine / Kafka
    ```sql
    CREATE SOURCE IF NOT EXISTS flugdaten_stream (
    timestamp timestamp with time zone,
    flugdaten_value varchar
    )
    WITH (
    connector='kafka',
    topic='flugdaten',
    properties.bootstrap.server='digipods.digitalisierung.stahl-holding-saar.de:9092',
    scan.startup.mode='earliest'
    ) FORMAT PLAIN ENCODE JSON;
    ```
- Create a materialized view that represents data we offer as product. This also defines the data transformation/mapping from streams   
    ```sql
    CREATE MATERIALIZED VIEW flugdaten_stream_mv AS
    SELECT flugdaten_value,
    count(*) AS total_visits,
    count(DISTINCT flugdaten_value) AS unique_visitors,
    max(timestamp) AS last_visit_time
    FROM flugdaten_stream
    GROUP BY flugdaten_value;
    ```
- Query data from materialized view (standard postgres)
    ```sql
    SELECT * FROM flugdaten_stream_mv;
    ```
- Result should look as follows. Note: Only total_visits include valid data, that changes after each query 
   ```
  flugdaten_value	total_visits	unique_visitors	last_visit_time
  (null)	        1124079	        0	            (null)
  ```