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

[code]
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

1. t_test_1sample


* t-test를 할 data의 mean 근처의 값으로 t-test후 t통계량과 p_value 관찰 #모집단 평균을 알고 있음
```python 
from scipy.stats import ttest_1samp
ttest_1samp(df_hk['age'], popmean = 39.24)[1] < 0.05  

# 결과값 : TtestResult(statistic=0.0, pvalue=1.0, df=249)
1.0 < 0.05
# 결과 : False, 결과 해석: 95% 신뢰수준으로 100% 일치
# popmean: 모집단의 평균
```

2. Two sample t-test
```python
from scipy.stats import ttest_ind
ttest_ind(df_hk[(df_hk['company']=='A')].salary , df_hk[(df_hk['company']=='B')].salary)

#결과 : Ttest_indResult(statistic=5.941362455469809, pvalue=1.2532322871358408e-08)

```




   2-1.  sample t-test (A>=B) #less_귀무가설(B)보다 작다(하단측검정)
   ```python
   ttest_ind(df_hk[(df_hk['company']=='A')].salary , df_hk[(df_hk['company']=='B')].salary,
         alternative='less')

   #결과값: Ttest_indResult(statistic=5.941362455469809, pvalue=0.9999999937338386)
   ```

  2-2. sample t-test (A<=B) #greater_귀무가설(B)보다 크다(상단측검정)
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