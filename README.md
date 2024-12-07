# 시스템 아키텍처

```mermaid
graph TD
    subgraph Producer
        A[Kafka Producer: 샘플 데이터 생성]
    end

    subgraph Kafka
        B[Kafka Broker - input_topic]
        C[Kafka Broker - output_topic]
    end

    subgraph Spark
        D[PySpark Streaming Application]
        D --> E[Machine Learning Model: Logistic Regression]
    end

    subgraph REST_API
        F[Django REST Framework API]
    end

    subgraph User
        G[User Request - API Call]
    end

    %% Data Flow
    A --> B
    B --> D
    D --> E
    E --> D
    D --> C
    C --> F
    G --> F


## 추가 다이어그램: Django와 PySpark 통합 구조

아래는 Django와 PySpark가 같은 환경에서 구성된 구조를 설명한 다이어그램입니다:

```mermaid
graph TD
    A[AWS EC2 Instance] --> B[Ubuntu OS]
    B --> C[Python & Conda]
    C --> D[Django Application]
    C --> E[PySpark Environment]

    D -->|Gunicorn| F[Nginx]
    F -->|HTTP Requests| G[Users]

    E --> H[Spark Jobs]
    H --> I[Data Sources]
    I --> J[Hadoop HDFS or S3]

    G -->|Trigger| D
    D -->|Submit Spark Jobs| E
    E -->|Process Data| H
