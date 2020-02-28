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


