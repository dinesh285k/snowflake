# snowflake

# login with command prompt 
```
snowsql -a <account identifier> -u <user_name>
```

<img width="810" height="234" alt="image" src="https://github.com/user-attachments/assets/26753dd7-3157-4119-8601-83f5f9a1c029" />


```
CREATE OR REPLACE STAGE cars_json_stage;
```

```
PUT file:///C:/path_to_your_folder/*.json @cars_json_stage;
PUT 'file://D:\\aws project\\car.json' @cars_json_stage AUTO_COMPRESS=FALSE; unzip the file
```

```
LIST @cars_json_stage;
```
<img width="806" height="243" alt="image" src="https://github.com/user-attachments/assets/ce9b5f45-0e10-41ba-96e3-f7d479ab7262" />


```
CREATE OR REPLACE FILE FORMAT json_format
  TYPE = 'JSON';
```
<img width="821" height="172" alt="image" src="https://github.com/user-attachments/assets/09955603-6467-4342-bc29-6ab32d5af7cb" />


```
CREATE OR REPLACE TABLE cars_json (
    data VARIANT
);
```
<img width="773" height="204" alt="image" src="https://github.com/user-attachments/assets/cc20a53d-3a2f-4c91-b5d5-de7616352e0e" />


```
COPY INTO cars_json(data)
FROM @cars_json_stage
FILE_FORMAT = (TYPE = 'JSON');
```

```
COPY INTO cars_json(data)
FROM @CARS_JSON_STAGE/car.json
FILE_FORMAT = (TYPE = 'JSON');
```

<img width="1641" height="198" alt="image" src="https://github.com/user-attachments/assets/aa59956e-bae7-47b2-b108-dd641e94f3d6" />


```
SELECT * FROM cars_json LIMIT 2;
```
<img width="765" height="443" alt="image" src="https://github.com/user-attachments/assets/a4b6d5b1-3541-445c-9112-e301fbc5032b" />


```
INSERT INTO cars_json (id, first_name, last_name, car_make, car_model, car_model_year)
SELECT
    data:id::INT,
    data:first_name::STRING,
    data:last_name::STRING,
    data:car_make::STRING,
    data:Car_Model::STRING,
    data:Car_Model_Year::INT
FROM json_stage;
```

```
SELECT * FROM cars;
```

