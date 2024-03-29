# ML 기초
> Machine Learning (인공지능) 기초학습   

<br>

## Jupyter Notebook 사용 tip
1. shift + tab + tab : 함수설명
2. Command + 좌우 >> 문장 끝으로 이동 / alt + 좌우 : 문단 끝으로 이동
3. x = 행삭제
4. z = 행삭제 취소


<br><br>

## Numpy/ Pandas 코드

```python
 1. 함수 및 메서드
    type(): 자료형 정보 (list, array 등) 
    .dtype : 데이터 타입정보 (int, float 등)
    df.select_dtypes("object") : df 데이터 중 'object'타입의 데이터들만 추출
    .iloc[:, df.dtypes =='int64'] : 상동
    .reset_index : 인덱스 초기화
    .value_counts()
    .sort_values(by=[''])
    .tolist()

 2. 펜시 인덱싱 (리스트로 감싸줘야함)
    df.iloc[[0,3,5,7],[3,5,7]]
    df.loc[0:3,['name','age','salary']] 
     (loc: 0-3 또한 숫자형이 아닌 문자열로 인덱싱 된 것이다.)

 3. 부울 인덱싱
    df_hk.loc[df_hk['age']>30, :] #행선택을 조건문으로 줄수도 있다. 
 
 4. 어떠한 값이라도 문자로 처리할때 따옴표 3개
    '''abc'''
    """abc""" 
 
 5. a = [1,2,3], b = [4,5,6] 일 때, 
    a + b = [1,2,3,4,5,6] 으로 출력된다.
    행렬계산을 하기 위해선 1차원 배열로 바꿔줘야한다. 
    a = np.array[1,2,3] , b= array[4,5,6]
    a + b = [5,6,9]

 6. 튜플은 하나의 원소일때도 뒤에 ,를 꼭! 붙여줘야 함 (3,) 아니면 숫자형으로 인식됨 (3)

 7. print 와 return의 차이점  
    return은 결과값을 또 값으로 받아서 다른 곳에서 활용 가능 , 프린트는 단순 출력만

 8. 라이브러리 설치
   [terminal]  
      pip install tensorflow
   [jupyter notebook] \
      !pip install tensorflow
   또는
      import os
      os.system('pip install tensorflow')

 9. 불린인덱스는 loc만 사용가능 / iloc은 불가
   result = df_food.drop(columns=['state'])
   len(result[(result['cook_time']>0) & result['prep_time']>0])

 10. 범위로 배열 생성
    range (리스트)
    np.arange(배열)
    
 11. n개 column 에 대한 aggregation
         df_hk[['age','salary']].agg(['mean','sum','count'])
     n개 column 에 대한 n개 aggregation_각각 요약정보를 다르게 출력하고 싶을때 딕셔너리 이용
     이때 1개 column에 2개 이상 aggregation을 적용하면 마지막 aggregation이 적용 (age : max적용됨)
         df_hk[['age','salary']].agg({'age':'mean', 'age':'max', 'salary':'max'})
     두개를 다 사용하고 싶다면, 아래 방법 활용 (각각 열을 정의하여 생성)
         df_hk[['age','salary']].agg(age_mean = ('age','mean'), age_max = ('age','max'), sal_cnt = ('salary','count'), sal_median = ('salary','median'))


 12. ML돌릴때 하나로도 결측치가 있으면 에러나게된다. Merge_key값으로 조인시 결측치가 없는지 확인이 필요

 13. replace 또는 map #dict활용 
     df_hk['gender'].replace({'F':'Female' ,'M':'Man'})

 14. Lambda
     df_hk['jumin7'].apply(lambda x : '19'+ x[0:6])

 15. 등급화 : np.where 또는 cut 이용

      #np.where (엑셀 if문과 동일)
      np.where(df_hk['age'] < 30,'30미만',
            np.where(df_hk['age']<=40, '40대','50대이상'))[:10]
      # cut
      pd.cut(x = df_hk['age'], bins = [0,20,30,40,100], labels = ['10대', '20대', '30대', '40대이상'], right= True)
      * right = True : 오른쪽 값을 해당구간에 포함하는게 T, 다음 구간에 포함하는게 F 
                       즉, 이하인지 미만인지 
      
      bins수 (구간이다보니) > label수

 16. datetime(날짜)형으로 변환 2가지 방법
     pd.to_datetime(df_hk['jumin7'], format = '%y%m%d-%w')
     .astype('datetime64')

     활용
      # datetime 활용
      df_hk['birthday'] = df_hk['jumin7'].apply(lambda x : '19'+ x[0:6]).astype('datetime64')
      df_hk['birthday'].dt.year
      df_hk['birthday'].dt.month
      df_hk['birthday'].dt.day
      df_hk['birthday'].dt.weekday #월요일은 0
      df_hk['birthday'].dt.day_name() #day_name은 ()필요

 17. Array 배열생성
     np.array([1,2,3]) #배열 생성
     np.zeros((3,3)) # 0원소로만 구성된 3 by 3 행렬
     np.zeros((3,3)) # 9원소로만 구성된 3 by 3 행렬
     np.eye(3) #단위행렬(대각행렬) 생성
     
18.  Array 관련 함수
     .ndim #차원확인
     .reshape(-1,3) #차원변경
     .size #원소개수
     .flatten() #다시 1차원으로 펼쳐줌


19. Numpy 난수 생성
    np.random.seed(42)
    np.random.choice(np.arange(1,45),size = (5,6), replace = True) #replace = True, 복원추출 
    np.random.choice(np.arange(1,45),size = (5,6), replace = False) #replace  =False, 비복원추출
    np.random.shuffle(array)

20. 내적
   - 전제조건 : M1의 열의 수 M2의 행의 수가 같아야함
   - 결과값의 크기 : M1의 행의 크기 X M2의 열의 크기
   - 행렬곱은 교환법칙이 성립하지 않는다. (앞뒤가 바뀌면 결과값이 다르다.)
   - 단순 쩜곱은(곱하기연산) 교환법칙 성립함


    M1 = np.array([2,4,6,8]).reshape(2,2)
    M2 = np.array([3,5,7,9]).reshape(2,2)

   #방법1
   M1.dot(M2)

   #방법2
   np.dot(M1,M2)

   #방법3
   M1@M2

     

 18. 장바구니 분석시 판매량이 제일 많은 날 찾기
     [‘Date’].value_counts().idxmax()

 19. 날짜데이터에서 요일 한글로 추출하기
      dt.day_name(locale=‘ko_kr’)

 20. 데이터 프레임에서 연속된 인덱스 슬라이싱하여 제거하기
      DF.drop(DF.index[23:53], inplace=True)

```
<br><br>

## Series 와 DataFrame
[Series] :  Pandas의 1차원
 1) 함수 및 메서드
      A = pd.Series([1,2,3])
      A.values
      A.index
      A.idxmax(최대값의 위치)
      A.isin([1,2])

[DataFrame] : 1차원 Series를 모아놓은 것 Pandas의 2차원 
 1) 함수 및 메서드
   Crosstab  
    - 두변수를 조합하여 살펴볼때 사용하는 pandas 함수 (빈도표)
    - normalize 인자에 True,1,0값을 할당하여 값을 정규화할수있음
      pd.crosstab(df['aa'], df['bb'])


      pd.DataFrame([1,2,3], [4,5,6]], columns = ['A', 'B', 'C'])
      pd.DataFrame({'A':[1,4], 'B':[2,5], 'C':[3,6]})
      pd.DataFrame(np.arange(6).reshape(2,3) +1 , columns=['A','B','C'])

<br><br>

## 통계
 1. mode
    ```python
    from scipy.stats import mode
    mode(array) #mode : 최빈값 (빈도값이 모두 동일 할 때는 첫번째 값 리턴), count : 빈도수)
    ```


 2. [조건부확률]은 crosstab을 활용하여 푼다.<br> (범주형 자료의 빈도표, 수치형 자료의 경우 상관관계 crosstab이용) <br>
    ```pd.crosstab(df['a'], df['b'])```

 3. [중심극한 정리 증명]
      ```python
      import matplotlib.pyplot as plt
      import numpy as np
      import random


      avg_values = []
      for _ in range (1,10000): # 횟수를 증가시키면 정규분포로 변화 (10000번 반복)
         random_sample = random.sample(range(1, 1000),100) #1~1000까지 숫자를 100개 뽑아서
         x = np.mean(random_sample) #평균 산출
         avg_values.append(x) #평균값 저장

         plt.hist(avg_values, bins = 100) #10000개의 평균값으로 분포그래프 확인
         plt.show()
      ```

<br><br>

## 표본추출

1. 단순임의추출
2. 층화표본추출 (의료-코호트분석)
3. 계통추출
    - 첫표본을 무작위로 추출하고 표집간격 k만큼 떨어진 곳에서 데이터 추출
4. 군집추출

```Basic Code_ Random Sampling``` 
  > 샘플 추출은 단순임의 추출이 기본이지만, groupby 를 사용하면 층화 표본추출 기능을 구현할 수 있다. <br>
Sklearn - train_test_split
df_train, df_test = train_test_split(df, test_size = 0.3, random_state = 42)

1)  pandas - sample() <br>
   n= 표본개수 frac= 비율, random_state = 표본추출결과를 고정
   Replace : 복원추출 여부, weights : 가중치
   파라미터 n 과 frac은 동시사용은 불가 ```(frac은 비율로 추출 0.005등)``` <br>
      ```python
      df.groupby('season').sample(n=2, random_state= 42) >> 층화추출기능
      ```


2) scikit-learn <br>
   ```python
      from sklearn.model_selection import train_test_split

      df_train, df_test = train_test_split(df, test_size = 0.3, random_state = 42)
   ```
   <br><br>


```표본 추출 방법별 코드```

* ###   Random sampling
   ```python
   from sklearn.model_selection import train_test_split
   x_train, x_test = train_test_split(df_hk, test_size =0.3, random_state=42)
   x_train[:5]
   ```

* ### Sytematic sampling
  ```python
   df_idx = df_hk.reset_index()

   x_train = df_idx[(df_idx['index'] % 5 != 0)]
   x_test = df_idx[(df_idx['index'] % 5 == 0)]
   ```

* ### Cluster sampling
   ```python
   df_cluster = df_hk[df_hk['company'] =='A']
   df_cluster
   ```
* ### Stratified Random Sampling
   ```python
   df_hk['company'].value_counts()

   pd.crosstab(df_hk['company'], df_hk['gender'])
   ```
<br><br>

