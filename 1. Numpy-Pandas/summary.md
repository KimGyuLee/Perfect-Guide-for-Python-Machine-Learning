# Numpy-Pandas

## 데이터 프레임 생성

~~~python
col_name1 = ['col1', 'col2', 'col3']
list1 = [[1, 2, 3], [11. 12. 13]]
array1 = np.array(list1)

df_list1 = pd.DataFrame(list1, columns=col_name1)

# 딕셔너리 형태로 바로 넣어도 된다.
~~~

## 데이터 삭제
- row를 삭제할 때는 axis=0, column을 삭제할 때는 axis=1
- 삭제하는 두 가지 방법
 
 ~~~python
 # 원본 데이터를 바꾸지 않고 새로운 데이터 프레임 생성
 titanic_drop_df = titanic_df.drop('Age', axis=1, inplace=False)
 ~~~
 
~~~python
# 원본 데이터를 바꿈
titanic_df.drop('Age', axis=1, inplace=True)
~~~

- 여러 개 컬럼 삭제
~~~python
titanic_df.drop(['Age', 'Famliy_No'], axis=1, inplace=True)
~~~

## 인덱스
- 판다스의 index 객체는 RDBMS의 Primary Key와 유사하게 레코드를 고유하게 식별하는 객체이지만, RDBMS와는 다르게 컬럼명이 없고 연산도 불가능하다.
- DataFrame.index : index 객체만 추출
- reset_index() : 인덱스를 새롭게 연속 숫자 형으로 할당하고 기존 인덱스는 'index'라는 새로운 컬럼 명으로 추가

~~~python

~~~


