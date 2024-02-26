![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/04a65a28-62a0-4505-a55b-56b890dcb8ab)![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/9f70bdf4-a7a9-4edb-91b6-01715a306a1e)![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/0ec7d94d-5d5d-4bdb-9d7e-7bd92cb8756b)# Project-Pork-belly-classification-analysis-using-pork-belly-image-data
2023년 빅데이터 분석리더과정 딥러닝 프로젝트

## 팀소개
| 구분 | 이름   |
|------|--------|
| 멘토 | 안은석 |
| 팀장 | 강지훈 |
| 팀원 | 손옥희 |
| 팀원 | 장병용 |

## 프로젝트 소개
- 데이터: 돼지 700여마리의 통삼겹을 1.5cm 일정한 두께로 잘라 스캔한 1.8만여장의 이미지와 이미지 속 근육의 넓이를 계산 및 측정한 수치 데이터
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/b0b21719-1b36-42da-b5a8-485e6f6f8563)
- 분석개요:
    - 데이터 분석1: 근육&지방비율 데이터를 활용한 클러스터링 분석
    - 데이터 분석2: 세부 근육별 면적 데이터를 활용한 클러스터링 분석
    - 모델 구현 및 성능평가: 클러스터링된 삼겹살별 이미지 데이터를 활용한 딥러닝 분류모델 구현
- 프로젝트 과정

| No |            단계            |         세부         |         기여자         |
|:--:|:--------------------------:|:--------------------:|:----------------------:|
|  1 | 데이터 전처리              | 　                   | 강지훈, 손옥희, 장병용 |
|  2 | 데이터 표준화              | 　                   | 강지훈                 |
|  3 | 수치 기반 군집분석 및 검증 | k-means, k-medoids   | 강지훈, 손옥희, 장병용 |
|  4 | 이미지 전처리              | skimage, imageo               | 손옥희, 장병용         |
|  5 | 이미지 분류 모델링         | CNN, vgg16, resnet50 | 장병용                 |
|  6 | 모델 선정 및 튜닝          | CNN, vgg16, resnet50 | 장병용                 |

## 세부과정
### 1. 수치형 데이터 형변환 및 정제
1) 전처리 과정(29,903 -> 21,786 row)
    * 값이 0인 경우 `.` 으로 입력된 케이스 -> `.`을 0으로 변경
    * 상대 위치 변수 추가: 한 돼지에서 삼겹살 조각이 몇 번쨰 위치인지 반영하는 변수(0~1사이 값)
    * 전체면적(totalbelly) 근육면적(totalm), 지방면젹(totalf)이 0이거나 음수인 경우 제거
    * 결측값 제거
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/0138f323-4419-4af1-93f3-8ae1efb73cfc)
### 2. 최종 데이터와 변수
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/05fdb873-00fa-4f13-9f94-38913fc1aae7)

### 3. 수치형 데이터를 활용한 삼겹살 클러스터링 및 검증
1) 사용 변수: 깊은흉근 면적(deepm), 넓은등근 면적(latissimusm), 몸통피부근 면적(cutaneousm), 배곧은근 면적(rectusm), 배바깥경사근 면적(external), 배속경사근 면적(internalm), 기타면적(etca), 근육 면적(totalm), 지방 면적(totalf)
2) 데이터 표준화: 각 면적을 전체 면적으로 나눠 삼겹살에서 각 면적의 비율로 사용
3) 사용 알고리즘: k-means clustering, k-medoids clustering 중 k-menas 선택
4)  진행 순서: 적절한 군집 개수(k) 탐색(계층적 군집 분석의 덴드로그램과 Elbow Method 사용) → 군집 결과 확인
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/c427693e-29ae-412b-9150-a1e22946113a)

### 4. 클러스터링 검증 및 고찰
1) 클러스터링 결과 확인
    * 2개의 주성분을 통한 2차원 시각화(2개의 주성분 분산의 비율 97.3%)
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/1fa21df2-7789-43d7-b17d-faca5d1ffa86)
    * 각 변수들의 분포 확인
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/905cfeb9-ca3a-44d6-8ea5-ab4c55109caf)
    * 군집분석 고찰
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/4e7fd99e-e4c2-4b0f-af26-76316143f409)
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/1d4aafea-d796-4949-a0a0-cad025857a89)

### 5. 이미지 데이터의 전처리
1) 원본 이미지 18,025개의 이슈
    * 사업년도에 따라 이미지 파일의 용량 차이 존재
    * 고기 부위에 따라 부적합한 데이터 존재
    * 고기 스캔작업 중 휴먼에러가 발생한 케이스 존재
2) 진행한 전처리 과정
    * 훈련에 적합하도록 노이즈 제거 = 이미지에서 고기영역만 추출(Skimage)
    * 부적합한 이미지 제거
    * 이미지 규격의 통일
    * Clustering 결과와 이미지의 mapping
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/3efce7fb-0590-4e64-894b-6fc7b37ea07f)
    * 추출한 이미지에서 에러이미지 검출(Pillow)
        * 종이를 인식해서 추출하거나
        * 전체 고기 중 국소부위를 인식한 케이스 존재
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/a5652966-9b53-4a08-9ff9-542314c7c899)
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/588b5f48-0d25-4741-b622-dbf08ed69254)