## 데이터 전처리

   <b>함수 및  메서드</b>
   ```python
    1.  .isna(), .isnull(), .notna(), .notnull() 
      # null 과 NaN과 na은 동일하다고 봐도 무관

        df.notna().sum(axis = 1)

    2. .fillna()
       df = df.fillna(value = {'Sepal_Width':df['Sepal_Width'].mean()}) 
       또는
       df['Sepal_Width'] = df['Sepal_Width'].fillna(df['Sepal_Width'].mean())
       round(df.var(),3)

    3. .select_dtypes()
       df.select_dtypes('float64').isnull().sum().sum()


    4. Outlier (평균+ 1.5 표준편차일때)
       mean = df3['Sepal.Length'].mean()
       std = df3['Sepal.Length'].std()
       len(df[(df3['Sepal.Length'] > mean+ (1.5*std))|(df3['Sepal.Length'] < mean- (1.5*std))])

    5. 조건 추출 numpy - where()함수
       a = np.where(df['Sepal_Length'] >= 3)

       np.where(df_hk['age'] < 30,'30미만',
            np.where(df_hk['age']<=40, '40대','50대이상'))[:10]

       #조건으로 범주 나눌때 npwhere, 조건으로 추출시 loc 
      
    6. 변수명 바꾸기 
       [특정 컬럼 변경 : pandas - .rename() 사용]
       df4 = df4.rename(columns = {'is_setosa':'is_seto'})
       Data로 접근후 파라미터에서 컬럼 지정

       [데이터 전체 일괄 변경 : pandas - .columns 사용]
       df4.columns = ['name', 'gender', 'height', 'age', 'blood_type', 'company']

    7. .astype('type명')

    8. .apply(lambda x : x, )

    9. .str.slice(0:4)
       문자열 슬라이싱

    10. to_datetime(a)
    
      a= df5[df5['casual']>25]['datetime'] #필터링
      b = pd.to_datetime(a)
      b.dt.date.nunique()
      bike_time = pd.to_datetime(bike['date time'][:3])
      bike_time.dt.year
      bike_time.dt.month
      bike_time.dt.hour
      bike_time.dt.date

    11. 더미변수화
      pd.get_dummies (data, columns= [''], drop_first =True) #get_dummies는 가변수 대상은 없앰
      #drop_first를 사용하지않고 가변수를 모두 활용할 경우, 완전공선성 등 여러가지 문제 발생
    
    12. reset_index(drop = True) : 기존의 인덱스를 초기화 하는 메서드 + 동시에 series를 데이터프레임으로 바꿔주는 역할도 함 
    (drop = True : 기존 인덱스 제거)

    13. .set_index('컬럼명') : 특정변수를 인덱스로 지정할 경우 사용하는 메서드, 데이터 병합 또는 시계열 분해에서 연산을 위해 활용

    14. 최대값을 가진 행의 인덱스를 구할때 idxmax()

      [예제1]
      df5['datetime']=pd.to_datetime(df5['datetime'])
      df5['hour']= df5['datetime'].dt.hour
      df5.groupby('hour')['registered'].mean().idxmax()

      [예제2]
      a= bike[(bike['season']==2)].groupby(bike['datetime'].dt.hour)['registered'].mean()
      b= bike[(bike['season']==4)].groupby(bike['datetime'].dt.hour)['registered'].mean()
      abs(a-b).idxmax()

    15. Binding연산 (행 또는 열 연산가능) : pandas- concat() 

      pd.concat([bike1, bike2.reset_index(drop = True)], axis = 1).reset_index(drop=True)

    16. Join연산 : pandas- merge()

      pd.merge(left = df_a, right = df_b , left_on = 'member', right_on = 'name',
            how = 'inner')
    17. crosstab() : wide form >> clustering(군집화) 알고리즘에 사용됨

      pd.crosstab(dia['cut'],dia['clarity'], normalize =True).round(2)
      
      # normalize =True : 바로 조건부 확률로 확인이 가능
      # normalize 는 True/ False 외에 1,0도 있다
      # normalize = 1: 열기준으로 정규화 / 0 : 행기준

      #cut과 clarity 별로 가격의 평균
      pd.crosstab(dia['cut'],dia['clarity'], values =dia['price'], aggfunc = pd.Series.mean)
      
      #위의 내용의 long form 버젼 (결과값은 동일)
      dia.groupby(['cut', 'clarity'])['price'].mean().reset_index()
  
  18. melt()
   wide form 데이터프레임을 Long Form으로 자료구조를 변환하는 메서드, id_vars 인자에 기준이 되는 변수를 지정하여 처리 <br>
   
   크로스탭에서 melt 사용 시에는 기존 인덱스화 되어있는 열을 reset_index()를 통해 열 먼저 되돌려 주고 melt 함수 사용

   elec_melt = elec.melt(id_vars= ['YEAR','MONTH','DAY'])
   elec_melt

 19. pivot()
   Long form 데이터 프레임을 wide form으로 자료구조를 변환하는 메서드
   Index / columns/ values 인자에 각각 대상변수를 지정하여 출력데이터 구조를 결정 <br>
   crosstab의 value + aggregate function와 기능이 동일하지만, 피벗이 더 많이 쓰임 <br>
   또한 군집분석 실시 전 데이터 전처리에 주로 활용됨
   (pivot()은 pv 실행만, pivot_table()은 요약 연산까지)
 20. between(2005,2007) : 2005~2007 까지 
 
 21. nlargest(5) 큰순서대로 상쉬 5개 추출 

 22. drop()
   
   # drop 은 데이터 단위로 접근 
   # 1. dropna은 subset 이용
     df_hk_na= df_hk_na.dropna(subset ='age')

   # 2. drop(row index 사용)으로 삭제
     df_hk.drop(index = df_hk[(df_hk['expenditure'] < min) | (df_hk['expenditure'] > max)].index
  
   # 2-1(중요!!). drop 대신 반대조건으로 필터링 가능 
     df_hk[(df_hk['expenditure'] >= min) & (df_hk['expenditure'] <= max)]
     
     [참고] (행추출시 'NOT'은 ~ 로 사용 가능)
     df_ds = df_ds[(~df_ds['last_new_job'].isin(['>4', 'never']))]

   # 3. 그외 columns 사용하여 삭제 가능

   23. .pow(2) : 지수연산 (2일때는 제곱)
        ** 와 동일 (**0.5 는 루트가 된다)

   ```

 
     

  
   <br><br>

 ## 데이터 시각화

 ```import matplotlib.pyplot as plt``` <br>
 ```import seaborn as sns ```<br><br>

 ## #1. histogram 

<b>[matplotlib]</b> <br>
속성값 참고 : https://matplotlib.org/stable/api/markers_api.html
```python
figure = plt.figure(figsize=(5, 4), facecolor ='pink')
plt.plot([0,1,2,3],[1,4,9,12], color = 'red', marker = 'o', markersize = 3,
         linestyle ='dashed', linewidth = 0.5)
plt.plot([0,1,2,3],[10,20,30,40], color = 'gray', marker = '', markersize = 8,
         linestyle ='solid', linewidth = 0.5)

plt.xlabel('x_label')
plt.ylabel('y_label')
plt.title('matplotlib chart')


plt.show()
```
<br><br>
<b>[seaborn]</b> <br>

* seaborn의 histogram은 histplot과 displot이 대표적이며 histplot은 axes레벨, displot은 figure레벨임
```python
# seaborn histogram histplot
figure = plt.figure(figsize = (3,2))
sns.histplot(df_hk['age'], kde=True) 
#kde:추청선 보여주기
sns.histplot(x='age', data=df_hk, kde=True, bins=30)
```
 <br>

## #2. distplot

<b>[seaborn]</b> <br>
   ```python
   # seaborn histogram distplot 확률밀도함수(추정선)
figure = plt.figure(figsize = (3,2))
sns.distplot(df_hk['age'])
```
 <br>

## #3. countplot
<b>[seaborn]</b> <br>
   ```python
plt.figure(figsize=(4, 3))
sns.countplot(x='company', data=df_hk)
```
 <br>

## #4. barplot
<b>[matplotlib]</b> <br>
```python
# bar 값을 만들어야 함

plt.figure(figsize=(4, 3))
a_mean = df_hk[df_hk['company'] == 'A'].salary.mean()
b_mean = df_hk[df_hk['company'] == 'B'].salary.mean()
c_mean = df_hk[df_hk['company'] == 'C'].salary.mean()
X = df_hk['company'].unique()

plt.bar(x=X, height=[a_mean,b_mean,c_mean])
plt.xticks([0,1,2],['company A','company B','company C']) # plt.xticks([0,1,2] 눈금간격
plt.show()
```
<b>[seaborn]</b> <br>
* seaborn barplot y값 default mean으로 계산 (sum, median 변경 가능)

```python
plt.figure(figsize=(3,2))
sns.barplot(data = df_hk, x= 'company', y= 'salary')


#confidence interval을 없애고, color를 green으로 통일, 평균외에 총합/ 중앙값으로 표현. 
# hue 인자를 사용하여 x값 세분화 (남/여 데이터로 한번 더 나누기) #x,y축 데이터 바꿔주면 축 바꿔서 그려줌
# estimator= np.median, np.sum

plt.figure(figsize=(3,2))
sns.barplot(data = df_hk, x= 'company', y= 'salary', estimator='sum', ci=None ,color='green', hue='gender')

```
## #5. boxplot
<b>[matplotlib]</b> <br>
```python
# matplotlib boxplot, x(범주형), y(연속형)
plt.figure(figsize=(3,4))
plt.boxplot(x= df_hk[['age','height']],data=df_hk)
plt.show

# matplotlib boxplot, x(범주형), y(연속형)
a_age = df_hk[df_hk['company']=='A']['age']
b_age = df_hk[df_hk['company']=='B']['age']
c_age = df_hk[df_hk['company']=='C']['age']

plt.figure(figsize=(3,4))
plt.boxplot([a_age, b_age, c_age])
plt.show
```

<b>[seaborn]</b> <br>
```python
# seaborn boxplot, x(범주형), y(연속형)에 대한 4분위값을 표현
plt.figure(figsize=(3,4))
sns.boxplot(data=df_hk, x= 'company' ,y='age')

# hue 인자를 사용하여 x값 세분화
plt.figure(figsize=(3,4))
sns.boxplot(data=df_hk, y= 'company' ,x='age', hue='gender')
```
<br>

