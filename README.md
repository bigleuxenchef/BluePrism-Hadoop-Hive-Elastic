# BluePrism-Hadoop-Hive-Elastic
This project aims at testing and providing insight on how to integrate BluePrism with Hadoop and Elasticsearch Stack
As I am a fa experimenting, I like to install everything by myself, this is a way to get to understannd thing under the hood. Here are the list of sofware installed in my sand box for this project :

- Hadoop 2.7.3
- Spark 2.2.1
- Hive 2.1.0
- Oozie 4.3.0 (optional)
- Hue 3.12.0
- Elastic 6.x, Kibana 6.x

# Testing Hadoop/Hive

First make sure you have everything you need in *hadoop*, I use *hue* tool s very friendly rather than the *hadoop* command shell. Furthermore as we are going to use hive as the proxy to get access to all data, it is important to visualize that everything works fine.

## Hue

<img src="./images/hue-3.12.0.png" width=100% align="middle">

## Sample of using Hive to access Elastic table from Hue

<img src="./images/hue-elastictable.png" width=100% align="middle">

## Sample using shell beeline to get to hive.

<img src="./images/beeline-hive.png" width=100% align="middle">






