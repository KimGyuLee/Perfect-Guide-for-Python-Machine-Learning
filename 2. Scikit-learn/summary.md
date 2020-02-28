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

## 스케일링
### 표준화
- 평균이 0이고 분산이 1인 정규분포 형태로 변환
~~~python
scaler = StandardScaler()
scaler.fit(df)
df_scaled = scaler.transform(df)
~~~

### 정규화
- 서로 다른 피처의 크기를 통일하기 위해 크기를 변환
- MinMaxScaler는 데이터 값을 0과 1 사이의 범위 값으로 변환한다.
~~~python
scaler = MinMaxScaler()
scaler.fit(df)
df_scaled = scaler.transform(df)
~~~