## #6. Pie Chart
<b>[matplotlib]</b> <br>
```python
plt.figure(figsize=(3,4))
a_count = df_hk[df_hk['company'] == 'A'].company.count()
b_count = df_hk[df_hk['company'] == 'B'].company.count()
c_count = df_hk[df_hk['company'] == 'C'].company.count()

plt.pie(x = ([a_count,b_count,c_count]), 
        labels=(['company A','company B','company C']), autopct='%.1f%%') # autopct 전체 백분율, ' %.2f '는 소숫점 2자리

plt.show()
```
## #7. Scatter Plot
<b>[seaborn]</b> <br>

```python
#hue 인자를 사용하여 x값 세분화
sns.scatterplot(df_hk, x= 'age', y='salary',hue='company')
```
<b>[python-plot]</b> <br>
```python
plt.figure(figsize=(3,4))
df_hk.plot.scatter(x= 'age' , y='salary')
```

## #8. heatmap
<b>[seaborn]</b> <br>
```python
#DataFrame의 corr()은 숫자형 값만 상관도를 구함> 상관도를 먼저 구해야됨

# annotation(주석) 인자로 상관계수 표시
plt.figure(figsize=(4,4))
corr=  df_hk.corr()
sns.heatmap(corr, annot = True)
#DataFrame의 corr()은 숫자형 값만 상관도를 구함

```
<br><br>

# 가설검정
- X : 범주형 , Y : 범주형 ⇒ 카이스퀘어 검정
- X : 범주형 , Y : 수치형 <br>
      ⇒ 범주형 그룹수가 2개이하 : ttest <br>
      ⇒ 범주형 그룹수가 3개이상 : ANOVA

<br><br>

## <b>T-TEST 검정</b>
> 두 집단간의 평균비교

<br>

<b>1.  t_test_1sample</b>

* t-test를 할 data의 mean 근처의 값으로 t-test후 t통계량과 p_value 관찰 #모집단 평균을 알고 있음
* <b> popmean: 모집단의 추정모수  즉, 𝒎₁</b> <br>
*  모평균과 가까워질수록 통계량은 낮아지고 p-value가 올라간다. <br>
*  Scipy -ttest_1samp() 사용 <br>
```활용: 객단가 평균이 00라고 알려져있다. 사실인가?```
  
   ```python 
   from scipy.stats import ttest_1samp
   ttest_1samp(df_hk['age'], popmean = 39.24)[1] < 0.05  

   # 결과값 : TtestResult(statistic=0.0, pvalue=1.0, df=249)
   1.0 < 0.05
   # 결과 : False, 결과 해석: 95% 신뢰수준으로 100% 일치
   ```

<br><br>
<b>2. Two sample t-test</b>

* 다른환경 (주말/주중) 즉, 독립된 모집단에서 추출된 각 두 집단간 평균이 같은지 검정
* 등분산 여부에따라 검정통계량 계산식이 달라서 등분산 검정을 해줘야한다.
* 등분산 검정 (Bartlett test) 
   - h0 : 등분산이다, h1 : 이분산이다
   - 유의수준 0.05보다 pvalue가 작을때 귀무가설 기각
* 등분산을 만족할 경우, equal_var = True , 이분산일때 equal_var = False
   ```python
   #두그룹으로 나누기
   g_m = df[(df['gender'] =='Male')]['forehead_ratio']
   g_f = df[(df['gender'] =='Female')]['forehead_ratio']

   from scipy.stats import ttest_ind , bartlett

   #등분산검정
   bartlett(g_m, g_f) #귀무가설 기각 : 이분산
   #t검정
   ttest_ind(g_m, g_f,  equal_var = False) #이분산 False
   ```



* 정규성을 만족하지 못하는 경우 wilcoxon rank sum test (순위합검정) 사용
* 독립일때 ttest_ind() 사용 <br>
```활용: 주중 객단가와 주말 객단가가 같은가?```

```python
from scipy.stats import ttest_ind
ttest_ind(df_hk[(df_hk['company']=='A')].salary , df_hk[(df_hk['company']=='B')].salary)

#결과 : Ttest_indResult(statistic=5.941362455469809, pvalue=1.2532322871358408e-08)

```


2-1.  sample t-test (A>=B) #less_ A(𝒎₀)보다 B(𝒎₁)가 작다 (하단측검정)
   ```python
   ttest_ind(df_hk[(df_hk['company']=='A')].salary , df_hk[(df_hk['company']=='B')].salary,
         alternative='less')

   #결과값: Ttest_indResult(statistic=5.941362455469809, pvalue=0.9999999937338386)
   ```

2-2. sample t-test (A<=B) #greater_ A(𝒎₀)보다 B(𝒎₁) 가 크다(상단측검정)
   ```python
   ttest_ind(df_hk[(df_hk['company']=='A')].salary , df_hk[(df_hk['company']=='B')].salary,
            alternative='greater')

   #Ttest_indResult(statistic=5.941362455469809, pvalue=6.266161435679204e-09)
 ```

 > 예제 
 1) iris 데이터를 사용하여('iris.csv') species column 'virginica'의 'sepal_width' 모평균이 3.14와 같은지 가설을 수립하고 유의수준 0.05에서 검정하시오
      ```python
      # H0 : 'virginica'의 'sepal_width' 모평균이 3.14 와 같다고 볼 수 있다 (유의수준 0.05)
      # H1 : 'virginica'의 'sepal_width' 모평균이 3.14 와 같다고 볼 수 없다 (유의수준 0.05)
      #df_iris['sepal_width'].mean()
      from scipy.stats import ttest_1samp, ttest_ind

      ttest_1samp(df_iris['sepal_width'], popmean = 3.14)[1] < 0.05
      #결과값:  True = H1 지지, H0 기각
      ```
 2) 'setosa'와 'versicolor'의 sepal_length 평균이 같은지 가설을 수립하고 유의수준 0.05에서 검정하시오
      ```python
      from scipy.stats import ttest_1samp, ttest_ind
      a = df_iris[(df_iris['species']=='setosa')]['sepal_length']
      b = df_iris[(df_iris['species']=='versicolor')]['sepal_length']

      ttest_ind(a,b)[1] <0.05
      #결과값 : True = H1 지지, H0 기각
      ```
  
3. 어떤 마트에서는 금요일/토요일의 주류 평균 판매량이 다른 요일보다 많다는 가설을 검정하려한다. 검증을 진행하시오
   ```python
   from scipy.stats import ttest_ind
   df3 = pd.merge(df1, df2, how = 'left', left_on = 'itemDescription',
            right_on = 'prod_nm')



   df3['Date'] = pd.to_datetime(df3['Date'])
   df3['day'] = df3['Date'].dt.day_name()
   df3 = df3[df3['Date'].dt.month.isin([1,2,3])]

   df3['FS'] = (df3['day'].isin(['Friday','Saturday'])) + 0 
   #피벗테이블을 하나로 만들어서 열을 분리하여 데이터셋으로 활용
   #이때 dropna를 통해 결측치는 제거하는 것이 중요하다.
   df_pv= df3.pivot_table(values='alcohol',index='Date',columns = 'FS',aggfunc='sum')
   df_pv
   ttest_ind(df_pv[0].dropna(),df_pv[1].dropna(), equal_var=False)[1].round(2)
   ```
<br>
<b>3. Paired sample t-test</b>

 * 동시간대 등 환경을 동일하게 맞춰준 동일한 모집단에서부터 추출된  두 집단간 차이가 있는지 검정
 * 표본이 정규성을 만족하지 못하는 경우 wilcoxon rank sum test (순위합검정) 사용
 * Scipy -ttest_rel() 사용
 * ```활용: 동년, 동월, 동시간대 이용객 대상으로 비회원의 대여량과 회원의 자전거 대여량의 평균차이 검정```

* Two sample t-test 중 Paired vs Independent <br>
   - 작년 / 당년 평균판매량 비교시 :  지점별 차이를 통제해줘야하니 Paired 사용
   - 지점별 평균판매량 비교시 : Independent 사용
   - Paired : 같은 조건의 데이터가 한쌍, 데이터개수가 동일, 순서 동일, 결측치 안됨
   - Independent : 그룹 내의 평균끼리 비교 , 순서관계없음, 개수 동일 필요없음 <br> ```단, 평균의 차이만으로는 두 집단이 다르다라고 단정 할 수 없다.``` <br> 
   ```A 집단이 B집단에 포함 된 경우일 수 있음 ``` <br>
   ```So, 분산대비 평균을 봐야함 ==> 독립 이표본 검정(분산까지 포함하여 검정하는 방식)``` <br>

> 예제 
 1) 한국과 일본의 년도별 육류 소비량 평균이 비슷한 수준인지 대응검정하시오
```python
#1. 두 국가만 필터링하여 pv테이블을 만들어 데이터 순서를 맞춰야함
df_kj = df[(df['LOCATION'].isin(['KOR','JPN']))]
df_kj_pv = pd.pivot_table(data= df_kj, index= ['TIME','SUBJECT'], columns = 'LOCATION',values = 'Value',aggfunc=sum)
df_kj_pv


#대응ttest에서는 결측치 불가, 전체 결측치 제거수행
df_kj_pv = df_kj_pv.dropna()

#ttest 수행
from scipy.stats import ttest_rel
ttest_rel(df_kj_pv['KOR'],df_kj_pv['JPN'])[0].round(4)
```


<br><br><br>

## <b>ANOVA 검정</b> 

* 수치가 통계적으로 동질적인지 이질적인지 검증하기 위해 현업에서 많이 사용됨 <br>
* 그룹이 2개 이상 일때 사용하며, 2개인 경우는 t-test의 결과값과 동일하게 나온다. <br>

<b> 1. 일원분산분석 (One way Anova)</b>
* 세집단 이상 간의 평균차이
* 수치형 종속변수(평균)와 명목형 독립변수가 각각1하나씩일때 실시
* (명목형 독립변수 예시: company 같은 집단)
* 명목형 독립변수가 문자형인경우에는 상관없지만, 
  1,2,3,4 처럼 구분되어있는 경우 숫자형으로 인식하게하지 않기 위해, 일반적으로 독립변수 앞에 C로 감싸준다.
   ```python
   model= ols(formula = 'price ~ C(color)', data = df).fit()
   anova_lm(model)
   ```
  ```활용: 금,토,일이 같은 '주말'인지 or 80점과 81점이 동일한 수준인지 등```

<br>

<b>[scipy]</b> <br>
```python
# ANOVA scipy.stats 사용
from scipy.stats import f_oneway

##sample test 준비필요
a= df_hk[df_hk['company'] =='A'].salary
b= df_hk[df_hk['company'] =='B'].salary
c= df_hk[df_hk['company'] =='C'].salary

f_oneway(a,b,c)[1] < 0.05 #H0기각 :회사와 연봉은 연관이 있다.
```
<b>[statsmodels]</b> #분산분석표 제공
```python
# ANOVA statsmodels 사용
from statsmodels.formula.api import ols
from statsmodels.stats.anova import anova_lm
from statsmodels.stats.multicomp import pairwise_tukeyhsd

model = ols(formula = 'salary~ company', data= df_hk).fit() #formula: 종속변수~독립변수 

anova_lm(model)
```

