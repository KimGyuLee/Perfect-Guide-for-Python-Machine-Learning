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

- 행 위치와 인덱스 명칭(RangeIndex)이 같을 경우에는 ix[0,1]에 오류가 발생하지 않지만, 위의 그림과 같이 행 위치와 인덱스 명칭이 다를 경우 오류가 발생한다. ix[0,1]은 명칭과 위치 중 명칭부터 찾기 때문에 행에서 RangeIndex:0 이 없으므로 오류를 발생시키는 것이다.
- 명칭 기반, 위치 기반 모두 헷갈리기 때문에 가능하면 불린 인덱싱을 사용하는 것이 좋다.

## example
~~~ python
titanic_df[['Survived', 'Pclass']]  # 여러 컬럼을 추출할 때에는 리스트 형태로 넣을 것
~~~

~~~python
titanic_df.iloc[0,0]  # 위치 기반

titanic_df.loc['one', 'Nmae']  # 명칭 기반
~~~

~~~python
titanic_boolean = titanic_df[titanic_df['Age']>60]  # 불린 인덱싱
~~~

~~~python
titanic_df[titanic_df['Age']>60][['Name', 'Age']]
# 'Age'>60 조건에 맞는 'Name', 'Age' 컬럼만 추출

titanic_df[['Name', 'Age']][titanic_df['Age']>60]  # 위와 동일
~~~

~~~python
titanic_df[ (titanic_df['Age']>60) & (titanic_df['Pclass']==1) & (titanic_df['Sex']=='female') ]
~~~

~~~python
cond1 = titanic_df['Age'] > 60
cond2 = titanic_df['Pclass']==1
cond3 = titanic_df['Sex']=='female'
titanic_df[cond1 & cond2 & cond3]
~~~

## Aggregation 함수 & Group by
- Aggregation 함수 호출 시 axis 값을 명시하지 않으면 axis=0과 같은 결과를 출력한다.
![aggregation](https://user-images.githubusercontent.com/58073455/75559082-2f114580-5a86-11ea-938c-622996d449a1.PNG)

~~~python
titanic_df[['Age', 'Fare']].sum(asix=0) # 행축 방향으로 sum, 결론적으로는 column의 합계
~~~
~~~python
titanic_df[['Age', 'Fare']].sum(axis=1) # 열축 방향으로 sum, 해당 컬럼의 모든 row의 합계
~~~
~~~python
titanic_df.groupby('Pclass')['Age'].sum()
~~~
~~~python
titanic_df.groupby('Pclass')['Age'].agg([max, min])  # 여러 함수를 적용하는 방법
~~~
~~~python
# 컬럼별로 다른 함수를 적용하는 방법
agg_format={'Age':'max', 'SibSp':'sum', 'Fare':'mean'}
titanic_df.groupby('Pclass').agg(agg_format)
~~~

## Pivot
~~~python
pd.pivot_table(DataFrame, index='기준일자', columns='성별', values='이용금액')
~~~
![피벗](https://user-images.githubusercontent.com/58073455/75560738-13f40500-5a89-11ea-85bf-d7262fee3107.png)

## lambda식
~~~python
# 일반함수
def get_square(a):
    return a**2

print('3의 제곱은:', get_square(3))
~~~

![람다식](https://user-images.githubusercontent.com/58073455/75563695-1b69dd00-5a8e-11ea-93fe-d90938b8f21b.PNG)

~~~python
# 람다식
lambda_square = lambda x : x**2

print('3의 제곱은:', lambda_square(3))
~~~

- apply lambda 식으로 데이터 가공
~~~python
titanic_df['Name_len'] = titanic_df['Name'].apply(lambda x : len(x))
# 'Name' 컬럼에 있는 인자들이 하나씩 x로 들어오면, len(x) 즉, x의 길이가 자동으로 리턴된다.
~~~

~~~python
titanic_df['Child_Adult'] = titanic_df['Age'].apply(lambda x : 'Child' if x <= 15 
else ('Adult' if x <=60 else 'Elderly'))
# 'Age' 의 값이 15 이하이면 'Child'를 반환하고, 나머지 중에서 60 이하이면 'Adult'를 반환하고, 
그 외에는 'Elderly'를 반환한다.
~~~
