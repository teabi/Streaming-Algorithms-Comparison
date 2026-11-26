
# 스트리밍 알고리즘 2종 구현 및 성능 비교

## 1. 프로젝트 소개

본 프로젝트는 대용량 데이터 스트림 환경에서 전체 데이터를 메모리에 저장하지 않고 데이터를 처리하는 스트리밍 알고리즘을 구현하고 성능을 비교하는 것을 목적으로 한다.

본 실험에서는 다음 두 가지 알고리즘을 구현하였다.

- Bloom Filter: 원소의 포함 여부를 확률적으로 판정
- Count-Min Sketch: 데이터 항목별 빈도를 근사적으로 추정

## 2. 데이터셋

- Dataset: MovieLens 1M
- Source: https://grouplens.org/datasets/movielens/1m/
- Records: 1,000,209
- Format: DAT
- Main file: ratings.dat

각 레코드는 다음과 같은 구조를 가진다.

UserID::MovieID::Rating::Timestamp

데이터는 한 줄씩 읽어 스트림 형태로 처리하였다.

## 3. 구현 알고리즘

### 3.1 Bloom Filter

Bloom Filter를 이용하여 사용자와 영화의 조합이 이미 등장했는지 확인하였다.

평가 항목:
- False Positive Rate
- False Negative
- Memory Usage
- Processing Time

### 3.2 Count-Min Sketch

Count-Min Sketch를 이용하여 영화별 평가 횟수를 근사적으로 계산하였다.

평가 항목:
- Mean Absolute Error (MAE)
- Relative Error
- Memory Usage
- Processing Time

## 4. 실험 환경

- Language: Python
- Platform: Google Colab
- Dataset: MovieLens 1M
- Libraries: hashlib, pandas, numpy, time

## 5. 실험 결과

### 5.1 Bloom Filter

| Bit Array | Hash Count | Memory (Bytes) | FPR (%) |
|---:|---:|---:|---:|
| 1,000,000 | 4 | 125,000 | 92.95 |
| 5,000,000 | 4 | 625,000 | 9.35 |
| 10,000,000 | 4 | 1,250,000 | 1.31 |

### 5.2 Count-Min Sketch

| Width | Depth | Memory (Bytes) | MAE |
|---:|---:|---:|---:|
| 5,000 | 3 | 60,000 | 10.2499 |
| 5,000 | 5 | 100,000 | 1.5774 |
| 5,000 | 7 | 140,000 | 0.3114 |
| 5,000 | 10 | 200,000 | 0.0092 |

## 6. 결론

실험 결과, Bloom Filter는 메모리 크기가 증가할수록 False Positive Rate가 감소하였다.

Count-Min Sketch는 Depth가 증가할수록 빈도 추정 오차가 감소하였다. 그러나 메모리 사용량도 함께 증가하였다.

따라서 스트리밍 알고리즘을 실제 서비스에 적용할 때는 정확도, 메모리 및 처리 시간 사이의 균형을 고려하여 적절한 파라미터를 선택해야 한다.

## 7. Repository 구성

- Streaming_Algorithms_Comparison.ipynb: Python 구현 및 실험 코드
- bloom_memory_fpr.png: Bloom Filter 메모리와 FPR 비교 그래프
- cms_memory_mae.png: Count-Min Sketch 메모리와 MAE 비교 그래프
- final_bloom_results.csv: Bloom Filter 실험 결과
- final_cms_results.csv: Count-Min Sketch 실험 결과
