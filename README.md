# geeks2-hive
GEEKS 2 : HIVE

## 0) Start HDFS & Yarn

หากยังไม่ได้ start service ให้ start ก่อน ด้วยคำสั่ง
```
start-dfs.sh && start-yarn.sh
```

## 1) นำไฟล์เช้า HDFS

สร้าง directory ชื่อ hospital_info_data และนำไฟล์ hospital_info.csv เข้าไปใส่ไว้ข้างใน
```
hadoop fs -mkdir hospital_info_data
hadoop fs -put hospital_info.csv /user/student/hospital_info_data
```

## 2) Start service ของ Hive Server

start service ด้วยคำสั่ง คือ
```
hiveserver2
```

## 3) ใช้ dbeaver เชื่อมต่อมายัง Hive Server

เปิด Dbeaver เลือก Apache Hive และระบุการเชื่อมต่อดังนี้

```
Host : <ip ของ vm>
Username : student
```

## 4) สร้าง Table 

```
CREATE EXTERNAL TABLE IF NOT EXISTS hospital_info (
  hospcode INT,
  name STRING,
  address STRING,
  moopart STRING,
  tmbpart STRING,
  amppart STRING,
  chwpart STRING,
  area_code STRING,
  tmbpart_text STRING,
  amppart_text STRING,
  chwpart_text STRING,
  zipcode STRING,
  hosptype STRING,
  hosptype_text STRING,
  sss_code STRING,
  sss_code_text STRING,
  hospital_phone STRING,
  hospital_fax STRING,
  date_report STRING,
  date_update STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
location '/user/student/hospital_info_data'
tblproperties ("skip.header.line.count"="1");
```

## 5) ทดลอง Query ข้อมูล

```
SELECT * FROM hospital_info LIMIT 3;
```
