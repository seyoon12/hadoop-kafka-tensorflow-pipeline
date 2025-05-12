# hadoop-kafka-tensorflow-pipeline
음성 데이터 수집 분석 End-to-End 빅데이터 AI 아키텍처

## 1. 개요
본 프로젝트는 실시간 음성 데이터 수집부터 대용량 저장, 텍스트 변환, AI 분석, 시각화까지의 엔드 투 엔드 빅데이터 AI 플랫폼 구축을 목표로 한다.

### 1.1 목표
Kafka 기반 실시간 음성 메타데이터 수집

Hadoop 기반 대용량 음성 파일 저장

Spark 기반 배치 전처리 및 STT 변환

Hive/Presto 기반 텍스트 분석 SQL 처리

TensorFlow 기반 자연어 처리(NLP) 분석

Zeppelin 기반 분석 결과 시각화

### 1.2 아키텍처 구성도
[Client App] → [Kafka] → [Kafka Connect HDFS Sink] → [Hadoop HDFS]
      ↓                               ↑
[음성 메타데이터 전송]                [음성 파일 저장]

[Batch Spark Job] → [STT 변환 (Vosk/Google)] → [Hive/Presto (SQL 분석)]
         ↓
[TensforFlow NLP 분석]
         ↓
[분석 결과 저장 및 Zeppelin 시각화]

### 1.3 주요 기술 스택
구성 요소	기술명
메시징	Kafka, Kafka Connect
스토리지	Hadoop HDFS
배치 처리	Spark
메타스토어	Hive Metastore
SQL 분석	Presto
시각화	Zeppelin
AI 분석	TensorFlow, STT Engine (Vosk/Google STT)
스케줄러	Oozie (옵션)
모니터링	OpenTSDB (옵션)

### 1.4 데이터 흐름
Kafka (Producer)
음성 파일 경로 또는 음성 데이터 메타 정보 발행
                 ↓
Hadoop HDFS (Kafka Connect Sink)
원본 음성 파일 저장
                 ↓
Spark Batch + Vosk
HDFS에 저장된 WAV 파일 불러오기

Vosk STT 처리
텍스트 결과 재저장 (HDFS / Hive 테이블)
                 ↓
Hive / Presto
텍스트 데이터 SQL 조회 및 분석
                 ↓
TensorFlow NLP
Hive/Presto에서 불러온 텍스트 기반 감정 분석/키워드 추출
                 ↓
결과 데이터 저장 (HDFS / Hive)
Zeppelin / Hue



