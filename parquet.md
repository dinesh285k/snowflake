
```
create schema parquet;
```
<img width="582" height="116" alt="image" src="https://github.com/user-attachments/assets/381e6c54-3a3a-4731-8c6c-f65100f74011" />


```
CREATE OR REPLACE STAGE PARQUET;
```
<img width="636" height="117" alt="image" src="https://github.com/user-attachments/assets/212800db-f4d7-48dc-bd08-400fff72824d" />

```
create file format parquet_format
type=parquet;
```
<img width="661" height="173" alt="image" src="https://github.com/user-attachments/assets/3c252e21-ac4f-48ca-a016-22a0f09c2024" />


```
CREATE OR REPLACE TABLE mt_car ( 
data VARIANT
);
```
<img width="691" height="170" alt="image" src="https://github.com/user-attachments/assets/9c3ffffd-99ba-426f-a8fa-6a3ba146b1dc" />


```
PUT 'file://D:\\aws project\\MT_cars.parquet' @PARQUET AUTO_COMPRESS=FALSE;
```
<img width="1177" height="132" alt="image" src="https://github.com/user-attachments/assets/c93faf85-689c-4391-ae64-b54b966f4d6c" />


```
COPY INTO mt_car
FROM @PARQUET/MT_cars.parquet
FILE_FORMAT = (TYPE = 'PARQUET');
```
<img width="1638" height="204" alt="image" src="https://github.com/user-attachments/assets/f129f39f-5a93-4c4f-8049-81943737ce4e" />



```
select * from table(infer_schema(LOCATION => '@parquet' , FILE_FORMAT => 'parquet_format' , FILES => 'MT_cars.parquet'));
```
<img width="1451" height="376" alt="image" src="https://github.com/user-attachments/assets/7854daf6-fea2-4f69-a17b-f9a217d06a38" />


```
CREATE OR REPLACE TABLE t_parquet_info (
    model TEXT,
    mpg REAL,
    cyl NUMBER(38, 0),
    disp REAL,
    hp NUMBER(38, 0),
    drat REAL,
    wt REAL,
    qsec REAL,
    vs NUMBER(38, 0),
    am NUMBER(38, 0),
    gear NUMBER(38, 0),
    carb NUMBER(38, 0)
);
```
<img width="780" height="423" alt="image" src="https://github.com/user-attachments/assets/1063dac5-b2ca-49c6-9f72-a9e11521d5d6" />


```
COPY INTO t_parquet_info
FROM @parquet/MT_cars.parquet
FILE_FORMAT = (TYPE = 'PARQUET')
MATCH_BY_COLUMN_NAME = CASE_INSENSITIVE;
```
<img width="1616" height="215" alt="image" src="https://github.com/user-attachments/assets/9bb25c22-e6bc-4ac9-bb4d-863facd75058" />

```
SELECT * FROM t_parquet_info LIMIT 10;
```

<img width="891" height="348" alt="image" src="https://github.com/user-attachments/assets/fdc70d57-89ed-44cd-a552-47b34f3841f6" />