>예제
1. 가장 많이 판매된 10개상품을 주력상품으로 설정하고 특정요일에 프로모션을 진행할지 말지 결정
일원분산분석을 통하여 요일별 주력상품의 판매개수의 평균이 유의미하게 차이가 나는지 알아보자.
```python
```


<br><br>
<b>2. 이원분산분석(Two way Anova)</b>
* 수치형 종속변수 1개, 명목형 독립변수가 2개일때 실시
* 주요효과 + 교효효과 (독립변수같의 영향성) 함께 분석
* 주요효과 귀무가설 : 평균이 같음
* 교호작용효과 귀무가설:  요인간 교호작용이 없음 
* : 를 이용 (주요효과 뒤 +로 연결)

```python
from statsmodels.formula.api import ols
from statsmodels.stats.anova import anova_lm
model = ols(formula = 'price ~ cut + color + cut:color', data=df).fit()
anova_lm(model)

#결과해석: 다이아몬드의 cut별 또는 color별간에 price 평균이 같으며(차이 없음), cut-color간 교호작용도 없다.
```
```python
from statsmodels.formula.api import ols
from statsmodels.stats.anova import anova_lm

model = ols('registered ~ C(season)+C(holiday) + C(season):C(holiday)',
           data= df_bike).fit()
anova_lm(model).round(5)
```








## <b>사후검정_tukey</b> 
* 독립2표본 t-검정과 유사
* reject : 유의수준 안에서 '귀무가설' 기각 여부 
  (False : 기각 불가 /  True : reject (기각))
* True : 귀무가설 기각이니까 두 집단은 다르다는 것.
  
```python
#endog : y label
#alpha : 유의 수준 0.05
from statsmodels.stats.multicomp import pairwise_tukeyhsd

posthoc = pairwise_tukeyhsd(df_hk['salary'], df_hk['company'], alpha =0.05 ) #종속,독립 순

print(posthoc) #변수에 할당해서 프린트 필요
```


<br>

> 예제

bike 데이터(bike.cvs)를 사용하여, 요일별 registered 평균이 같은지 가설을 수립하고 유의수준 0.05에서 검정하니,

평균이 같지 않을때, 평균이 유의수준 0.05에서 차이나지 않는 조합(False)은 몇 개인가 ?
```python
from statsmodels.stats.multicomp import pairwise_tukeyhsd

post_hoc = pairwise_tukeyhsd(df_bike['registered'], df_bike['date'], alpha = 0.05)
print(post_hoc)
```

<br>

## <b>상관분석</b>
- 상관계수를 통해 선형관계 여부를 분석
- Pandas-corr()메서드 : 상관계수만 제공
- Scipy 함수 : 상관계수와 p-value 확인 가능 <br>
    (검정통계량을 내부적으로 가지고 있지만 보여지는 숫자는 검정통계량이 아닌 상관계수와 PV)
- 검정 통계량 : t
- 거의 pearson이 주로 사용되며, spearnam,kendall의 순서형 상관분석은 대표적으로 설문조사 (나쁨/ 좋음 /매우좋음 등)에 사용됨
  



<b>[corr()]</b> <br>
```python
# pearsonr, spearmanr, kendalltau
df_hk.corr() #default method = pearson
df_hk.corr(method='pearson')
df_hk.corr(method='kendall')
df_hk.corr(method='spearman')

#groupby를 활용한 상관분석
df2= df.groupby('weather')[['temp','casual']].corr()
df2 = df2.reset_index()
df2[(df2['atemp'])<1]

```
<b>[scipy]</b> <br>
```python
# pearsonr
from scipy.stats import pearsonr
pearsonr(df_hk['age'], df_hk['salary'])

# spearmanr
from scipy.stats import spearmanr
spearmanr(df_hk['age'], df_hk['salary'])

# kendalltau
from scipy.stats import kendalltau
kendalltau(df_hk['age'], df_hk['salary'])
```
```!! corr는 DF로 추출해야함 [[]] !!```

> 예제 
 <br>
1.
   temp, atemp, humidity, registered의 상관 계수중 가장 높은것은 ?
   ```python
   df_bike[['temp','atemp','humidity','registered']].corr()
   ``` 
<br>

2. 날씨가 맑은날(weather = 1) 과 그렇지 않은날 온도(temp)와 자전거 대여 숫자(casual)의 상관계수의 절대값은 얼마인가 ?
      ```python
      df_bike[(df_bike['weather'] == 1)][['temp','casual']].corr()
      ```


3. 년도별 육류 소비량 합계를 구하여 Time 과 Value간의 상관분석하여라
   ```python
   #~별로 집계시 pv 활용
   df_k_pv = pd.pivot_table(df_k, index = 'TIME', values= 'Value',aggfunc= 'sum').reset_index()

   df_k_pv.corr()
   ```

<br>

## <b>독립성(연관성) 검정</b> ```[카이제곱검정]```
   - 범주형데이터와 범주형데이터간의 영향이 있는지 독립성 검정을 수행시 사용
   - 적합도, 독립성, 동질성 검정 사전에 진행 필요
   - 검정통계량 : 카이제곱 ∑ ((관측도수 - 기대도수)² / 기대도수)
   - :star: crosstab (빈도표) 자료 활용 필요 <br>
       - 빈도표는 각 독립변수와 종속별로 한번씩 만들어야함
         ```python
         #빈도테이블
         from scipy.stats import chi2_contingency
         result = []
         List = ['Sex','BP','Cholesterol','Agr_gr','Na_to_K']
         for i in List:
            table = pd.crosstab(df[i], df['Drug'])
            result += [[i, chi2_contingency(table)[1]]]
            
         pd.DataFrame(result, columns= ['var','pvalue'])
         ```
       - 비교변수가 여개 일때 활용코드
         ```python
         pd.crosstab(index = [df['BP'], df['Sex']],columns = df['Cholesterol']) 
         ``` 
   - 카이제곱 기대빈도표는 독립일때를 가정하여 그러짐 P(A∩B) = P(A)*P(B)
   - 자유도는 (r개수-1) * (c개수-1)
         
   - 두 명목형 자료 검정 <br>
     (수치형일 경우는 구간화/범주화를 통해서 명목형으로 변환후 사용)



   - correction = False 는 연속성 수정을 적용하지 않음을 의미함 ```chi2_contingency(crosstab2 , correction = False)```
 <br>

```python
# 관측값 cross 제공 필요

cross = pd.crosstab(df_hk['gender'], df_hk['company'])
#margins = True : 행/열합계, normalize = True: 전체기준

from scipy.stats import chi2_contingency #독립성검정
chi2_contingency(cross)

#결과값 dof =자유도
Chi2ContingencyResult(statistic=1.674107142857143, pvalue=0.43298440342651534, dof=2, expected_freq=array([[44.8, 44.8, 22.4],
       [55.2, 55.2, 27.6]

pvalue=0.43298440342651534 > 0.05
#H0 채택: 독립이다(상관없다)
```

> 예제

1) season과 weather dtype을 문자형으로 변환하고
두 변수가 관련있는지 적절한 검정을 하고 검정통계량과 p-value를 구하시오
   ```python
   df_bike['weather']= df_bike['weather'].astype('str')
   df_bike['season']= df_bike['season'].astype('str')
   cross = pd.crosstab(df_bike['weather'], df_bike['season'])
   chi2_contingency(cross)[1] < 0.05
   #h0 기각
   ```

2) 자전거 총 대여수(count)가 상위 30%일때 'high', 그 미만 일때 'low' 인 파생변수(count_high)를 생성하고
count_high와 workingday의 연관성 여부를 검정하고 검정 통계량을 구하시오 (소숫점 넷째자리 반올림하여 표기)
   ```python
   import numpy as np
   df_bike['workingday']= df_bike['workingday'].astype('str')

   df_bike['count_high'] = np.where(df_bike['count']>= df_bike['count'].quantile(0.3), 'high','low')
   cross = pd.crosstab(df_bike['count_high'], df_bike['workingday'])
   chi2_contingency(cross)[0].round(4)
   ```


<br><br>

## 등분산 검정
* 두 집단 또는 그이상의 집단간 분산이 같은지 여부 검정
* 귀무가설 : 집단간 분산은 서로 같음

  1. f_test : 두집단대상 / 정규분포를 따를 때 사용 
     (Anova 정규분포를 따름)
      
      <b>python에는 f검정 함수가 없기 때문에
      Scipy - f.cdf() (누적분포관련 함수)에
      f 검정통계량 (분산비), 첫번째 데이터의 자유도, 두번째 데이터의 자유도를 직접 계산하여 p-value를 구한다.</b>
  2. Bartlett's test : 두집단 이상 대상 / 정규분포를 따를 때 사용
  3. Lavene's test : 두집단 이상 대상 / 정규분포를 따를 필요가 없음

> 예제

1) 남성과 여성의 1회 평균 송금액의 분산을 비교검정하고, 그 결과의 검정통계량은 얼마인가?
(2집단이니까 분산비를 구해서 F검정도 가능)



   ```python
   from scipy.stats import f
   from scipy.stats import bartlett
   from scipy.stats import levene

   #공통전처리
   df['trans_mean'] = df['Total_trans_amt'] / df['Total_trans_cnt']
   M_a =df[(df['Gender']== 'M')]['trans_mean']
   F_a =df[(df['Gender']== 'F')]['trans_mean']

   #---F검정---

   #F통계량
   F = M_a.var() / F_a.var()
   print(F)

   #f검정_cdf
   result = f.cdf(F, dfd = len(M_a)-1, dfn = len(F_a)) 
   print(result)

   #p-value
   p = (1-result) * 2


   #---bartlett 검정---
   bartlett(M_a, F_a)


   #---levene 검정---
   levene(M_a, F_a)
   ```

<br><br>

