## 인코딩
### 레이블 인코딩
~~~python
from sklearn.preprocessing import LabelEncoder

items = ['tv', '냉장고', '컴퓨터', '선풍기']

# LabelEncoder를 객체로 생성한 후, fit()과 transform()으로 label 인코딩 수행
encoder = LabelEncoder()
encoder.fit(items)
labels = encoder.transform(items)
~~~

~~~python
# 인코딩 클래스 확인
encoder.classes_
~~~


### 원-핫 인코딩
~~~python
# 사이킷런의 원-핫 인코딩은 복잡(labelencoder -> 2차원 변환 -> 원-핫 인코딩)
# pandas 함수를 사용하는 것이 쉽다.
pd.get_dummies(DataFrame) 
~~~
