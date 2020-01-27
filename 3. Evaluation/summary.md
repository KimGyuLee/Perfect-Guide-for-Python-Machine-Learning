# Evaluation - Classification 성능 평가 지표
회귀보다는 분류, 특히 이진분류일 때 여러가지 성능 지표들을 다 고려해야 한다. 회귀는 성능 지표들이 실제값과 예측값이 얼마나 차이가 나는지에 대해 일관적으로 구성되어 있다. 0이냐 1이냐, 사망이냐 생존이냐, 양성이냐 음성이냐를 분류하는 이진분류는 다양한 성능지표를 고려하는데, 정확도는 이진 분류에서 잘 사용하지 않는다. 성능 지표들을 살펴보면, 오차행렬을 가지고 정밀도와 재현율을 도출하고, 정밀도와 재현율이 얼마나 균형잡혀있는지를 f1 score를 통해 확인한다. 특히 이진분류일 때, roc와 auc를 성능 지표로 많이 활용한다.  

# 1. Accuracy - 정확도  
![accuracy_formula](https://user-images.githubusercontent.com/58073455/73163518-804eb200-4133-11ea-9006-142a508372c4.PNG)

* 정확도는 직관적으로 모델 예측 성능을 나타내는 평가 지표이다. 하지만 이진 분류의 경우 데이터의 구성에 따라 ML 모델의 성능을 왜곡할 수 있기 때문에 정확도 수치 하나만 가지고 성능을 평가하지 않는다.  

* 특히 정확도는 불균형한 레이블 값 분포에서 ML 모델의 성능을 판단할 경우, 적합한 평가 지표가 아니다.  

* 예를 들어, 신용카드 사기검출을 위한 전체 데이터 개수가 10,000 건일 경우, 9,900 건은 '정상'이고 100 건, 즉 1% 만 '사기'라고 할 때, 모든 데이터를 '정상'으로 예측한다고 하더라도 정확도는 99% 가 나온다.  


# 2. Confusion Matrix - 오차행렬  
![confusion_matrix](https://user-images.githubusercontent.com/58073455/73163888-2ef2f280-4134-11ea-8f08-89c49881521d.PNG)

* 이진 분류의 예측 오류가 얼마인지와 더불어 어떠한 유형의 예측 오류가 발생하고 있는지를 함께 나타내는 지표이다.  

* **TN (True Negative)** : 예측을 Negative로 했는데, 맞은 것 (True) - 실제는 Negative  
* **FN (False Negative)** : 예측을 Negative로 했는데, 틀린 것 (False) - 실제는 Positive  
* **FP (False Positive)** : 예측을 Positive로 했는데, 틀린 것 (False) - 실제는 Negative  
* **TP (True Positive)** : 예측을 Positive로 했는데, 맞은 것 (True) - 실제는 Positive  

![confusion_matrix2](https://user-images.githubusercontent.com/58073455/73164834-0cfa6f80-4136-11ea-98e4-c74dd9c32217.PNG)

* TP는 0이다. Positive로 예측한 것이 한 건도 성공하지 못했다.
* 더불어 FP가 0이므로 Positive로 예측 자체를 수행하지 않았음을 알 수 있다.

![accuracy_formula2](https://user-images.githubusercontent.com/58073455/73164948-4337ef00-4136-11ea-9b4f-9753f4043027.PNG)

* Positive로 예측 자체를 수행하지 않았음에도 불구하고, 레이블 값의 불균형으로 인하여 정확도가 90% 가 나온다.


# 3. Precision - 정밀도
![precision](https://user-images.githubusercontent.com/58073455/73165189-b04b8480-4136-11ea-883d-855a0ac1daa3.PNG)

* 정밀도는 예측을 Positive로 한 대상(FP+TP) 중에, 예측과 실제 값이 Positive로 일치한 데이터(TP)의 비율을 뜻한다.  

* FP가 낮아야 정밀도가 올라간다. (Positive로 예측했으나 실제값은 Negative인 건수)  

* 사이킷런에서 precision_score() 제공  


# 4. Recall - 재현율
![recall](https://user-images.githubusercontent.com/58073455/73165300-e5f06d80-4136-11ea-801f-0eacbd3b3fa5.PNG)

* 재현율은 실제 값이 Positive인 대상(FN+TP) 중에, 예측과 실제 값이 Positive로 일치한 데이터(TP)의 비율을 뜻한다.

* FN이 낮아야 재현율이 올라간다. (Negative로 예측했으나, 실제값은 Positive인 건수)

* 사이킷런에서 recall_score() 제공  

* 정밀도와 재현율 둘다 TP를 분자로 갖지만, 정밀도는 예측을 Positive로 한 대상을 분모로, 재현율은 실제값이 Positive인 대상을 분모로 한다는 차이가 있다.  


## 정밀도와 재현율의 trade-off
* 업무에 따른 재현율과 정밀도의 상대적 중요도  
 - 정밀도가 상대적으로 더 중요한 지표인 경우는 실제 Negative 음성인 데이터 예측을 Positive로 잘못 판단(FP)하게 되면 업무상 큰 영향이 발생하는 경우이다. ex. 스팸메일  
 
 - 재현율이 상대적으로 더 중요한 지표인 경우는 실제 Positive 양성인 데이터 예측을 Negative로 잘못 판단(FN)하게 되면 업무상 큰 영향이 발생하는 경우이다. ex. 암 진단, 금융사기 판별  



# 5. F1 Score


# 6. ROC Curve & AUC