## 시계열분석
### <b>평활화</b>
 - 이동평균법 
   -  단순이동평균법 (Simple Moving Average)
  
      메서드 : Pandas =rolling() <br>
      window에는 이동평균대상이 되는 데이터 개수 n 를 지정 <br>
      n일부터 평균치 계산됨으로 최초데이터 n-1개 만큼 결측치 존재 <br>
      center에 True를 입력할 경우 중심 이동 평균실시 가능 <br>

      ```python
      import pandas as pd
      df = pd.read_csv('./data/seoul_subway.csv')

      df_sub["mean5"] =df_sub['승차총승객수'].rolling(window=5).mean()
      df_sub[:10]
      ```


   -  가중이동평균법 (Weighted Moving Average)
  <br><br>

 - 지수평활법 
   -  단순지수평활법(EWMA)  
      메서드 : Pandas-ewm() <br> 
      Alpha = 지수평활계수 입력
      ```python
      df_sub["EWMA"] =df_sub['승차총승객수'].ewm(alpha = 0.9).mean()
      df_sub[:10]
      ```


   -  이중지수평활법(Winters) 
   -  삼중지수평활법(HoltWinters)


### <b>시계열분해</b>


- 메서드 : statsmodels - seasonal_decompose()
- Model 인자에 'multiplicative'를 입력하면 승법모형 적용(기본 = 가법모형
- :star: 시계열 데이터 컬럼을 인덱스화 해줘야한다.

```python
from statsmodels.tsa.seasonal import seasonal_decompose
#tsa : time series analysis

df['사용일자'] = pd.to_datetime(df['사용일자'], format = '%Y%m%d')
df_sub = df[(df['노선명'] =='1호선')&(df['역명'] =='종로3가')]
df_sub = df_sub.set_index('사용일자') #시계열 데이터 인덱스화 : 데이터레벨로 접근

result = seasonal_decompose(df_sub['승차총승객수'][:200])
result.plot()
#result.seasonal
#result.trend 
#result.resid 
```


<br><br>

# <b>Machine Learning </b>

## <b>1. Pre-processing</b>
### <b>1. Scaling</b>

 - 스케일링 전후 비교를 위해 histogram 2가지

   ```python
   df_hk.hist()

   sns.histplot(df_hk[['height','age', 'salary' , 'expenditure']])
   ```



 -  min_max scaling (최소-최대 변환) (범위:0~1) <br>
    -  표준화 : min-max 단위를 고르게 하기 위하여 모든 값을 0~1사이로 바꾸는 것 
      ```python
      # 대상변수 선택 (수치형) 'height', 'age', 'salary', 'expenditure'

      df_num = df.select_dtypes(include=['float64','int64'])
      df_cat = df.select_dtypes(include=['object'])


      from sklearn.preprocessing import MinMaxScaler
      scaler = MinMaxScaler()
      scaler.fit(df_num)
      df_scaled = scaler.transform(df_num)
      pd.DataFrame(df_scaled, columns = df_num.columns)

      # 시각화 

      fig, ax = plt.subplots( nrows= 1 , ncols=2, figsize=(14, 5))

      ax[0].set_title('original ')
      ax[1].set_title('minmax')


      df_num.plot.hist(ax= ax[0] )
      df_mm.plot.hist(ax= ax[1] )
      plt.show()

      ```

 -  standard scaling (Z-score 변환) (범위 : 0 중심, -∞ ~ +∞) <br>
     - 정규화: StandardScaler 모든 변수의 값을 평균이 0이고 분산이 1인 정규 분포로 변환 
      ```python
      from sklearn.preprocessing import StandardScaler
      scaler_ss = StandardScaler()
      df_scaled_ss = scaler_ss.fit_transform(df_num)
      df_ss = pd.DataFrame(df_scaled_ss, columns= df_num.columns)
      df_ss
      #시각화 
      fig, ax = plt.subplots( nrows= 1 , ncols=3, figsize=(14, 5))

      sns.histplot(x='salary', data=df_num, ax= ax[0])
      sns.histplot(x='salary', data=df_mm, ax= ax[1], color='green')
      sns.histplot(x='salary', data=df_ss, ax= ax[2], color='orange')

      ax[0].set_title('df salary histplot')
      ax[1].set_title('df_minmax salary histplot')
      ax[2].set_title('df_stan salary histplot')
      plt.show()
      ```
<br>

### <b>2. Get dummies</b>

```python
# 해당 column만 get_dummies
pd.get_dummies(df[['gender', 'blood_type', 'company', 'grades']],drop_first= True)  

#전체 데이터에 get_dummies
pd.get_dummies(df, columns =['gender', 'blood_type', 'company', 'grades'], drop_first= True)  
```

<br><br>

## <b>2. Feature Engineering</b>


1) filter (기준을 만족하는 변수 추출)
- 예시) 독립변수 수치형 변수중 회귀계수가 높은 2개 선정 (feature selection) 하시오
독립변수 수치형 변수중 t검정 통계량의 p-value가 0.05이하인것을 선정하시오
   ```python
   # p-value 값 0.05 미만 / coef 절대값 0.5이상인 변수를 선택
   model_ols.params.index[(model_ols.pvalues < 0.05)& (model_ols.params.abs() >= 0.5)]
   ```
2) wrapper
 - 전진선택법, 후진제거법, 단계선택법

3) embedded


<br><br>

## <b>3. Model</b>

> ## <b> Unsupervised Learning </b>
>  '예측'보다는 없었던 y를 찾는 것에 주안점 <br>
>  모델에 fit 시킬때 y가 None


<br>

## <b>계층적 군집분석</b>
- :star: 이상치 및 데이터변동에 민감
- N개의 데이터가 있을때 N개의 군집으로 시작~ 최대 하나의 군집이 남을 때까지 거리가 가장 가까운 두 요소를 군집화 를 반복
- n_cluster 설정시 n 개수가 될 때까지 군집화
- 사전에 K를 할당할 필요가 없음
- 거리기반(유사도)로 묶기
   - 최단연결법
   - 최장연결법
   - 평균연결법
   - 중심연결법
   - 와드연결법 
  <br>

- :star: 데이터개수가 많은 경우 연산에 많은 시간이 소요 <br>
  (5천개~만개를 넘기는 데이터에는 비권장)
- :star: 계층도(Dendrogram) 확인 가능: 데이터간 거리를 기반으로 도식화한 도표 (model사용하지않고 scipy에서 자료로 스스로 연산)
  
- [메서드] 
  - sklearn-AgglomerativeClustering() <br>
      - n_clusters = 분래 군집개수 설정 <br>
      - Affinity = 데이터 간 거리계산방법 <br>
      - Linkage = 군집간 유사도 방법 설정 <br>
  - Spicy - dendrogram() 
  - Spicy - Linkage() =  데이터 간 거리 계산 및 군집 형성
- 유클리디안 거리 공식 : 두 거리 diff를 제곱하고 더하여 마지막에 루트를 씌워줌
  
```python
import pandas as pd
from sklearn.cluster import AgglomerativeClustering
from scipy.cluster.hierarchy import dendrogram, linkage
from matplotlib import pyplot as plt

df = pd.read_csv('./data/iris.csv')
df_x = df[['Sepal.Length','Sepal.Width','Petal.Length','Petal.Width']]
model = AgglomerativeClustering(n_clusters = 3).fit(df_x) 
# y label이 없는 비지도학습 > 독립변수만 fit 시킴
# (default) method = ward 
df['cluster'] = model.labels_
pd.crosstab(df['Species'], df['cluster'])

df.groupby('cluster').mean().reset_index()
# 군집별 centroid구하기


# 그래프 그리기
link = linkage(df_x, method = 'ward') 
# link : cluster링 결과, 처음 두 개는 행 번호, 거리, 클러스터에 속한 데이터 수, 묶어지면서 새로운 numbering 부여됨
#(default) method = single 위 모델과 일치 시켜줌 > ward로 변경
dendrogram(link)
plt.show()

# 시각화를 통해 insight 발굴 (black box 유추하기)
# 예시 (독립,종속 그래프에 hue로 cluster 결과값 입히기)
fig, ax = plt.subplots( nrows= 1 , ncols=2, figsize=(14, 5))
sns.scatterplot(x='age', y='salary', data=basetable1, hue='company',  palette='Set1', ax= ax[0] )
sns.scatterplot(x='age', y='salary', data=basetable1, hue='cluster_hier',  palette='Set2', ax=ax[1] )

ax[0].set_title('category : company ')
ax[1].set_title('category : hierarchy cluster')
```

## <b>비계층적 군집분석</b>
- 임의의 k점을 기반으로 가까운 거리의 데이터를 묶음
- k를 확정하기 위해 여러번의 시행착오 필요
- 결과를 고정하기 위해 seed설정 필요 <br>
  ```활용 : 고객군집을 나눌때 Model로 예측하고, 가장 관심있는 종속변수, 독립변수 좌표 위에 label값을 hue를 둔 시각화를 통해 나눈 기준(black-box) 을 유추하며 insight를 가져온다 ```
  
```python
import pandas as pd
from sklearn.cluster import KMeans
cluster_1_2 = KMeans( n_clusters=3, random_state=123).fit(basetable_cluster_1) 
basetable1['cluster_kmean'] = cluster_1_2.labels_

basetable1.groupby('cluster_kmean').mean() # model.cluster_centers_ attribute 와 기능동일, 단 해당 코드는 컬럼이 없어 별도 df작업을 해줘야하기 때문에, groupby를 직접 해주는 것이 더 편리

# Attribute 확인
cluster_1_2.inertia_



pd.crosstab( basetable1['cluster_hier'], basetable1['cluster_kmean']) #계층적 model과 비교
pd.crosstab( basetable1['company'], basetable1['cluster_kmean'])

#시각화
fig, ax = plt.subplots( nrows= 1 , ncols=3, figsize=(16, 5))
sns.scatterplot(x='age', y='salary', data=basetable1, hue='company',        palette='Set1', ax=ax[0] )
sns.scatterplot(x='age', y='salary', data=basetable1, hue='cluster_hier',   palette='Set1', ax=ax[1] )#계층적 model과 비교
sns.scatterplot(x='age', y='salary', data=basetable1, hue='cluster_kmean',  palette='Set1', ax=ax[2] )

ax[0].set_title('category : company ')
ax[1].set_title('category : hierarchy cluster')
ax[2].set_title('category : kmeans cluster')
plt.show()

```
<br><br>

## <b>PCA</b>
- 주성분이 기존 변수들의 분산을 얼마나 커버하는지에 따라 주성분을 선택하게되며, 최대 기존 변수개수만큼 뽑아낼 수 있다.
- n_component : 산출할 주성분 개수 입력
- .cumsum() : 시리즈객체의 누적합 계산 메서
- 고유벡터 : 방향 / 고유값: 벡터공간

- PCA STEP
  1. 정규화 (0으로 이동)
  2. 공분산 행렬계산
  3. 공분산 행렬의 고유벡터와 고유값(공분산 설명력)계산
  4. 원본데이터와 고유벡터를 내적하여 주성분 구하기
   
   
