# Data Provenance in Distributed Machine Learning

> [Paper](https://link.springer.com/chapter/10.1007/978-3-030-41418-4_19) | No Code?

**Data Delineation**: crucial aspect of distributed machine learning.

**Data Lineage**: considers what data is missing, who uses it and what happens (is it modified, updated...). 

The pipeline monitors user input, collects information and handles data storage. The pipeline uses UDF (user defined functions) to process data. These are a set of steps of data processing (both intermediate and final data). Generates event logs to the pipeline, then data is stored dumped. 

- PM collects information from the pipeline and stores it in a database.
- PM assigns an unique identifier to each data item and evaluates the data and processing.
- Data service handles the storing of data and the processing of data.
- Elastic search gets data from logs and historical data.
- Trustworthyness of data is evaluated by the PM.
- DML is based on SparkSQL and keeps track of the data lineage and records the data logs. 
- PySpark is modified to increase accuracy. 

To train the model, Stellargraph is used: reads the generated data logs from RDD and PySpark. (and gives resulting logs)

This work tests the trustworthiness of pipeline before training the model.

Keeps overhead under 20% and is able to handle 1000s of data logs. But is higher on compelx queries.

Uses ElasticSearch (paid product) and is not open source. Stellargraph is free and open source, but is not the main focus of the paper and needs provenance retrieval.
Competitors are **Akka** (I think?)  and **Orleans** (couldn't find anything online) (less support for data recovery). 

This tool also has no code available I could find...