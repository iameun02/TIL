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

## 가설검정

1.  t_test_1sample


* t-test를 할 data의 mean 근처의 값으로 t-test후 t통계량과 p_value 관찰 #모집단 평균을 알고 있음
```python 
from scipy.stats import ttest_1samp
ttest_1samp(df_hk['age'], popmean = 39.24)[1] < 0.05  

# 결과값 : TtestResult(statistic=0.0, pvalue=1.0, df=249)
1.0 < 0.05
# 결과 : False, 결과 해석: 95% 신뢰수준으로 100% 일치
```
<b> popmean: 모집단의 추정모수  즉, 𝒎₁</b>

2. Two sample t-test
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

3. ANOVA 검정
> 수치가 통계적으로 동질적인지 이질적인지 검증하기 위해 현업에서 많이 사용됨 <br>
> (금,토,일이 같은 '주말'인지 or 80점과 81점이 동일한 수준인지 등) <br>
> 그룹이 2개 이상 일때 사용하며, 2개인 경우는 t-test의 결과값과 동일하게 나온다. <br>
> 일원분산분석이 아니라 다중분산분석일 경우 반복문 사용필요 <br>

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
<b>[statsmodels]</b> <br>
#분산분석표 제공
```python
# ANOVA statsmodels 사용
from statsmodels.formula.api import ols
from statsmodels.stats.anova import anova_lm
from statsmodels.stats.multicomp import pairwise_tukeyhsd

model = ols(formula = 'salary~ company', data= df_hk).fit() #formula: 종속변수~독립변수 

anova_lm(model)
```

3-1. 사후검정 #tukey

```python
#endog : y label
#alpha : 유의 수준 0.05
from statsmodels.stats.multicomp import pairwise_tukeyhsd

posthoc = pairwise_tukeyhsd(df_hk['salary'], df_hk['company'], alpha =0.05 ) #종속,독립 순

print(posthoc) #변수에 할당해서 프린트 필요
```
결과해석 : reject 가 True면 다르다. False면 같다. <br>
T-test 경우는 결과 값이 False로 나오는게 다르다는 것이다.<br>

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

1. 상관분석
  - 검정 통계량 : t



<b>[corr()]</b> <br>
```python
(1) # pearsonr, spearmanr, kendalltau
df_hk.corr() #default method = pearson
df_hk.corr(method='pearson')
df_hk.corr(method='kendall')
df_hk.corr(method='spearman')
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

1. 카이제곱
   -  적합도, 독립성, 동질성 검정 사전에 진행 필요
   - 검정통계량 : 카이제곱 ∑ ((관측도수 - 기대도수)² / 기대도수)


```[독립성 검정]``` <br>
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

## Scaling

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