``` 활용 : VIF 지수가 10 초과하는 변수들이 다수 존재 할때 PCA를 통해 차원 축소``` <br>
``` 또한 기존변수를 활용한 모델과, 추출한 1개이상의 주성분울 활용한 모델을 비교하여 나은 모델을 채택할수 있음```

### <b>직접 증명해보기</b>

```python
#1. 정규화
iris_std = StandardScaler().fit_transform(df_iris_2)
df_iris_std = pd.DataFrame(iris_std, columns =  df_iris_2.columns)
df_iris_std

#2. 공분산행렬 확인 
import numpy as np 
cov_matrix = np.cov(df_iris_std.T) #wide form으로 변환필요
#변수가 n개일때 n*n 의 공분산 생성

#3. 고유값(분산설명력, explained_variance), 고유벡터 추출(사영계수, components)
eigenvalues, eigenvectors = np.linalg.eig(cov_matrix)

#고유값(분산설명력, explained_variance) =eigenvalues
#고유벡터 추출(사영계수, components) = eigenvectors


#4. 내적
pca_iris = pd.DataFrame({'pca1':df_iris_std @ eigenvectors.T[0], 'pca2':df_iris_std @ eigenvectors.T[1], 
                         'pca3':df_iris_std @ eigenvectors.T[2], 'pca4':df_iris_std @ eigenvectors.T[3]})


#5.시각화 비교 
fig, ax = plt.subplots( nrows= 1 , ncols=2,  figsize=(6,3))

sns.scatterplot(x = 'sepal_length', y = 'sepal_width', data=df_iris_2,   ax= ax[0])
sns.scatterplot(x = 'pca1', y = 'pca2',                data=pca_iris,    ax= ax[1])

ax[0].set_title('sepal_length, sepal_width')
ax[1].set_title('pca1, pca2')
plt.show()
```
### <b>sklearn</b>
```python
from sklearn.decomposition import PCA
pc = PCA(n_components=3) #주성분 개수 : 최대 기존변수개수까지
pc.fit(df_iris_std)

#고유값(singular_values)
pc.singular_values

#분산설명력(explained_variance)
pc.explained_variance_

#고유벡터 확인(사영계수, components)
pc.components_

#pca1 (안해도됨)
df_iris_std @ pc.components_[0]

# transform으로 PCA 계산, df_iris_std @ pc.components_[0]
# transform, 이때 columns의 값은 pca1~4로 변경되어야 함
pd.DataFrame(pc.transform(df_iris_std), columns = [ 'pca_'+ str(i) for i in  range(1,5)] )

# 누적 분산 설명력(explained_variance_ratio_)
print(pc.explained_variance_ratio_)
print(pc.explained_variance_ratio_.cumsum())

# 누적 분산 설명력(explained_variance_ratio_) 시각화
sns.lineplot(x = [1,2,3,4], y=pc.explained_variance_ratio_.cumsum()) #cumsum주의
plt.xticks([1,2,3,4])
plt.title('explained_variance_ratio_')
plt.show()
```
<br><br>

## <b>Association Rules</b>
- 확률에 근거 (조건부확률이 압도적으로 사용됨)
  - itemsets생성
  - if(선행) ~then(후행) 규칙 조사
- n개의 item으로 가능한 조합의 수는 2**n 이기 때문에, <br>
  support(많이 사는 조합) , confidence 기준으로 item 목록을 자른다.
- Apriori : 빈발하는 itemset을 찾는 mining 기법
- 선생과 후행은 공통원소가 없어야 하며, 각각 중복없는 항목의 집합이어야함
- 지지도(Support) : support(x→y) x,y 가 같이 구매될 확률
- 신뢰도(Confidence) : support(x→y) / support(x)
- 향상도(Lift) : confidence(x→y) / support(y) <br>
    - Lift > 1 : 보완재 / 양의 상관관계 <br>
    - Lift = 1 : 독립적인 관계 <br>
    - 0 < Lift < 1 : 대체제 / 품목간 상호 음의 상관관계 <br>
- max_len: 아이템 조합 최대값 설정 <br>
- use_columnes= True : 아이템명 사용 <br>
 ```활용 : 추천시스템```

```python
#!pip install mlxtend
### [예문1]
import pandas as pd
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules
df= pd.read_csv('./data/association_rules_mart.csv')

#판매 상위 30개 품목에 한정하여 데이터셋 준비하기
df_cnt = df['Item'].value_counts().reset_index()
df_cnt = df_cnt.sort_values(by='Item', ascending = False)
df_cnt = df_cnt.iloc[:30,]

#원본데이터에서 판매상위품목만 필터링
df = df[(df['Item'].isin(df_cnt['Index']))]

#사전 중복 제거 
df.drop_duplicates(subset = ['ID','Item'])

#pivot으로 itemlist생성
df['purchase'] =True
df_pivot= df.pivot_table(index='ID', columns = "Item", 
                         values ="purchase", aggfunc = max,
                        fill_value = False)
item_sets = apriori(df_pivot, min_support = 0.005, use_colnames =True, max_len = 3)
item_freq.head(3)

#연관규칙 생성
df_rules = association_rules(item_sets, metric = 'lift', min_threshold = 1.5)
df_rules


### [예문2]
# step 1) drop_duplicates 한개의 빌당 2개 이상 구매한 중복건 제거
df_mart = df_mart.drop_duplicates(subset =['ID', 'Item'])

# step 2) itemlist 만들기 방법 1 (Encoder활용)
# 2-1) id별로 item 정리 
df_mart = df_mart.groupby('ID').apply( lambda x: x['Item'].tolist()).reset_index().rename(columns={0:'Item'})
df_mart

# 2-2) min_support=0.005, min_threshold=0.005
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori, association_rules

encoder = TransactionEncoder()
encoder_result = encoder.fit(df_mart['Item'] )


# 2-3) transform
trans = pd.DataFrame( encoder.transform( df_mart['Item']), columns =encoder.columns_ )
trans


# step 2)itemlist 만들기 방법 2 (Pivot활용)
# pivot_table 생성
   # df_mart['cnt'] = True
   # trans = pd.pivot_table(df_mart, values='cnt', index='ID', columns='Item', aggfunc = 'max', fill_value= False) #중복구매건이 있을때 T/F이 생기니까 max로 해주면 T를 반환


# TransactionEncoder attribute 확인
te1.columns_mapping_


# step 3) apriori
apri = apriori(trans, use_colnames=True,  min_support=0.01)
apri #조건 최소 지지도 min_support=0.01, use_colnames=True (아이템명으로 보여주기)


# step 4) association_rules
asso = association_rules( apri1, metric='confidence', min_threshold=0.01)  
asso  # 조건 최소 신뢰도 0.01로 주기 


# step 5) antecedents이 단일 Item인 건 추출
asso[(asso['antecedents'].apply(lambda x:len(x)) == 1)]

# step 6) 우유를 사는 사람은 후행으로 어떤 상품을 많이 사는지 lift 내림차순으로 정렬

#asso1['antecedents'].values[:10]
asso.loc[ asso['antecedents'] == frozenset({'Milk'}), : ].sort_values('lift', ascending=False).head(10)

```
<br><br>

## <b>모델평가</b>
- Elbow score
  - kmeans inertia_ (응집도)활용
  - Inertia 값, 군집화후 각 중심점에서 군집의 데이타간 거리를 합산한것으로 응집도를 나타내는 값 = cluster 개수를 높힐 수록 inertia는 작아짐, 값이 작을 수록 응집도가 높게 군집화가 잘되었다고 평가할 수 있음
  - k가 몇일때 응집도가 가장 dramatic 하게 감소하는지 확인
   ```python
   # n_clusters=k를 1부터 10까지 적용

   inertias = []
   mapping = {}
   K = range(1, 10)

   for k in K:
      kmeanModel = KMeans(n_clusters=k).fit(basetable_cluster_1) 
      inertias.append(kmeanModel.inertia_)
      mapping[k] = kmeanModel.inertia_
      print('k값 ', k , '=>', kmeanModel.inertia_)

   # Elbow score 시각화
   plt.plot(np.arange(1, 10), inertias, 'bx-')
   plt.xlabel('Values of K')
   plt.ylabel('Inertia')
   plt.title('The Elbow Method using Inertia')
   plt.show()
   ```
- Silhouette score
    - silhouette_score가 1에 가까워야 Positive
    - 각 데이터 포인트와 주위 데이터 포인트들과의 거리 계산을 통해 값을 구하며, 군집 안에 있는 데이터들은 잘 모여있는지, 군집끼리는 서로 잘 구분되는지 클러스터링을 평가하는 척도로 활용
    - 값이 0에 가까운 경우 : 두 군집 간 거리가 거의 비슷한 경우   (잘 구분되지 않은 상태)
    - 값이 -1에 가까운 경우는, 데이터 포인트 i가 오히려 이웃 클러스터에 더 가까운 경우를 의미 (잘못 할당된 상태) 
  - silhouette_score(data, 라벨)
  
   ```python
   from sklearn.metrics import silhouette_score
   

   k_score = pd.DataFrame(columns =['k', 'score'])
   for i in np.arange(2, 7):
      model_clustering = KMeans( n_clusters=i, random_state=123).fit(basetable_cluster_1)
      a = silhouette_score( basetable_cluster_1,model_clustering.labels_)
      k = pd.DataFrame({'k':[i], 'score':[a]})
      k_score = pd.concat([k_score, k]).reset_index(drop=True)
      print("K값 ", i, " silhouette score: ", a.round(3) )
   
   #시각화
   sns.lineplot(x='k', y='score', data=k_score)
   plt.xticks([2, 3, 4, 5, 6])
   plt.show()
   ```





<br><br><br>
> ## <b> Supervised Learning </b>
<br>

## <b>선형회귀</b>
 - statsmodels vs sklearn 비교 
 - statsmodels는 통계기반 관점  (summary 표 등 통계자료 보기 편함) 
 - sklearn는 머신러닝 관점
 - 입력값의 차이(statemodels ols의 경우 formula 문법이 있음 / sklearn는 fit() 활용)
-  ols model 과 sklearn 모델 두가지로 접근 가능
-  회귀 ols는  연속형 종속변수, 연속형 독립변수
   ANOVA ols 는 연속형 종속변수, 명목형 독립변수
-  ols.summary()에서 fpvalue로 선형성 검증
-  ols는 학습한 데이터만 별도로 모델에 적합시키지 않아도 알아서 걸러서 적합함
- 반면 sklearn은 intercept로 절편 적합 여부 설정이 가능하여 강력한 최적화 강점을 가지고 있다

