# 시스템 아키텍처

```mermaid
graph TD
    subgraph Producer
        A[Kafka Producer - 샘플 데이터 생성]
    end

    subgraph Kafka
        B[Kafka Broker (input_topic)]
        C[Kafka Broker (output_topic)]
    end

    subgraph Spark
        D[Structured Streaming - PySpark 애플리케이션]
        D --> E[ML 모델 - Logistic Regression]
    end

    subgraph REST_API
        F[Django REST Framework - Prediction API]
    end

    subgraph User
        G[사용자 요청 - API Call]
    end

    %% Data Flow
    A --> B
    B --> D
    D --> E
    E --> D
    D --> C
    C --> F
    G --> F
