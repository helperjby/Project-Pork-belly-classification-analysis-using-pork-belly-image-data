# Project-Pork-belly-classification-analysis-using-pork-belly-image-data
2023년 빅데이터 분석리더과정 딥러닝 프로젝트

## 팀소개
| 구분 | 이름   |
|------|--------|
| 멘토 | 안은석 |
| 팀장 | 강지훈 |
| 팀원 | 손옥희 |
| 팀원 | 장병용 |

## 프로젝트 소개
- 데이터: 돼지 700여마리의 통삼겹을 1.5cm 일정한 두께로 잘라 스캔한 3만여장의 이미지와 이미지 속 근육의 넓이를 계산 및 측정한 수치 데이터
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
1. 수치형 데이터 형변환 및 정제
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/0138f323-4419-4af1-93f3-8ae1efb73cfc)
    * 전처리 과정(29,903 -> 21,786 row)
        * 값이 0인 경우 `.` 으로 입력된 케이스 -> `.`을 0으로 변경
        * 상대 위치 변수 추가: 한 돼지에서 삼겹살 조각이 몇 번쨰 위치인지 반영하는 변수(0~1사이 값)
        * 전체면적(totalbelly) 근육면적(totalm), 지방면젹(totalf)이 0이거나 음수인 경우 제거
        * 결측값 제거
2. 최종 데이터와 변수
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/c9e745b7-8df0-4574-b7a6-58709990bc89)
3. 수치형 데이터를 활용한 삼겹살 클러스터링 및 검증
    * 사용 변수: 깊은흉근 면적(deepm), 넓은등근 면적(latissimusm), 몸통피부근 면적(cutaneousm), 배곧은근 면적(rectusm), 배바깥경사근 면적(external), 배속경사근 면적(internalm), 기타면적(etca), 근육 면적(totalm), 지방 면적(totalf)
    * 데이터 표준화: 각 면적을 전체 면적으로 나눠 삼겹살에서 각 면적의 비율로 사용
    * 사용 알고리즘: k-means clustering, k-medoids clustering 중 k-menas 선택
    * 진행 순서: 적절한 군집 개수(k) 탐색(계층적 군집 분석의 덴드로그램과 Elbow Method 사용) → 군집 결과 확인
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/c427693e-29ae-412b-9150-a1e22946113a)
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/9b083290-ddba-45d1-85a3-b6391c4e505f)
4. 클러스터링 검증 및 고찰
![image](https://github.com/helperjby/Project-Pork-belly-classification-model-using-pork-belly-image-data/assets/69462995/a16f8abe-c89c-480d-9355-4aea8b319266)

5. 이미지 데이터의 전처리
6. 


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
