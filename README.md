# Calorie_prediction

## 칼로리 소모량 예측(DACON Basic)
### 설명
 - table 데이터를 활용한 회귀분석부터 다시 공부해보고자 데이콘에서 진행하는 'Basic 칼로리 소모량 예측 경진대회'에 참여
 - 마감 이틀 전 참여를 해서 gridsearchCV를 사용하여 kerasregression 모델의 하이퍼 파라미터 튜닝으로 Public RMSE 0.48434 88등/ Private RMSE 0.49537 등으로 마무리

### 과정
 + **데이터 설명**
   + 대회에서 제공하는 11개의 독립변수로 이루어진 7500개의 Train 세트와 타겟을 제외한 10개의 독립변수로 이루어진 7500개의 Test 세트를 사용
   + 컬럼명 : 'Exercise_Duration', 'Body_Temperature(F)', 'BPM', 'Height(Feet)', 'Height(Remainder_Inches)', 'Weight(lb)', 'Weight_Status', 'Gender', 'Age', 'Calories_Burned'
   + 데이터 전처리
     + 독립변수 중 단위 변환이 필요한 컬럼들에 대해서 변환 실행
     + 타겟 데이터 분리 및 학습데이터에서 타켓 컬럼 삭제
     + PolynomialFeatures를 사용하여 부족한 독립변수에 복잡도를 증가시키고 StandardScaler도 함께 적용하여 모델의 설명력을 높이는 용도로 사용
 + **모델링**
   + tensorflow의 kerasregressor를 모델로 선택
   + gridsearchCV 하이퍼파라미터 튜너를 사용하여 최상의 조합을 찾기 위한 교차검증 실시
   + 조건으로 제시한 조합들 중 최상의 조합을 사용한 모델 학습
   + 검증세트로 검증 실시
 + **테스트 결과**
   + Test 세트를 사용하여 칼로리 소모량 예측 실시
   + submission 으로 저장 후 submit, Public RMSE 0.48434 / Private RMSE 0.49537(종료 후 확인) 를 얻음

### 회고
  - 이번 대회 참여는 기초부터 다시보자는 마음으로 시작했지만 너무 늦게 참여해서 여러 모델을 시험해볼 수 없었다
  - 대회 마감 후 다른 분들의 코드를 리뷰할 기회가 있었는데 모두들 복잡한 모델이나 튜닝을 하기보다 간단한 선형모델을 사용했을 때 점수가 높았다고 해서, 더욱 아쉬웠다.
  - 시간이 없다고 생각하다보니 전처리에 대한 다양한 시도와 모델링에서도 baseline 모델을 설정하고 기초모델부터 돌려봤어야 했는데 그러지 못했다는 것이 크게 다가왔다.
  - 그리고 내가 모르던 라이브러리를 알게되었다. 몇몇 참가자분께서 pycaret의 Automl을 사용하였는데 다양한 모델의 예측을 한눈에 볼 수 있었다고 한다. 조만간 실험해보고 업데이트 할 생각이다.
---
### 프로젝트 회고 기반 고도화 작업 진행
 + 23.05.05
   + 기존에 올린 코드에 데이터 분석 내용 추가
 + 23.05.08
   + 대회 종료 이후 학습해본 모델 및 성능 비교
     |모델명|RMSE|baseline 기준 전처리 차이점|
     |:---:|:---:|:---:|
     |GridsearchCV kerasregressor|0.4805||
     |Linear Regressor|0.2983|PolynomialFeatures degree 2 -> 3 변경, interaction_only=True 추가|
     |Linear Regressor|0.2880|위 모델에서 Weight_Status 컬럼 삭제|
     |Linear Regressor|0.2874|위 모델에서 Height(cm) 컬럼 추가 삭제|
     |Linear Regressor|0.1505|위 모델에서 예측값 정수형 변환|
     |Cross Validation|0.2915|PolynomialFeatures degree 2 -> 3 변경, interaction_only=True 추가|
     |Cross Validation|0.2888|위 모델에서 Weight_Status 컬럼 삭제|
   

### 사용한 프로그래밍 언어 및 라이브러리
<img src="https://img.shields.io/badge/Python-blue?style=flat"/> <img src="https://img.shields.io/badge/scikit_learn-yellow?style=flat"/> <img src="https://img.shields.io/badge/tensorflow-orange?style=flat"/> <img src="https://img.shields.io/badge/matplotlib-orange?style=flat"/>


### 데이터 정보
 - **데이터**
   - Dataset : https://www.dacon.io/competitions/official/236097/data
