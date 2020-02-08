# Numpy-Pandas

* **데이터 삭제**
  - row를 삭제할 때는 axis=0, column을 삭제할 때는 axis=1
 
 삭제하는 2가지 방법
 
 ~~~python
 # 원본 데이터를 바꾸지 않고 새로운 데이터 프레임 생성
 titanic_drop_df = titanic_df.drop('Age', axis=1, inplace=False)
 ~~~
 
~~~python
# 원본 데이터를 바꿈
titanic_df.drop('Age', axis=1, inplace=True)
~~~

