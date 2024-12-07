# kafka_spark_ai_proj

# 시스템 아키텍처

```mermaid
graph TD
    subgraph Producer
        A[Kafka Producer<br>샘플 데이터 생성]
    end

    subgraph Kafka
        B[Kafka Broker<br>(input_topic)]
        C[Kafka Broker<br>(output_topic)]
    end

    subgraph Spark
        D[Structured Streaming<br>PySpark 애플리케이션]
        D --> E[ML 모델<br>(Logistic Regression)]
    end

    subgraph REST_API
        F[Django REST Framework<br>Prediction API]
    end

    subgraph User
        G[사용자 요청<br>(API Call)]
    end

    %% Data Flow
    A --> B
    B --> D
    D --> E
    E --> D
    D --> C
    C --> F
    G --> F
