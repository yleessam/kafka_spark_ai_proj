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