<br>

### <b> 선형회귀 가정 4가지 선형성, 정규성, 등분산, 독립성</b>
### <b>1. 선형성</b>
- F 검정의 pvalue로 확인
- summary()의 t 검정 값도 '선형의 유효성'을 확인하는것이지만, 이것은 두집단 간 검증지표며, x가 많은 다중회귀에서는 f-pvalue로 확인 가능하다.
- :star: 귀무가설 : 선형성이 없다
   ```python
   # 선형회귀 그래프, regplot: scatter plot, regression line, confidence band를 한 번에 그리는 기능
   sns.regplot(x='salary', y='expenditure', data=df)
   sns.regplot(x=df['salary'], y=predict_ols)

   # F 검정의 pvalue로 확인
   model_ols.f_pvalue 
   model_ols.f_pvalue < 0.05
   # 결과 : True (h1 지지 : 선형성이 있다고 판단)
   ```
### <b>2. 잔차의 정규성</b>
- 잔차 그래프로 확인
- shapiro 의 경우 p값이 0.05 이상이면 정규성 만족한다
- :star: 귀무가설 : 정규성을 만족한다 

   ```python
   # 잔차 계산
   residual = df['expenditure']-predict_ols

   # 잔차 그래프 1
   plt.scatter(df['salary'], residual)
   plt.show()
   # 잔차 그래프 2
   sns.distplot(residual)
   plt.show()

   # shapiro 정규성 검정, Ho: 정규성을 가진다 (p-value > 0.05)
   from scipy.stats import shapiro
   shapiro(residual)[1] < 0.05
   # 결과해석: TRUE , 0.05 보다 작으므로 귀무가설 기각(= 정규성을 만족 못함)
   # residual이 그룹화 되어 있어 shapiro test에서 정규성이 안 나옴

   # 시각화
   import scipy.stats as stats
   stats.probplot(residual, plot=plt)
   plt.show()
   ```

### <b>3. 잔차의 등분산</b>
- 예측값과 잔차의 산점도로 파악
   ```python
   # 잔차그래프로 확인, X가 커질때 잔차의 간격이 변하면 안됨, 간격이 일정하면 등분산성 만족
   sns.regplot(x=predict_ols, y=residual)
   ```
### <b>4. 잔차의 독립성</b>
- 잔차가 독립인지(자기상관성이 있는지) 검정
   ```python
   #perform Durbin-Watson test

   from statsmodels.stats.stattools import durbin_watson
   durbin_watson(model_ols.resid)

   # 더빈 왓슨 통계량은 0 ~ 4사이의 값을 갖을 수 있음
   # 0에 가까울수록 → 양의 상관관계
   # 4에 가까울수록 → 음의 상관관계
   # 2에 가까울수록 → 오차항의 자기상관이 없음
   ```
<br><br>

### <b> 단순선형회귀</b>
- 데이터를 ~별로 회귀모델을 만들 경우 각각 반복문을 돌려줘야하고 (fit, pred), 
- 이때의 결정계수를 구하기 위해선 model.score(독립변수, 종속변수)로 구한다.

### <b>statsmodels_ols</b>
```python
from statsmodels.formula.api import ols
model_ols = ols(formula = 'expenditure ~ salary', data= df).fit()

model_ols.summary()

model_ols.params #절편, 회귀계수
model_ols.resid #잔차

# 회귀식 만들어보기
def linear_ols(x):
    return (model_ols.params[1]* x + model_ols.params[0])
linear_ols(4720)

# predict로 예측값 확인
predict_ols = model_ols.predict(df['salary'])

# 시각화 
fig, ax = plt.subplots( nrows= 1 , ncols=2, figsize=(14, 5))
sns.scatterplot(x=df['salary'], y=df['expenditure'], palette='Set1', ax= ax[0] )
sns.scatterplot(x=df['salary'], y=predict_ols, palette='Set2', ax=ax[1] )

ax[0].set_title('expenditure ')
ax[1].set_title('predict_ols')
plt.show()
```
### <b>statsmodels_OLS</b>
```python
# statsmodels.api
import statsmodels.api as sm

model_sm = sm.OLS(df_train1['salary'], sm.add_constant(df_train1[['age']])).fit()
model_sm

#sm.add_constant 있어야 상수항이 포함됨
model_sm.predict(sm.add_constant(df_test1[['age']]))[:5]

# summary() #상수항확인가능
model_sm.summary()
```

### <b>sklearn</b></b>
```python
# LinearRegression 호출
from sklearn.linear_model import LinearRegression

# 모델선택, 독립변수(salary), 종속변수(expenditure) 입력, fit 
model_lm = LinearRegression()
model_lm.fit(X = df[['salary']], y= df[['expenditure']]) 
#x변수는 df형태가[[]] 필수지만, y변수에는 []도 가능 & []로 처리해야 결과값도 []로 리턴되어 후처리시 편리
결과값 가공에 용이
# 회귀계수 확인
model_lm.coef_
# intercept_ 확인
model_lm.intercept_

# 회귀식 만들어보기
def linear_lm(x):
    return (model_lm.coef_[0] * x) + model_lm.intercept_
# 회귀식으로 예측
pred_lm = model_lm.predict(df[['salary']])

# 선형회귀 그래프
sns.regplot(x=df['salary'], y=pred_lm)
```
<br>

> 예제
1. 1년동안 가장 많이 판매된 10개상품을 주력상품으로 설정하고 특정 요일에 프로모션을 진행할지 말지 결정하고자한다. 먼저 요일을 선정하기 전에 일원분산 분석을 통하여 요일별 주력상품의 판매개수의 평균이 유의미하게 차이가 나는지 알아보고자 한다.
```python
df1['cnt'] = 1
df1['Date'] = pd.to_datetime(df1['Date'])
df1['day'] = df1['Date'].dt.day_name()
df1

item10 = df1['itemDescription'].value_counts().sort_values(ascending = False)[:10].index

pv= pd.pivot_table(df1[df1['itemDescription'].isin(item10)], index= ['Date','day']
                   , values = 'cnt', aggfunc= 'sum'  ).reset_index()
pv


from statsmodels.formula.api import ols
from statsmodels.stats.anova import anova_lm

model = ols(formula = 'cnt ~ C(day)', data= pv).fit()
anova_lm(model)
#model.predict(pv[['day']])
```

<br><br><br>

### <b>다중선형회귀</b>
### <b>다중공선성 문제</b>
  - 분산팽창 계수(VIF)가 10이상이면 제거
  - method: patsy- dmatrices() <br>
return_type인자에 dataframe으로 설정시 후처리 용이
- statsmodele-variance_inflation_factor() <br>
분산팽창 계수를 연산을 위해 반복문 또는 list comprehension 사용

```python
from patsy import dmatrices
df_sub = df.loc[:,'season':'casual']
formula ='casual ~ '+ '+'.join(df_sub.columns[:-1])
y, X = dmatrices(formula , data = df_sub, return_type = 'dataframe')

#반복문 돌리면서 변수별 하나씩 매칭하여 상관계수 구함
from statsmodels.stats.outliers_influence import variance_inflation_factor as via
df_vif = pd.DataFrame()
df_vif['colname'] = X.columns
df_vif['VIF'] = [vif(X.values, i) for i in range(X.shape[1])]
df_vif
#결과값에서 intercept는 절편항이니까 신경안써도됨
```
<br><br>

## <b> 로지스틱 회귀</b>
-  베르누이 분포를 따를 경우 사용
-  (pred>0.9) + 0) #기본값 0.5 외 threshold 설정시 유용
### <b>statsmodels_logit</b>
```python
import pandas as pd
import numpy as np
from statsmodels.api import Logit

df['is_setosa'] = (df['Species'] =='setosa') + 0
model = Logit(df['is_setosa'], df.iloc[:,:2]).fit()
model   #통계모델 : (종속, 독립) 순서 주의

pred = model.predict(df.iloc[:3,:2])
pred_class = (pred > 0.5) +0 
#통계모델은 결과값이 proba 확률로 산출되기 때문에, threshold값 지정하여 2진 분류 수기로 진행해줘야함. ()안의 조건에 해당되는 것이 1 


#승산비 구하기 (회귀계수를 exp해주면 된다.)
np.exp(model_lo2.params)
```
### <b>statsmodels_formula_logit</b>
```python
from statsmodels.formula.api import logit

# formula 생성
form = 'car_type ~ ' + ' + '.join(df_hk_0.drop('car_type',axis =1).columns)
form  #통계모델 : (종속, 독립) 순서 주의

model_logit = logit(form, data = df_hk1_0).fit()
model_logit.summary()
```

### <b>statsmodels</b>

```python
import statsmodels.api as sm

model_smLogit = sm.Logit(endog = df_hk1_0['car_type'], exog = sm.add_constant(df_hk1_0.drop('car_type', axis=1))).fit()
# 통계모델 : (종속, 독립) 순서 주의
# sm.add_constant intercept으로 상수항 포함시키기

model_smLogit.summary()
```

### <b>sklearn</b>
- solver 최적화 알고리즘 설정 가능 (최적값을 산출할때 많이 사용)
```python
from sklearn.linear_model import LogisticRegression

model_lg = LogisticRegression(C=100000 ,solver='newton-cg')
# C=100000: 정규화(L1, L2규제) 강도의 역수; 양의 실수, 값이 작을수록 더 강력한 정규화 지정

model_lg.fit(df.iloc[:,:2],df['is_setosa'])

pred = model_lg.predict_proba(df.iloc[:,:2])
pred = pred[:,1]
roc_auc_score(df['is_setosa'], pred) # 실측값, 예측값순
accuracy_score(df['is_setosa'], (pred>0.9) + 0) 
```

<br><br>
## <b>나이브 베이즈</b>
-  사전확률 및 추가정보를 기간으로 사후확률을 추론하는 통계기법 '베이즈 추정' 기반 분류
-  종속변수 각 범주의 등장빈도인 '사전확률' 설정이 중요
-  각 데이터의 사전 확률을 기반으로 사후확률 계산
-  종속변수가 연속형 변수일 때, Gaussian Naive Bayes (가우시안 나이브 베이즈)
-  종속변수가 범주형 변수일 때, Multinomial Naive Bayes (다항 나이브 베이즈) 
  
    
### <b>sklearn</b>
```python
import pandas as pd
from sklearn.naive_bayes import GaussianNB

df =pd.read_csv('./data/iris.csv')
df['is_setosa'] = (df['Species']=='setosa') + 0

# 사전확률(비율) 구하기
df['is_setosa'].value_counts(normalize = True)


model_g = GaussianNB()
model_g.fit(df.iloc[:,:4], df['is_setosa'])

# 사전확률 메서드 활용하여 구하기
model_g.class_prior_

# 계수
model_g.theta_

pred= model_g.predict_proba(df.iloc[:,:4])
pred
```

