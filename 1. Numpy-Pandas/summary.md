# Numpy-Pandas

## 데이터 프레임 생성

~~~python
col_name1 = ['col1', 'col2', 'col3']
list1 = [[1, 2, 3], [11. 12. 13]]
array1 = np.array(list1)

df_list1 = pd.DataFrame(list1, columns=col_name1)

# 딕셔너리 형태로 바로 넣어도 된다. (DataFrame(dict))
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

- row 방향으로 삭제
~~~python
titanic_df.drop([0, 1, 2], axis=0, inplce=True)

# index가 0, 1, 2인 row 삭제
~~~

## 인덱스
- 판다스의 index 객체는 RDBMS의 Primary Key와 유사하게 레코드를 고유하게 식별하는 객체이지만, RDBMS와는 다르게 컬럼명이 없고 연산도 불가능하다.
- DataFrame.index : index 객체만 추출
- reset_index() : 인덱스를 새롭게 연속 숫자 형으로 할당하고 기존 인덱스는 'index'라는 새로운 컬럼 명으로 추가 (인덱스 자체가 의미있는 값을 가질 때, 인덱스로 새로운 컬럼을 만들기 위해서 사용)

~~~python
titanic_reset_df = titanic_df.reset_index(inplace=False)
~~~

## 데이터 셀렉션 및 필터링
- 명칭(label) 기반 인덱싱 : 컬럼의 명칭을 기반으로 위치를 지정하는 방식 (loc[])
- 위치(Position) 기반 인덱싱 : 0을 출발점으로 하는 가로축, 세로축 좌표 기반의 행과 열 위치를 기반으로 데이터를 지정한다. 따라서 행, 열 위치값으로 정수가 입력된다. (iloc[])
- ix[]는 명칭 기반과 위치 기반 인덱싱을 함께 제공한다.

![인덱싱](https://user-images.githubusercontent.com/58073455/74100242-04f7f200-4b70-11ea-87ba-94ce11bf8ce2.PNG)