### 6. 이미지 분류 모델 구축
1) 총 data set 15,486개
2) Train data 80%(12,499) / Test data 20% (3,125)
3) 1차 탐색(컴퓨팅파워 문제로 5,150개의 data로 1차 탐색 진행)
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/2dee1dc1-71cb-4634-be20-0a146ef540a5)

### 7. 모델 선정 및 튜닝
1) 전체 데이터로 2차 모델 후보군에 대해 input size 120과 150을 비교 
    * basic_cnn
    * vgg16
    * resnet50
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/88c3c79d-2e8b-4b61-af97-b47dc251943f)
2) 2차 모델평가 요약
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/4a37f78b-6a8e-426c-9d9a-15fbe3425329)
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/d9c6ee0e-e762-4849-a2c9-6ff52beab7d1)

### 8. 결론 및 반성
1) 결론
    1) 통삼겹살의 조각별 이미지 데이터에서 계산된 각 근육넓이 데이터로 삼겹살의 군집분석을 실시한 결과정부에서 추진하고 있는 웰빙삼겹, 풍미삼겹, 꽃삼겹 3개로 나누어 지되, 지방과 근육이 적절한 그룹이 하나 더 생김. (풍미형 꽃삼겹이라 가칭함)
    2) 신기하게도 각 클러스터는 해부학적으로 비슷한 위치들에 몰려있어 삼겹살 가장 윗부분(목살쪽)인 꽃삼겹, 삼겹살의 가장 끝부분(뒷다리부분)인 웰빙삼겹, 가운데부분인 풍미삼겹으로 나누어지는것을 확인
    3) 그럼에도 불구하고, 전신이 살코기인 웰빙형, 반대로 지방이 많은 풍미형 돼지도 있는 것으로 보임
    4) 클러스터 정보를 활용해 이미지정보로 “풍미/풍미형 꽃/꽃/웰빙” 삼겹 여부를 예측하는 모델링을 했고,Test Accuracy 기준 성능 0.74가량으로 출력됨
    5) 성능을 향상시키기 위해서는 앞서 언급한 ‘전신 풍미형 삼겹, 전신 웰빙형 삼겹’ 돼지를 제거해 표준형에 가까운 돼지들로 분석을 하면 좋은 결과가 예상되나, 아쉽게도 시간이 부족해 추가분석을 하지 못함
    6) 학술적으로 다가가기 위해서는 1.5cm 두께로 잘라진 이미지들을 척추단위로 표준화가 필요

2) 반성
    1) 프로젝트 주제가 이미지 관련이었으나 컴퓨팅 파워가 너무 제한적인 상황이라 다양한 모델 및 파라미터 튜닝을 시도할 수 없었던 점이 아쉬웠음
    2) 3가지 기본 모델에 2가지 input size로 variation을 주는 정도로도 시간이 빠듯해 모델 성능을 0.62정도에서 만족해야 했음
    3) 삼겹살 이미지 특성상 특정 사물의 이미지 분류와 다르게 이미지 색상 변화가 매우 디테일해서 분류 분석에 어려움이 있음
    4) 특징을 분석하는 컨볼루션 레이어와 은닉층을 재설계하여 모델링해보면 좋을 것 같음


</br>
</br>

## 빅데이터 분석 리더 집체교육 학습내용
- **1일차: 빅데이터 비즈니스 전략 및 사례**
    - 데이터 활용의  기술동향
    - 데이터 분석 방법론 및 분석 사례 연구
- **2일차: 분석 도구 학습(R)**
    - R 소개 및 설치
    - R 프로그래밍1
    - R 프로그래밍2
- **3일차: 데이터 분석 기초**
    - 모집단과 표본
    - 확률과 확률표본
    - 통계적 추론
    - 분포에 관한 추론(ANOVA, ANCOVA, MANOVA)
- **4일차: R을 활용한 분석**
    - 회귀분석
    - 주성분 분석
- **5일차: 시계열 분석**
    - 개요
    - STL
    - 지수 평활(단순, 이중, Holt-Winters)
    - ARIMA(비계절 ARIMA, 계절형 ARIMA)
    - 모형 평가 및 진단
- **6일차: 데이터 분석 기획 및 리터러시**
    - 데이터주의 Dataism
    - 데이터 분석 기획
    - 데이터 과제 발굴 방법
    - 데이터 분석 거버넌스
- **7일차: Machine Learning**
    - 기계학습개요
    - 기계학습의 분류
    - R interface to Keras
- **8일차: 비지도 학습법**
    - K-Nearest Neighbors 이론과 구현
    - 나이브 베이즈 분류 이론과 구현
    - 의사결정 나무 이론과 구현
- **9일차: 지도 학습법**
    - 앙상블 학습 개념과 종류(Bagging, Boosting, Random Forest)
    - Support Vector Machine 개념과 종류(선형 SVM, 비선형 SVM)
- **10일차: 인공신경망 및 딥러닝**
    - 인공 신경망 개념
    - 딥러닝 개념
    - CNN 이론과 구현
    - RNN 이론과 구현
