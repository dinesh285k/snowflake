# snowflake

# login with command prompt 
```
snowsql -a <account identifier> -u <user_name>
```

<img width="810" height="234" alt="image" src="https://github.com/user-attachments/assets/26753dd7-3157-4119-8601-83f5f9a1c029" />


```
CREATE OR REPLACE STAGE json_stage;
```

```
PUT file:///C:/path_to_your_folder/*.json @json_stage;
```

```
LIST @json_stage;
```

```
CREATE OR REPLACE TABLE cars_json_stage (
    data VARIANT
);
```

```
COPY INTO cars_json_stage(data)
FROM @json_stage
FILE_FORMAT = (TYPE = 'JSON');
```

```
INSERT INTO cars (id, first_name, last_name, car_make, car_model, car_model_year)
SELECT
    data:id::INT,
    data:first_name::STRING,
    data:last_name::STRING,
    data:car_make::STRING,
    data:Car_Model::STRING,
    data:Car_Model_Year::INT
FROM cars_json_stage;
```

```
SELECT * FROM cars;
```

