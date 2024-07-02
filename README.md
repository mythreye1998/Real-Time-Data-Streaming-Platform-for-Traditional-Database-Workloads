{\rtf1\ansi\ansicpg1252\cocoartf2758
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;\f1\fswiss\fcharset0 Helvetica-BoldOblique;\f2\fswiss\fcharset0 Helvetica-Oblique;
\f3\fswiss\fcharset0 Helvetica-Bold;\f4\fswiss\fcharset0 ArialMT;\f5\froman\fcharset0 Times-Roman;
}
{\colortbl;\red255\green255\blue255;\red0\green0\blue0;}
{\*\expandedcolortbl;;\cssrgb\c0\c0\c0;}
\margl1440\margr1440\vieww28600\viewh17440\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 Streaming Data for Traditional Database Workload\
\
\
The project focuses on implementing a streaming setup for traditional database using TPC-H benchmark. \
Streaming Platform : Apache kafka\
Database : Postgres\
Dataset : TPC-H\
\
Our project is implemented in different phases :\

\f1\i\b  Setting Up Your Environment:
\f0\i0\b0 \
Install PostgreSQL: Ensure you have a working installation of PostgreSQL.\
Set Up a Streaming Platform: Choose and set up a streaming platform (Apache Kafka ) that will feed data into PostgreSQL.\
Commands :\
\'97Intiate Zookeeper server :/Downloads/kafka_2.12-3.6.0$ bin/zookeeper-server-start.sh config/zookeeper.properties\
\'97Kafka serve : ~/Downloads/kafka_2.12-3.6.0$ bin/kafka-server-start.sh config/server.properties\
\'97CREATE KAFKA TOPIC : /Downloads/kafka_2.12-3.6.0/confluent-7.5.2/bin/sh kafka-topics --create --topic tpch --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1\
\'97LIST TOPIC : /Downloads/kafka_2.12-3.6.0/confluent-7.5.2/bin$ sh kafka-topics --list --bootstrap-server localhost:9092\
\'97Schema Registry property : ~/Downloads/kafka_2.12-3.6.0/confluent-7.5.2$ bin/schema-registry-start etc/schema-registry/schema-registry.properties ( edit the properties )\
\'97CREATED A "CONFIG file" UNDER confluent-7.5.2 which has
\f2\i  connect-avro-standalone_postgres.properties
\f0\i0  and 
\f2\i sink-quickstart-Postgres.properties.\

\f0\i0 \'97UPDATE PLUGIN.PATH IN : 
\f2\i home/voohitha/Downloads/kafka_2.12-3.6.0/confluent-7.5.2/config/connect-avro-standalone_postgres.properties 
\f3\i0\b as
\f2\i\b0  plugin.path=share/java,/home/voohitha/Downloads/kafka_2.12-3.6.0/confluent-7.5.2/share/java/kafka-connect-jdbc,/home/voohitha/Downloads/kafka_2.12-3.6.0/confluent-7.5.2/share/java ( 
\f0\i0 for 
\f2\i connect-avro-standalone_postgres.properties)\
\'97UPDATE PROPERTIES  under sink-quickstart-Postgres.properties.
\f0\i0 \
TPC-H Dataset: Obtain the TPC-H dataset or use tools to generate this data.\
\'97 Modified makefile in dbgen \
\pard\pardeftab720\qj\partightenfactor0

\f4\fs26\fsmilli13333 \cf0 \expnd0\expndtw0\kerning0
\outl0\strokewidth0 \strokec2 CC\'a0 = gcc (compiler., prefers using c compiler as makefile is written in c)
\f5\fs24 \

\f4\fs26\fsmilli13333 DATABASE = POSTGRES ( name of the database that is used)
\f5\fs24 \

\f4\fs26\fsmilli13333 MACHINE\'a0 = LINUX (operating system )
\f5\fs24 \

\f4\fs26\fsmilli13333 WORKLOAD = TPCH
\f5\fs24 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0 \cf0 \kerning1\expnd0\expndtw0 \outl0\strokewidth0 \'97 Converted data records to .csv file.\
\pard\pardeftab720\qj\partightenfactor0

\f4\fs26\fsmilli13333 \cf0 \expnd0\expndtw0\kerning0
\outl0\strokewidth0 \strokec2 >\'a0 \'a0 csv_file="$\{tbl_file%.tbl\}.csv"
\f5\fs24 \

\f4\fs26\fsmilli13333 >\'a0 \'a0 sed 's/|$//g' "$tbl_file" | awk -F '|' 'BEGIN \{OFS=","\}
\f5\fs24 \

\f4\fs26\fsmilli13333 \'a0\'a0\'a0\'a0\'a0\'a0\{print $0\}' > "$csv_file".
\f0\fs24 \kerning1\expnd0\expndtw0 \outl0\strokewidth0 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f1\i\b \cf0 Design the Streaming Data Model
\f0\i0\b0 \
Streaming Data Ingestion: Implement a method to continuously ingest TPC-H data into your streaming platform.\
\'97 Implemented a producer.py file to read the data from  TPC-H tool kit  and push it to kafka topic\

\f1\i\b Integrate PostgreSQL with the Streaming Platform
\f0\i0\b0 \
Data Push Mechanism: Develop a mechanism to push data from the streaming platform to PostgreSQL.\
\'97 Implemented a consumer.py file to push the data continuously from kafka topic to Postgres. \
Real-time Query Execution: Ensure PostgreSQL can execute queries in real-time as data streams in.\
\'97 Transform the TPC-H query to Postgres queries\

\f1\i\b Performance Evaluation
\f0\i0\b0 \
Benchmarking: Run the modified TPC-H queries against your streaming setup.\
}
