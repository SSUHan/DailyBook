# Pandas 시작하기

pandas 의 개발 방향

* 자동적으로 혹은 명시적으로 축의 이름에 따라 데이터를 정렬할 수 있는 자료구조
* 잘못 정렬된 데이터에 의한 일반적인 오류를 예방
* 다양한 소스에서 가져온 다양한 방식으로 색인되어 있는 데이터를 다룰 수 있는 기능
* 통합된 시계열 기능
* 시계열 데이터와 비시계열 데이터를 함께 다룰 수 있는 통합 자료 구조
* 누락된 데이터를 유연하게 처리할 수 있는 기능
* SQL 같은 일반 데이터베이스처럼, 데이터를 합치고 관계연산을 수행하는 기능



## Pandas 의 자료 구조

* Series
* DataFrame



### Series

일련의 객체를 담을 수 있는 1차원 배열 같은 자료구조(어떤 NumPy 자료형이라도 담을 수 있다)

색인을 가지고 있는 **연관배열**과 같다.

> obj = Series([4,7,-5,3])
>
> obj.values
>
> obj.index



시리즈 객체를 만듬과 동시에 색인 지정도 가능

> obj2 = Series([4,7,-2,4], index=['d','a','b','c'])



Series 를 이해하는 다른 방법은 **고정길이의 정렬된 사전형** 이라고 이해할 수 있다.

> 'b' in obj2



파이썬 사전 객체로 부터 Series 객체를 생성할 수 있다.



Pandas 의 isnull, notnull 함수는 누락된 데이터(NaN) 을 찾을때 이용한다.



다르게 색인된 데이터에 대한 산술연산이 가능하다.



### DataFrame

표 같은 시프레드시트 형식의 자료 구조로 여러 개의 칼럼이 있는데, 각 칼럼은 서로 다른 종류의 타입을 담을 수 있다.

색인의 모양이 같은 Series 객체를 담고있는 사전타입이라고 이해할 수 있다.



DataFrame 의 객체를 생성하는 일반적인 방법은, **같은 길이의 리스트에 담긴 사전** 을 이용하거나 **NumPy 배열** 을 이용할 수 있다.

> frame = DataFrame(data, index=['one', 'two','three', 'four'], columns=['year', 'state', 'pop', 'debt'])
>
> frame.columns
>
> frame.year # year 칼럼 데이터가 반환
>
> frame.ix['three']   # index:three 에 대한 row 가 반환



*DataFrame 의 색인을 이용해서 생성된 칼럼은 내부 데이터에 대한 뷰 일 뿐이며, 복사가 일어나지 않는다*

*따라서 이렇게 해서 얻어낸 Series 객체에 대한 변형은 실제 DataFrame 에 적용이 된다. 이를 원치 않는다면 copy 메서드를 이용한다*



Series 와 유사하게 values 속성은 DataFrame 에 저장된 데이터를 2차원 배열로 반환한다.

> frame.values



## Pandas 의 핵심기능

### 재색인

reindex 는 새로운 색인에 맞도록 객체를 새로 생성하는 기능이다.

reindex를 호출하면 데이터를 새로운 색에 맞게 재배열하고, 없는 색인 값이 있다면 NaN 을 추가한다.

> obj2 = obj.reindex(['a','b','c','d','e'], fill_value=0) # NaN 이 0으로 채워진다.
>
> obj3.reindex(range(6), method='ffill') # 앞의 값으로 누락된 값을 채운다. 뒤에 것으로 채우려면 bfill



### 하나의 Row or Column 삭제하기

> new_obj = obj.drop(['c','d'])



### 슬라이싱

> obj[2:4] # 라벨의 시작점과 끝점까지 포함한다는 점에서는 파이썬 슬라이싱과 다르다
>
> obj[obj['three'] < 2]



### DataFrame 산술연산

두 DataFrame 은 + 연산이 가능하다.

색인이 같으면 산술하고, 색인이 매칭되지 않는다면 NaN이 된다.

이를 디폴트값을 채워넣고 싶다면, fill_value= 예약어를 사용하면 된다.

> df1.add(df2, fill_value=0)  # 이렇게도 더할 수 있다.



### 함수 적용과 매핑



### 정렬과 순위



### 기술통계 계산과 요약



### 상관관계와 공분산



## 누락된 데이터 처리하기

* dropna : 누락된 데이터가 있는 축(row, column) 을 제외시킨다. 어느 정도의 누락데이터까지 용인할 것인지 조절 할 수있다.
* fillna : 누락된 데이터를 대신할 값을 채우거나 'ffill', 'bfill' 같은 메서드를 적용할 수 있다.
* isnull : 누락되거나 NA인 값을 알려주는 Boolean 형태의 값이 저장된 객체를 반환한다.
* notnull : isnull 과 반대되는 메서드이다. 





## 계층적 색인

