# ML 기초
> Machine Learning (인공지능) 기초학습   

<br>

## Jupyter Notebook 사용 tip
1. shift + tab + tab : 함수설명
2. Command + 좌우 >> 문장 끝으로 이동 / alt + 좌우 : 문단 끝으로 이동
3. x = 행삭제
4. z = 행삭제 취소


<br>

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



```