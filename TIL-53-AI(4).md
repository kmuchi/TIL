
### kafka
" 이벤트 스트리밍 플랫폼"
```
사용자 주문 발생 → 
  - 결제 시스템에 알려야 함
  - 재고 시스템에 알려야 함  
  - 배송 시스템에 알려야 함
  - 데이터 분석 시스템에 보내야 함
  - 추천 모델 학습 데이터로 쌓아야 함
```

- 각 시스템이 서로 호출하면 엉킴
- 각 시스템 kafka 구독하고 있다가, 주문 이벤트 오면 알아서 자기 일 함.

### Redis
- DB느리니까 RAM에 데이터 캐싱

### Spark
- 하둡보다 빠름
- API 쓰기 쉬움

### 분산처리
1. 저장 분산
    - 큰 파일 쪼개서 -> 저장
2. 연산 분산
    - 쪼개진 데이터 어떻게 병렬로 처리 -> 결과 합침

| 카테고리 | 비관리형 (직접 설치) | 관리형 서비스 |
| --- | --- | --- |
| 관계형 DB | EC2에 MySQL 설치 | AWS RDS, GCP Cloud SQL |
| NoSQL | EC2에 MongoDB | AWS DocumentDB, MongoDB Atlas |
| 캐시 | EC2에 Redis | AWS ElastiCache, Upstash |
| 메시지 큐 | EC2에 Kafka | AWS MSK, Confluent Cloud |
| 분산 연산 | EC2에 Spark 클러스터 | AWS EMR, Databricks |
| 쿼리 엔진 | 하둡 + Hive 직접 구축 | AWS Athena, BigQuery, Snowflake |
| 검색 | EC2에 Elasticsearch | AWS OpenSearch, Elastic Cloud |
| 함수 실행 | EC2에 웹 서버 | AWS Lambda, Cloudflare Workers |