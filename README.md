# Data_Genki_Dama
> 사용할 개발 환경
>
> - Google Colab
> - Jupyter Notebook
> - PyCham

### 목차

**[1. PySpark in Google Colab](#PySpark-in-Google-Colab)**



## PySpark in Google Colab

- **Environment Set**

  ```python
  !apt-get install openjdk-8-jdk-headless -qq > /dev/null
  !wget -q https://downloads.apache.org/spark/spark-3.0.3/spark-3.0.3-bin-hadoop2.7.tgz
  !tar xf spark-3.0.3-bin-hadoop2.7.tgz
  !pip install -q findspark
  ```

  ```python
  import os
  os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64"
  os.environ["SPARK_HOME"] = "/content/spark-3.0.3-bin-hadoop2.7"
  ```

  ```python
  import findspark
  findspark.init()
  ```

  - 무작정 `import pyspark~`를 사용하다가 환경변수 설정이 필요한 걸 깨닫고, 상기처럼 환경설정을 해야 에러 없이 SparkSession 생성 및 각종 구문이 정상작동하는 것을 확인함.

- **File Upload and Read**

  ```python
  from google.colab import files
  files.upload()

  # "파일 선택" 버튼 눌러서 파일 업로드
  ```

  ```python
  from pyspark.ml.feature import VectorAssembler
  from pyspark.ml.regression import LinearRegression

  dataset = spark.read.csv('my-csv.csv',inferSchema = True, header = True)
  ```

  - PySpark의 경우, 하단의 항목들을 통해서만 데이터셋 로드 가능
    - 로컬에 있는 파일
    - HDFS
    - Cassandra HBase
    - Amazon S3
    - 그 밖에 Hadoop으로 지원 가능한 Storage

