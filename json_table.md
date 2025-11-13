# snowflake

# login with command prompt 
```
snowsql -a <account identifier> -u <user_name>
```

<img width="810" height="234" alt="image" src="https://github.com/user-attachments/assets/26753dd7-3157-4119-8601-83f5f9a1c029" />

# Converting json file into snowflake table 

# create database and schema

```
create database json_db;
create databe json_sch;
use database json_db;
use schema json_sch;
```

# create stage for json 

```
CREATE OR REPLACE STAGE json_stage;
```
<img width="721" height="135" alt="image" src="https://github.com/user-attachments/assets/3b369299-ce20-476d-81d2-cf888101c2d4" />

# file upload from loal folder to snowflake

```
PUT 'file://D:\\aws project\\car.json' @json_stage AUTO_COMPRESS=FALSE;
```
<img width="1043" height="115" alt="image" src="https://github.com/user-attachments/assets/d219e5b2-2279-4f3a-a3f2-2402df2180ea" />

# copy format 
```
COPY INTO CAR_JSON
FROM @json_stage/car.json
FILE_FORMAT = (TYPE = 'JSON');
```
<img width="1566" height="159" alt="image" src="https://github.com/user-attachments/assets/53014e67-9f64-42a4-8468-42a30063a06f" />

# Create table in car format 

```
CREATE OR REPLACE TABLE cars AS
SELECT
data:id::INT AS id,
data:first_name::STRING AS first_name,
data:last_name::STRING AS last_name,
data:car_make::STRING AS car_make,
data:Car_Model::STRING AS car_model,
data:Car_Model_Year::INT AS car_model_year
FROM car_json;
```

<img width="748" height="264" alt="image" src="https://github.com/user-attachments/assets/bdcd21dc-d9f0-4fdc-a148-6dc00675e87b" />


# Verify table for json 
```
SELECT * FROM CAR_JSON limit 2;
```

<img width="813" height="404" alt="image" src="https://github.com/user-attachments/assets/2d214e17-f6c2-4a36-909e-3abaf22545c2" />

# verify table after conversion

<img width="792" height="138" alt="image" src="https://github.com/user-attachments/assets/88c63677-e8ae-4582-b4d9-67afee6bc06a" />















