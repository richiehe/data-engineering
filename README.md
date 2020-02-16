# Data-Engineering

此Repo总结了一些数据工程的概念，经验以及代码实践，内容会在后续会慢慢完善并且增加

### 数据概念
- [大数据5V](docs/data_concepts/Characteristics-of-Big-Data.md)
- 什么是ETL
- Source vs Sink
- 什么是Orchestration
- 批处理 vs 流处理 
- 架构对比：Lambda vs Kappa
- Spark相关概念
- Kafka相关概念
- 流处理相关概念


### 开发环境准备
- 本地设置Python虚拟环境 - pyenv
- 本地设置Python虚拟环境 - pipenv
- 在PyCharm IDE上配置python虚拟环境
- 在本机搭建Spark
- 搭建Databricks环境
- 搭建AWS EMR环境
- 在本地搭建HDFS
- 在本地搭建Airflow

### 数据处理
- 用Spark运行简单的Word Count
- 常用的Spark语法汇总

### 自动化测试
- pytest
- Spark自动化测试实例

### 数据处理集成实例
- Azure Data Lake Gen 2 -> Databricks -> Azure Data Lake Gen 2
- S3 -> EMR -> S3
- Kafka -> Elasticsearch -> Kibana
- Spring Boot -> Kafka -> Spark
- Airflow调度Spark程序

### 机器学习入门

### 环境问题解决
- [Spark与Kafka集成问题](/docs/issues/Spark-Kafka-Integration-Issue.md)