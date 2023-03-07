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
    [numpy]
 1. 함수 및 메서드
    type(): 자료형 정보 (list, array 등) 
    .dtype : 데이터 타입정보 (int, float 등)
    df.select_dtypes("object") : df 데이터 중 'object'타입의 데이터들만 추출
    .iloc[:, df.dtypes =='int64'] : 상동
    .reset_index : 인덱스 초기화
    .value_counts()
    .sort_values(by=[''])

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
 17. Array 생성
     np.array([1,2,3])
     np.zeros((3,3))

 18. .tolist()
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


 2. [조건부확률]은 crosstab을 활용하여 푼다.
    pd.crosstab(df['a'], df['b'])

 3. [중심극한 정리 증명]
   ```python
   import matplotlib.pyplot as plt
   import numpy as np
   import random


   avg_values = []
   for i in range (1,10000): # 횟수를 증가시키면 정규분포로 변화
   random_sample = random.sample(range(1, 1000),100)
   x = np.mean(random_sample)
   avg_values.append(x)

   plt.hist(avg_values, bins = 100)
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
  > 샘플 추출은 단순임의 추출이 기본이지만, groupby 를 사용하면 층화 표본추출 기능을 구현할 수 있다. ]
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

## <b>T-TEST 검정</b>
> 두 집단간의 평균비교

<br><br>

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
* 정규성을 만족하지 못하는 경우 wilcoxon rank sum test (순위합검정) 사용
* 등분산 가정을 만족하는 경우, equal_var 인자에 True를 할당
* ttest_ind() 사용 <br>
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
<br>
<b>3. Paired sample t-test</b>

 * 동시간대 등 환경을 동일하게 맞춰준 동일한 모집단에서부터 추출된  두 집단간 차이가 있는지 검정
 * 표본이 정규성을 만족하지 못하는 경우 wilcoxon rank sum test (순위합검정) 사용
 * Scipy -ttest_rel() 사용
 * ```활용: 동년, 동월, 동시간대 이용객 대상으로 비회원의 대여량과 회원의 자전거 대여량의 평균차이 검정```



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


> 예제 
 <br>
1.
   temp, atemp, humidity, registered의 상관 계수중 가장 높은것은 ?
   ```python
   df_bike[['temp','atemp','humidity','registered']].corr()
   ``` 
<br>

1. 날씨가 맑은날(weather = 1) 과 그렇지 않은날 온도(temp)와 자전거 대여 숫자(casual)의 상관계수의 절대값은 얼마인가 ?
      ```python
      df_bike[(df_bike['weather'] == 1)][['temp','casual']].corr()
      ```
```!! corr는 DF로 추출해야함 [[]] !!```


<br>

## <b>독립성(연관성) 검정</b> ```[카이제곱검정]```

   - 적합도, 독립성, 동질성 검정 사전에 진행 필요
   - 검정통계량 : 카이제곱 ∑ ((관측도수 - 기대도수)² / 기대도수)
   - crosstab (빈도표) 자료 활용 필요
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

# Machine Learning

## <b>Pre-processing</b>
### <b>1. Scaling</b>

 - 스케일링 전후 비교를 위해 histogram 2가지

   ```python
   df_hk.hist()

   sns.histplot(df_hk[['height','age', 'salary' , 'expenditure']])
   ```



 -  min_max scaling (최소-최대 변환) (범위:0~1) <br>
      ```python
      from sklearn.preprocessing import MinMaxScaler, StandardScaler
      m_scaler = MinMaxScaler()

      model = m_scaler.fit(df_hk[['height','age', 'salary' , 'expenditure']])
      x_train_scaled = model.transform(df_hk[['height','age', 'salary' , 'expenditure']])
      df_hk_minmax = pd.DataFrame(x_train_scaled, columns= ['height','age', 'salary' , 'expenditure'])
      df_hk_minmax 
      ```

 -  standard scaling (Z-score 변환) (범위 : 0 중심, -∞ ~ +∞)
      ```python
      from sklearn.preprocessing import MinMaxScaler, StandardScaler
      s_scaler = StandardScaler()

      model = s_scaler.fit(df_hk[['height','age', 'salary' , 'expenditure']])
      x_train_scaled = model.transform(df_hk[['height','age', 'salary' , 'expenditure']])
      df_hk_stand = pd.DataFrame(x_train_scaled, columns= ['height','age', 'salary' , 'expenditure'])
      df_hk_stand 
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

## <b>계층적 군집분석</b>
- 데이터변동에 민감
- 거리기반(유사도)로 묶기
- 데이터개수가 많은경우 연산에 많은 시간이 소요 (5천개~만개를 넘기는데이터에는 비권장)
- 계층도(Dendrogram): 데이터간 거리를 기반으로 도식화한 도표
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
#(default) method = single 위 모델과 일치 시켜줌 > ward로 변경
dendrogram(link)
plt.show()
```

## <b>비계층적 군집분석</b>
- 임의의 k점을 기반으로 가까운 거리의 데이터를 묶음
- k를 확정하기 위해 여러번의 시행착오 필요
- 결과를 고정하기 위해 seed설정 필요
```python
import pandas as pd
df = pd.read_csv('./data/iris.csv')
from sklearn.cluster import KMeans

model = KMeans(n_clusters = 3, random_state = 123).fit(df.iloc[:,:-1])

df['cluster'] = model.labels_
df.groupby('cluster').mean() # model.cluster_centers_ 와 기능동일, 단 해당 코드는 컬럼이 없어 별도 df작업을 해줘야하기 때문에, groupby를 직접 해주는 것이 더 편리
```
<br><br>

## <b>단순선형회귀</b>
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
<br><br>

## <b>다중선형회귀</b>
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

<br><br><br><br>
### <b>모델평가</b>
- R-square(결정계수)
- MAE
   ```python
   from sklearn.metrics import mean_absolute_error
   mean_absolute_error(y예측값, y실측값)
   ```
- MSE
   ```python
   from sklearn.metrics import mean_squared_error
   mean_squared_error(y예측값, y실측값)
   ```
- RMSE
   ```python
   mean_squared_error(y예측값, y실측값) ** 0.5
   ```
<br><br><br><br><br>
---------

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