<br><br>
## <b>Decision Tree</b>
- 비모수적 기법
- 전제 가정(정규성, 독립성 등)이 없어도됨
- 수치형, 범주형 데이터 모두 적용 가능
- 단, 전역 최적화를 얻지 못할 수 있음
- 과적합이 쉽게 발생
- 자료 가공이 거의 필요 없음
- max_depth : 트리의 최대 깊이 (default = None
→ 완벽하게 클래스 값이 결정될 때 까지 분할 <br>
또는 데이터 개수가 min_samples_split보다 작아질 때까지 분할)
→ depth를 높힐수록 피팅 (구간) 개수가 늘어남 <br> 
(피팅은 일정 구간마다 평균값으로 하게 되어있다) <br>
(시각화시 계단형으로 표현됨)<br>
  
- min_samples_split : 노드를 분할하기 위한 최소한의 샘플 데이터수 → 과적합을 제어하는데 사용
(default = 2 → 작게 설정할 수록 분할 노드가 많아져 과적합 가능성 증가)

```python
# DecisionTreeClassifier 호출
from sklearn.tree import DecisionTreeClassifier

model_dt = DecisionTreeClassifier(max_depth = 6, min_samples_split= 5, random_state =1234)

model_dt.fit(train_df_hk_3.drop('car_type',axis=1),
             train_df_hk_3['car_type'])

# feature_importances_  종속변수(car_type에 영향을 미치는 정도) -> feature_importances_로 분기 한다
model_imp = pd.DataFrame()
model_imp['feature']= model_dt.feature_names_in_
model_imp['feature_importance']= model_dt.feature_importances_
model_imp.sort_values(by ='feature_importance',ascending=False)

# plot_tree 시각화
from sklearn.tree import plot_tree
plt.figure(figsize=(35,10))
a = plot_tree(model_dt, 
              feature_names= model_dt.feature_names_in_,          
              # feature_names display
              class_names =  train_df_hk_3['car_type'].unique(), 
              # class_names display
              filled=True,                                       
              # color
              rounded=True,
              max_depth=4,                                      # display max_depth= 4
              fontsize=14)
```
[분기점을 확인하기 위한 시각화코드]
```python
from sklearn.tree import DecisionTreeClassifier, export_text, plot_tree

model = DecisionTreeClassifier()
model.fit(df[['Age','Na_to_K','Sex_cd','BP_cd','Ch_cd']],df['Drug'])

#텍스트로확인
export_text(model, feature_names= ['Age','Na_to_K','Sex_cd','BP_cd','Ch_cd'] )

#시각화로 확인
plot_tree(model, max_depth = 2,
         feature_names= ['Age','Na_to_K','Sex_cd','BP_cd','Ch_cd'],
         class_names= df['Drug'].unique(),
         precision = 3) # max_depth : 시각화 깊이 지정, _names : 데이터변수명 매칭, precision : 소수점자리 지정
```

<br>

## <b>KNN</b>
- 비모수 방식
- 분류/회귀 모두 가능
- 동률을 막기 위해 k값은 보통 홀수로 정함 (1에 가까울 수록 과적합)
- '거리'개념을 사용하는 알고리즘으로, 표준화/정규화 사용 필수
- 거리기준은 일반적으로 맨허턴거리 혹은 유클리안 거리 사용
```python
from sklearn.neighbors import KNeighborsClassifier,KNeighborsRegressor

#Classifier
df2 = pd.read_csv('./data/diabetes.csv')
df2['is_preg'] = (df2['Pregnancies'] > 0) + 0

X = df2[['Pregnancies', 'Glucose', 'BloodPressure','Insulin','BMI']]
Y = df2[['is_preg']]

from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(X, Y, random_state = 123, test_size = 0.2)

k = [3,5,10,20]
score = []

for i in k:
    model_kc = KNeighborsClassifier(n_neighbors = i)
    model_kc.fit(x_train, y_train)
    pred_g = model_kc.predict(x_test)
    score.append(accuracy_score(y_test,pred_g))
    print('k가',i,'일때 :',accuracy_score(y_test,pred_g))

result= pd.DataFrame()
result['k'] = k
result['score'] = score

result

#for문을 활용하여 K 파라미터값을 여러개 줘보고, f1score, accuracy_score 등 점수가 높은 값을 찾는다. 또는 random_search / grid_search 활용
```  





<br><br><br><br>


## <b>모델평가</b>
<b>1. 수치형</b>
- R-square(결정계수)
- MAE
   ```python
   from sklearn.metrics import mean_absolute_error
   mean_absolute_error(y실측값, y예측값)
   ```
- MSE
   ```python
   from sklearn.metrics import mean_squared_error
   mean_squared_error(y실측값, y예측값)
   ```
- RMSE
   ```python
   mean_squared_error(y실측값, y예측값) ** 0.5
   ```

<b>2. 범주형</b>

- f1-score (조화평균)<br>
(작은 값 쪽에 Advantage를 주어 평균선이 더 가까워짐) <br>
f1은 어느시점까지 상승했다가 하강하는 특징을 가지고 있어, 점수가 가장 높은 지점이 recall과 precision의 적정하게 조화로운 값이다.<br>
공식 : 2* ( (Recall * Precision )/ Recall + Precision)
   ```python
   from sklearn.metrics import f1_score
   ```
- 정확도
   ```python
   from sklearn.metrics import accuracy_score
   ```
- 정밀도
  ```python
  from sklearn.metrics import precision_score
  precision_score(y실측치, y예측치, pos_label = '컬럼명')
  #pos_label : 어느 데이터 기준으로 볼 건지 설정 가능 
  ```
- 재현율
  ```python
  from sklearn.metrics import recall_score
  ```
- AUC 
  ```python
  from sklearn.metrics import roc_auc_score
  ```
- 총 요약표
  ```python
  from sklearn.metrics import classification_report
  #print()로 출력
  ```


<br><br> 
<b> [TIP1] 유용한 코드 </b> <br>
1. Sample data 만들기 <br>
```df.pd.DataFrame[[0],]``` <br>
2. 2차원 데이터로 만들기 <br>
```[[]]``` <br>
```.values.reshape(-1,1)```


<br><br>


<b> [TIP2] 활용 시나리오 </b> <br>


1.  회사경영진과 버스기사간 연봉과 근무 처우 관련 협상
     1) 지선, 간선 버스의 경우 노선당 연수익이 10억이하인 경우 배차간격조정, 노선변경 등 수익구조 개선이 필요하다고 한다. 승객 1명당 기대수익이 천원이라고 했을 때, 몇개의 버스 노선이 대상인가?
         * 접근법 : .isin()을 통해 지선,간선 버스를 필터링하고, 시간대별 인원수 인 열들을 합산하기위해 sum(axis=1) #2차원에서 열들의 합은 axis = 1
          

     2) 노선별 정류장 개수가 많은지, 그에따라 버스기사 확충또는 배차시간을 조정해야 하는지 파악하기 위해,
        노선별 정류장 개수를 파악하고,  개수의 차이가 통계적으로 유의한지 확인
        * 접근법 :  노선별 평균 정류장 개수를 산출하고, ttest_ind 검정을 실시한다.
     
     3) 출퇴근 시간 (7시-9시) 배차간격을 조정하기위해 우선적으로 정류소별 출근시간 승차 패턴을 파악하고자한다.
   지선버스 노선을 대상으로 각 정류장별 승차인원을 계층적 군집분석을 활용하여 6개의 군집으로 분할 하였을때, 
    출근시간대에 승차인원이 가장 많은 정류소 군집의 번호는 몇번인가?

          * 접근법 : 지선노선 필터링 -> (월별, 정류소별)로 정리되어있는 자료를 (정류소별)로 합산하기    위해 특정변수명 지정없이 groupby(‘정류소’).sum() 을 바로 사용 ->  melt를 사용해 long form 으로 변환 후 정규화 <br>
                   이때 Scaler를 groupby된 데이터에 바로 적용하고 싶을 경우에
         사용자함수를 활용하여 scaler를 직접 만들고, fitting 없이 바로 transform하여 사용한다.
            ```python
            def nor_minmax(x):
               result = (x-x.min()) /( x.max() - x.min())
               return result

            df.groupby(‘정류소’)[‘인원수’].transform(nor_minmax)
            ```

            그다음 계층적분석분석을 실시 (n_clusters = 6) ->  model.labels_ 활용하여 군집 추출

<br><br>

2. 금융 정보
    1) 총 송금액이 고육수준, 혼인여부에 따라 어떤 특징을 보이는지 분산분석  후, 
        일회당 평균송금액을 종속변수로 헀을때 독립변수간 교호 작용 여부 확인
    2) 부양가족, 나이, 학력, 성별, 결혼여부, 가입기간, 누적송금횟수로 신용한도 결정하기
<br><br>

3. 홍보 상품 목록선정, 매장 매대 진열/ 소비자 동선 수정
    1) 2014년에는 매출이 발생했으나, 2015년에는 매출이 발생하지 않은 품목?
         * 접근법 :  2014년 데이터에  ['cnt'] = 1 로 파생변수 생성 후, <br> 
            데이터셋을 년도,아이템별로 groupby하여 카운트해주고 그결과를 년도별로 pivoting  

    1) 성별에 따라 상품 구매성향이 다르다는 가정을 확인하기 위해 연관분석 실시 <br>
         * 접근법 :  결과절 품목을 각각 확인



<br><br><br>
---------------------------------------

<b>실기 문제풀이</b>
```python
import pandas as pd
import numpy as np
df = pd.read_csv('./data/DS_Sample_3.csv',encoding ='utf-8')

movie3 = df.copy()
movie3['AirDate'] = pd.to_datetime(movie3['AirDate'])

movie3['group'] = np.where(movie3['AirDate'].dt.year.isin([2005,2006,2007]),'A',
         np.where(movie3['AirDate'].dt.year.isin([2008,2009,2010]),'B','C'))
#between(2005,2007)도 됨

movie3['success'] = movie3['Rating'] * movie3['Num_Votes'] 

movie3.groupby('DirectedBy')['success'].mean().max().astype(int)

from statsmodels.stats.anova import anova_lm 
from statsmodels.formula.api import ols

model = ols(formula = 'Num_Votes~ group', data= movie3).fit()
anova_lm(model)['F'][0] + anova_lm(model)['df'][0]
```