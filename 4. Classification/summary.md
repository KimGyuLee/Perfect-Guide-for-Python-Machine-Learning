## 앙상블
- 앙상블의 유형은 일반적으로 보팅(Voting), 배깅(Bagging), 부스팅(Boosting)으로 구분되며, 이외에 스태킹(Stacking) 등의 기법이 있다.
- 대표적인 배깅은 랜덤 포레스트 알고리즘이며, 부스팅은 에이다 부스팅, 그래디언트 부스팅, XGBoost, LightGBM 등이 있다. 정형 데이터의 분류나 회귀에서는 GBM 부스팅 계열의 앙상블이 전반적으로 높은 예측 성능을 보인다.
- 넓은 의미로는 서로 다른 모델을 결합한 것들을 앙상블로 지칭하기도 한다.

### 보팅 (Voting) & 배깅 (Bagging)
- 보팅과 배깅은 여러 개의 분류기가 투표를 통해 최종 예측 결과를 결정하는 방식이다.
- 보팅과 배깅의 다른 점은 보팅의 경우 일반적으로 서로 다른 알고리즘을 가진 분류기를 결합하는 것이고, 배깅의 경우 각각의 분류기가 모두 같은 유형의 알고리즘 기반이지만, 데이터 샘플링을 서로 다르게 가져가면서 학습을 수행해 보팅을 하는 것이다.
- 보팅 ex. Linear Regression + K Nearest Neighbor + Support Vector Machine  -> 투표
- 배깅 ex. Decision Tree + Decision Tree + Decision Tree -> 투표


