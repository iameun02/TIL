# 
<br>

## 1. 확률과 확률 분포
### 1. 확률의 개념과 특징
1) 확률의 규칙
 * 여사건의 확률 <br>
   P(Ac) : 1 - P(A) <br>
 * 합사건의 확률 <br>
   P(A ∪ B) = P(A) + P(B) - P(A ∩ B) <br>
 * 곱사건의 확률 <br>
   P(A ∩ B) <br>
2) 조건부 확률의 정의 <br>
   P(A|B) = P(A ∩ B) / P(B) <br>
3) 독립 사건의 정의
   두사건 A와 B가 다음 중 하나를 만족시키면 서로 독립이라고 함.
   (단 P(A)>0, P(B)>0) <br>
   - P(A|B) = P(A)
   - P(A ∩ B) = P(A) * P(B)
   - P(B|A) = P(B)
   <br><br>
### 2. 베이즈 정리 
  
   
!Notation (A: 결과, B₁~BK : 원인) <br>

1) 베이즈 정리의 활용 : 원인별 결과의 주건부 확률이 주어 졌을 때, 결과를 전제로 각 원인의 조건부 확률을 도출.
2) K개의 사건 B₁....BK는 서로 상호배반이며,
   B₁ ∪ ... ∪ BK = S라고 함.
   이때 사건 A가 일어났다는 조건 하에서 사건 Bj가 일어날 확률은 다음과 같음.
   P(Bj|A) = P(A ∩ Bj) / P(A)
   = P(Bj)P(A|Bj) / P(B₁)P(A|B₁)+...+P(Bk)p(A|Bk) 
3) 전제조건
 * 표본공간의 분할
   - k개의 원인들은 서로 상호 배반적이다.
   - k개의 원인들을 합쳤을때 전체집합 S가 된다.
 * 전확률 공식
   -  S라는 표본공간에서 정의되는 임의의 사건 A에 대하여 다음이 성립
   -  P(A)= P(A ∩ B₁) + ... + P(A ∩ B₁)
      = P(B₁)P(A|B₁) + ... + P(BK)p(A|BK) -- 각 원인별로 결과가 발생할 확률들의 합
   -  
4) 예제 <br>
      OO 공장에서 생산되는 제품은 기계 A.B.C 3가지에 의해 생산된다.
      전체 생산된 제품중에 불량이 발생 되었을 때 A로부터 발생 되었을 확률은 얼마일까? <br>
      각 기계 별 생산률 <br> 
      A : 0.5 , B : 0.3, C : 0.2 <br>
      각 기계 별 불량률 <br>
      A : 0.10, B : 0.15, C : 0.20 <br>
```
    P(A)P(B₁|A)
     / P(A)P(B₁|A) + P(B)P(B₂|B) + P(C)P(B₃|C) = 0.3703
```
<br><br>

### 3. 확률변수와 확률분포, 분포의 특성치
1) 확률변수 개념 <br>
   표본공간에서 정의된 실수값 함수.
   * 이산형 확률변수 : 확률변수가 취할 수 있는 값이 셀수 있는 경우<br>
   * 연속형 확률변수 : 주어진 구간에서 모든 실수 값을 취할 수 있어 셀수 없는 경우  0 < x < ∞ <br> 
2) 확률분포함수
   * 확률질량함수(pmf) : 이산형 확률변수 의 경우, 특정값 x에 대하여 나올 확률을 f(x)함수로 나타낸 것 _직선함수
   * 확률밀도함수(pdf) : 연속형 확률변수 의 경우, 특정값 x의 확률은 못구하지만, (무한대가 존재하기 때문에 모수가 무한대일 경우, 0으로 수렴) <br>
     x가 임의의 어떤 구간에 포함될 확률을 정의 할수 있다. (전체 확률에서 구간별 확률은 구할수 있기 때문)<br>
     , 또한 연속형 확률변수는 특정값에서의 확률이 0이기 때문에 등호의 유무는 확률에 영향을 주지 않음 _곡선함수
   * 누적분포함수 : X의 확률밀도함수가 f(x)일 때,  X의 누적분포함수는 F(x) 대문자로 표기하며, X⪳x 인 모든 X에 대한 f(x)의 적분 값이 됨 _곡선함수
   - f(x) : 높이 
3) 확률분포함수의 특성치 (X : 확률변수)
   * 기대값 ( E[X] | 𝑚 ) :  분포의 무게중심, 중심위치를 나타냄 (모평균)
   * 분산 : 분포의 산포를 나타냄 (모분산)
     V[X] = 𝜎² = E[(X - 𝒎)²]
      - 𝜎²가 큰 경우 : 중심으로부터 멀리 떨어진 X가 나올 가능성이 높음
      - 𝜎²가 작은 경우 : 중심으로부터 가까이 있는 X가 나올 가능성이 높음
   * 표준변차 : 분산의 제곱근. 단위가 보정됨
     S[X] = 𝜎 =√[x]
<br><br>

### 4. 이항분포, 포아송분포, 지수분포, 감마분포
1. 이산형분포
   1) 이항분포<br>
      * 베르누이 시행 : '성공' 또는 '실패' 오직 두가직 가능한 결과만 가짐 (eg.동전 던지기)
      * 이항확률변수 :  베르누이 시행을 독립적으로 n번 반복하는 실험
      * X : n번 시행중 '성공'횟수로 정의 (0과 n사이의 정수값)
      * 확률질량함수 
        f(x) = P(X=x) =
         (n<br>
          x) p^x(1-p)^(n-x) 
        - 각 시행마다 성공일 확률 구하는 공식  <br>
        X~Bin[n,p]  
        (n:시행횟수, p:성공횟수_p가 0에 가까울 수록 왼쪽에 치우친 그래프, 1에 가까울 수록 오른쪽에 치우친 그래프)
      * 이항분포의 특성치 
        - E[X] =np (각 시행마다 성공일 확률의 평균)
        - V[X] = np(1-p)
   2) 포아송분포 <br>
      단위 시간(부피,공간..등)에 사건 A가 발생하는 횟수 X _보통은 확률이 희박한경우 사용 
     
      f(x) = P(X=x) = 𝒆(-𝒎)𝒎^x /x!
      E[x] = V[x]  = 𝒎
      (eg.하루 고속도로에서 대형교통사고가 3번 일어날 확률은? 단 하루평균은 2회이다.
        => (𝒆-² 2³) / 3!
      (eg. 한시간에 평균 2명 손님이 방문하는 가게에 손님이 한시간에 아무도 안 올 확률
        =>  (𝒆-² 2⁰) / 0! = 𝒆² = 0.1353)
2. 연속형분포
   1) 지수분포
      내가 관심있는 사건이 발생할때까지 걸리는 시간 (포아송모수와 지수모수는 역의 관계) <br>
      포아송 평균발생횟수가 𝒎 은 소요시간 𝝀 = 1/𝒎 <br>
      f(x) = 1/𝝀 exp (-x/𝝀) <br>
     * 지수분포의 특성치
       X~EXP[𝝀]인 경우 E[X] = 𝝀
   2) 감마분포
      K번째 사건이 발생할 때까지 걸리는 시간 _연속형 밀도함수 <br>
      X~GAMMA[K,𝜽] (K:shape 모수, 𝜽:척도모수) <br>
      * 감마분포의 특성치
      X~GAMMA[K,𝜽]
      E[X] = K𝜽
      V[X] = K𝜽^2
<br><br>

### 5. 정규분포, 표준정규분포

1. 정규분포
   확률변수 X가 평균이 𝒎, 분산이 𝜎²이고 다음의 확률 밀도함수를 가질때, X는 정규분포를 따른다. <br>
   𝑓(𝑥) = 1 / √2𝜋𝜎  * 𝑒 ^ -(𝑥-𝑚)²/2𝜎² <br> 
   
   𝑿 ~𝑵 [𝑚,𝜎²] <br>
   𝑚 (중심위치모수) : 분포의 중심 , 𝜎²(척도모수) : 산포의 크기와 비례 <br>

   * 정규분포의 특성치 (모수가 됨)
   - 𝑬[𝑿] = 𝑚
   - 𝑽[𝑿] = 𝜎²
   
2. 표준정규분포
   정규분포로의 선형불변성에 의해 통해 만들어지게되미 <br>
   𝒁 = 𝑿-𝑚/𝜎 (선형변환시) ~𝑵[0,1] 이되며, 이때의 평균이 0 분산이 1인 정규분포 <br>
   즉, X의 값은 항상 𝑚와 𝜎의 정보를 필요로 하기때문에, X를 선형변환 ((X-기대값) /표준편차) 하여 <br>
   Z값으로 표준화 후 확률을 구함 (두확률은 동일) <br>
   0을 중심으로 완벽한 대칭형의 종모양 <br>
   * 선형변환시 기대값과 분산의 성질
     E[𝒂𝒙 + 𝒃] = 𝒂𝑬[𝑿] +𝒃
     𝑽[𝑎𝑥 + 𝑏] = 𝑎²𝑽[𝑿]

   * (1-𝛼)분위수 
    - 𝒁 0.05= 1.645,  𝒁 0.95 = -1.645
    - 𝒁 0.025= 1.96,  𝒁 0.975 =-1.96
  
<br><br>

### 6. 카이제곱분포, t분포, f분포

1. 카이제곱 분포
   서로 독립인 표준정규확률분포들에서 확률변수 k개가 제곱해서 더해져 유도된 밀도함수. <br>
   이 때 k는 카이제곱의 모수라고 부르고, 자유도가 된다.
   * 특성치
   - 𝑬[𝑿] =  𝑘
   - 𝑽[𝑿] = 2𝑘
   * (1-𝛼)분위수 
   - 𝓧² 0.05,10 : 𝓧가 𝓧²[10]을 따를 때  𝓧²[10]보다 큰 값이 나올 확률이 0.05 (= 𝜶) 이다.
2. t분포
   서로 독립인 표준정규분포의 확률변수 𝒁 와 카이제곱분포의 확률변수 𝑼 를 섞어서 함수를 만듬  𝑿= 𝒁 / √(𝑼/𝒌)<br>
   이 함수의 변수들의 값들을 𝑿라고 했을때 𝑿의 분포를 t분포라고 함. <br>
   t분포의 자유도 𝒌는 카이제곱의 자유도가 그대로 전달된다. <br>
   0을 중심으로 완벽한 대칭형의 종모양  <br>
   * 특성치
   - 𝑬[𝑿] =  0
   - 𝑽[𝑿] = 𝑘 / 𝑘-2 (단 𝑘>2)
    ✓ 표준정규분포는 기대값이 0 , 분산이 1인 반면, t분포는 기대값이 0 분산이 1보다 조금 크다 <br>
      => t분포가 봉우리는 조금 더 낮고 꼬리가 두꺼움 <br>
      또한 자유도 𝑘 가 ∞ 로 커질경우 1로 수렴하게되어, 결국 표준정규분포로 수렴된다.
   * (1-𝛼)분위수 (표기법: 분포명, 오른꼬리확률 𝜶, 분포에필요한모수 𝓽𝜶,𝓴)
   - 𝓽 0.05,7 : 자유도가 7인 𝓽 분포에서 오른꼬리 확률이 0.05에 해당되는 값 <br>
     이는 𝓽 분포는 대칭형이기 떄문에, 𝓽 0.95,7 값과 부호만 바꿔주면 동일하게 된다.
3. f분포
   서로독립인 자유도가 𝒌₁인 카이제곱분포 𝑼와 자유도가 𝒌₂인 카이제곱분포 𝑽 2개로부터 나온 <br>
   값을 이용하여 만든 함수 𝑿 = (𝑼/𝒌₁)/(𝑽/𝒌₂), 이 함수로부터 나온 변수들을 𝑿라고 했을때 𝑿들의 분포를 𝒇분포라고함.<br>
   자유도는 순서대로 분자자유도 : 𝒌₁ , 분모자유도 𝒌₂ 가 된다.
   * 특성치 (참고용..)
   - 𝑬[𝑿] =  𝒌₂ / (𝒌₂-2)
   - 𝑽[𝑿] = 2𝒌₂²(𝒌₁+𝒌₂-2) / 𝒌₁(𝒌₂-2)²(𝒌₂-4)
   * (1-𝛼)분위수 𝑭 𝛼,𝒌₁,𝒌₂ (순서중요!)
  
<br><br>

## 2. 탐색적 데이터 분석
### 1. 그래프에 의한 기술통계
1. 데이터 시각화 개요
1) 질적 자료인 경우 <br>
      - 명목형 : 혈액형, 성별 <br>
      - 순서형 : 학점, 사이즈(s,m,l), 상중하 <br>
    <br>
      (1) 1개변수 (값의 분포파악) : 바차트(막대그림), 파이차트 <br> 
          * 도수분포표 : 카테고리별 빈도(도수) <br>

      (2) 2개변수 (연관성파악): 히트맵, 스택드컬럼차트(누적)  
   <br>
          * 분할표 : 도수분포표를 2차원 (행렬) 으로 그린 것
<br>
1) 양적 자료인 경우 (숫자로 표현) <br>
      - 이산형 <br>
      - 연속형 <br><br>
  
      (1) 1개변수 (값의분포파악) : 히스토그램, 박스플롯, 라인차트, qq플롯 <br>

         - 히스토그램 : 구간별 빈도 (연속된 실수라서 구간을 먼저 지정 해줘야 한다. (beans)_ 막대가 붙어있는 것이 특징) <br>
         - 박스플롯 : 4분위수 개념 이용, 이상치 확인 가능 <br>
         - qq플롯 :  변수 하나가 주어졌을때 이 변수가, 정규분포를 따르는가 확인하는 그래프 <br>
  
                      표본분위수 (Quantile)와 이론분위수 (Quantile, 경험누적확률) 관계가 완벽한 선형관계 <br>
                      비선형일경우 한쪽으로 치우친 그래프의 형태임을 알수 있다. <br>
                      (오른꼬리가 긴경우 > qq플롯: 오목한 그래프 _ qq플롯 상에서 이론분위수보다 표본 분위수 값이 큰 형태 <br>
                       / 왼꼬리가 긴경우 > qq플롯 : 볼록한 그래프) <br>
                      * 경험누적확률 : 표본분위수 값들에 대하여 그 값보다 작거나 같은 확률을 더한것. <br>
       
      (2) 2개변수 (연관선파악) : 산점도 <br>
         - 산점도 : 두 변수간에 연관성을 알수 있다.  <br>
<br><br><br>

### 2. 수치적기술통계 (변동성)
1. 중심 위치 척도
1) 평균
2) 중위수(중앙값)
    - 홀수 : (𝐧+1)/2 <br>
    - 짝수 : (𝐧/2) 값과 (𝐧/2)+1 의 평균 <br>
3)  최빈값
      ``` 
      분포가 오른꼬리가 길 경우 : 최빈값 < 중위수 < 평균 
      분포가 왼꼬리가 길 경우 : 평균 < 중위수 < 최빈값 
      분포가 대칭인 경우 : 최빈값 = 중위수 = 평균 
      ```

<br>
    2. 상대적 위치 척도 <br>
    
   1. 사분위수 <br>   
          * Q1 : 1분위수 <br>
          * Q2 : 2분위수 <br>
          * Q3 : 3분위수 <br>
      <br>
   
 2.  변동성 척도 <br>
      1. 범위 (𝑚𝑖𝑛,𝑚𝑎𝑥) <br>
      2. 사분위간 범위 (𝑸3-𝑸1) : 중간 50%에 해당되는 범위 <br>
      3. 표본분산 : 𝒔 = (𝒙값 - 𝑥평균)² /𝒏-1 <br>
      4. 표본 표준편차 : 𝒔 = √𝒔² <br>
        * 분산은 차이가 -가 나오기때문에 제곱을 해주고, 이에대한 단위조정개념으로 표준편차를 구한다. <br>
      5. 변동계수 : 평균대비 표준편차가 몇배인지 보여주는 지표
       𝑐𝑣 = 𝑠/ 𝑥평균
       - 자료의 단위가 다를때, 스케일의 차이가 큰 경우 활용됨

 <br><br>
3. 형태 척도 <br>
      
 1. 왜도 : 분포의 비대칭 정도를 나타내는 척도 <br>
       - 음의왜도 : 왼쪽으로 꼬리가 김, 양의왜도 : 오른쪽으로 꼬리가 김 <br>
  2. 첨도 : 분포의 중심에서 뾰족함 정도를 나타내는 척도 <br>
       - 정규분포일때는 첨도= 0, 첨도가 양수일 수록 뾰족하고 긴 형태 <br>
  <br><br>
### 2. 수치적기술통계 (연관성)
  1. 선형적 연관성 척도 <br>
   1) 표본 공분산
      - 𝑆𝑥𝑦 = sum((𝑥𝒊 - 𝒙평균)(𝒚𝑖 - 𝒚평균)) /(𝒏-1) <br> 
      - 선형관계의 방향 <br>
        𝑆𝑥𝑦 > 0 인 경우 : 양의 선형관계 <br>
        𝑆𝑥𝑦 < 0 인 경우 : 음의 선형관계 <br>
      - 선형관계의 강도 : 공분산과 표준편차의 곱과 비교함으로 상대적 강도를 알수있음 <br> 공분산 단독으로는 강도를 알수 없음. <br>
      또한 단위의존적이며, 공분산이 0이라해도 비선형의 관계를 가질수도 있기때문에 독립이라고 말할 수 없다. <br>
       
         -𝑆𝑥𝑆𝑦 < 𝑆𝑥𝑦 < +𝑆𝑥𝑆𝑦 <br>

   2) 표본 상관계수 
      - 공분산의 단점을 보완 <br>
        ① 피어슨의 상관계수 <br>
          - 정규분포를 따르는 숫자형 변수의 연관성을 추론할때 활용
          - r𝒙𝒚 = 𝑆𝑥𝑦 / 𝑆𝑥𝑆𝑦 (-1 ≤ r𝒙𝒚 ≤ 1) <br>
          - 선형관계 방향 <br>
            r𝒙𝒚 > 0 인 경우 : 양의 선형관계 <br>
            r𝒙𝒚 < 0 인 경우 : 음의 선형관계 <br>
          - 선형관계 강도 : 0에 가까울수록 약하고 1에 가까울수록 강함(직관적)<br> 1 인경우 완벽한 선형관계로 직선으로 나타난다. <br>
       
        ② 스피어만의 상관계수 <br>
          - 서열번수이거나, 정규분포를 따르지 않는 숫자형 변수 연관성을 파악하는데 사용되며, <br>원자료 값의 '순위'를 구한뒤 순위에 대하여 상관계수를 구함.<br> 그 외 선형관계 방향, 강도 등 피어슨과 동일 <br>
  
         ③ 켄달의 상관계수  
      <br>
         - 정규분포를 벗어난 두 변수 '순위'의 일치 정도를 측정 <br> n개의 자료 중 2개씩 짝지어 추출하여, 한쌍이 같은 방향으로 움직이는지 (부합), 다른방향으로 움직이는지 (비부합) 측정하고, <br> 그 결과의 비중을 측정한다.<br> 그 외 선형관계 방향, 강도 등 피어슨과 동일 <br>
  <br><br>
  
  
  
## 3. 추정과 검정
### 1. 통계적 추론 개요, 표본추출법
1. 통계적 추론 개요 <br>
  1) 모집단 : 관심대상 전체  (eg.모든 전구 수명값)<br>
     - 𝑓(𝑥) 로부터 확률표본 𝑋₁, 𝑋₂, 𝑋₃... 은
       서로 독립이며 모두 동일하게 𝑓(𝑥) >모집단 분포를 가짐 => 'iid표본' <br>
       (확률표본이라는 것은 𝑋₁, 𝑋₂, 𝑋₃... 가 하나의 변수가아니라
        저 set가 여러번 반복되어 각 각 분포를 형성하고 있다는 것, <br>
        즉 전구 30개의 표본을 추출하는것을 n번 반복하여, 첫번째 추출~30번째 추출하는 set가 n개 있음<br>
        n개의 각 set 평균들의 집합을 𝑿 bar로 표기하며, <br>
        소문자 𝑥 bar일경우 1 set의 평균을 의미한다.)
  2) 모수 :  '모집단 𝐗'의 특성치로 기대값, 분산, 표준편차, 상관계수 등에 해당 (eg. 전구 수명의 평균 𝓶) <br>
  3) 표본 : sampling 𝑿₁, 𝑿₂, 𝑿₃, 𝑿₄...(eg. 전구 30개)
  4) 표본 자료 : 𝒙₁, 𝒙₂, 𝒙₃, 𝒙₄...
  5) 통계량 : '표본'의 특성치 𝑿 bar (eg. 전구 30개의 평균)
  6) 표본평균 : 𝑿 bar
  7) 표본분포 : 통계량의 확률분포
  8) 통계적 추론 : 통계량의 정보로 모수를 추정
<br>

|모수 (𝜃) |통계량 (𝜃^)|
|---|---|
|𝓶 (모집단의 모평균)|𝐗 bar (표본평균|
|𝜎² (모집단의 모분산 𝑽[𝑿])|𝑆² (표본의 분산)|
|𝜎 (모집단의 표준편차)|𝑆 (표본표준편차)|

𝑬[𝑋 bar] = 𝒎   ```모집단의 기대값은 표본의 기대값과 같다``` <br>
𝑽[𝑿 bar] = 𝜎²/ 𝒏 ```표본의 분산은 모집단의 분산을 표본의 수로 나눈것과 같다. 이로인해 표본의 수가 커질수록 산포가 작아지며, 모집단과 더 가까워 진다는 것이 증명된다.``` 



<br>
2.  표본추출방법 <br>

1) 단순임의 추출법 (Simple Random Sampling) <br>
   -  난수표를 활용해 추출 <br>
  
2) 계통추출법 (systematic sampling) <br>
   - 𝒌개의 구간으로 나눈후, 구간마다 순서대로 하나씩 추출 (𝒌 =모집단원소 수 / 표본수) ==> 데이터가 사이클을 가질 경우 편향의 문제가 생김 <br>
  
3) 집락추출법 (cluster sampling)<br>
   - 분할된 cluster 들이 자체적으로 모집단을 잘반영할 수있게 이질적인 요소들이 골고루 섞여 있어 한 cluster를 추출함 <br>(층화추출보다 조사가 더 용이하며, 조사비용이 적게 든다.) <br>

4) 층화추출법 (stratified sampling) <br>
   - 분할된 stratum(계층)들이 동질적인 요소로 구성되어있어, 각 stratum로부터 모집단을 구성하는 비율에 맞춘 갯수만큼 추출함 
<br><br>

### 점추정과 구간추정
> 추정량 :  모수 𝜃 의 추정에 사용되는 추정량 (𝜃^)
1. 점추정 
   - 하나의 모수를 한개의 값으로 추정 



2. 구간추정
   - 모수가 포함되리라 기대되는 구간의 모수를 추정
   - 신뢰구간 (𝐿,𝑈) <br>
   ```𝑃[𝐿 ⪯ 𝜃 ⪯ 𝑈] = 1- 𝛼 ``` <br>
   ```0 ⪯ 𝛼 ⪯ 1``` <br>
   ```[𝐿,𝑈]이 신뢰구간, 1- 𝛼 를 신뢰수준이라고 함 ```
    이때 구간은 추정량(𝜃^)에 의존적이기 때문에, 그 함수를 따른다.
    - 예시
      ```
      (조건1)정규분포를 따르는 모집단에 대하여 모평균𝒎 와 
      (조건2)분산𝜎² 정보를 알 때
      우리는 표본분포를 알수 있다. 

      표본분포의 평균은 모평균 𝒎과 동일하며 
      분산은 𝜎²/𝒏(표본수) 로 구할수 있다. 
      
      이때 표준화를 하면, 𝒁 = (𝑿 bar -𝒎) /𝜎²/𝒏(표본수)이며 ~𝑵[0,1]
      신뢰구간은 𝑿 bar ± 𝒁 𝛼/₂(𝜎/√𝒏)
      ```
 <br><br>

### 가설검정의 원리
표본으로부터 주어지는 정보를 이용하여, 모수에대한 예상, 주장 또는 추측 등의 옳고 그름을 판정하는 과정.
* 가설 : '모수' 에 대한 예상, 주장 또는 추측
   - 귀무가설 (𝙃₀) : 지금까지 사실로 알려져 있는 가설
   - 대립가설 (𝙃₁) : 표본자료로 부터 강력한 증거에 의해 입증하고자 하는 가설 <br>
    (결론은 귀무가설을 기각 또는 귀무가설을 기각하지 못함으로 표현됨) <br>
1. 가설유형
   관심모수가 𝑚 (eg.과자평균중량)이고, 검정하고자 하는 모수의 경계값이 𝑚₀(eg. 10g)일때,
   |단측(왼꼬리)검정|단측 (오른꼬리)검정 | 양측(양쪽꼬리)검정
   |:---:|:---:|:---:|
   |𝙃₀: 𝑚 = 𝑚₀,  𝙃₁ : 𝑚 < 𝑚₀ | 𝙃₀: 𝑚 = 𝑚₀, 𝙃₁ : 𝑚 > 𝑚₀ | 𝙃₀: 𝑚 = 𝑚₀, 𝙃₁ : 𝑚 ≠ 𝑚₀

      ```등호는 항상 귀무가설쪽에 있어야한다. ```
2. 검정통계량
   - 귀무가설과 대립가설 중 어느 하나를 택하는 기준을 결정하는 통계량
   - 통계량은 모수를 추정하는데 사용되면 '추정량', 모수를 검정하는데 사용되면, '검정통계량'이라고 불린다.
   - 모집단이 모분산이 알려진 정규분포인 경우, 모평균 𝑚관한 검정의 경우,
     * 검정 통계량 : 표본평균 𝑿 bar 의 함수인  𝒁 = (𝑿 bar -𝒎) /𝜎²/𝒏(표본수)
     * 검정 통계량의 표본분포 :   𝒁 = (𝑿 bar -𝒎) /𝜎²/𝒏 ~𝑵[0,1]
     * 귀무가설 𝙃₀: 𝑚 = 𝑚₀이 사실일때, 𝒁 = (𝑿 bar -𝒎₀) /𝜎²/𝒏 ~𝑵[0,1]
3. 귀무가설의 기각여부를 판단하기 위한 2가지 접근방식   
   ``` 두가지 방식은 동일한 결론을 가짐 ```
   - 기각역에 의한 검정 ('값'을 이용)
   - 유의확률에 의한 검정 ('확률'을 이용 , p-value)
      -  귀무가설이 사실인 경우 검정통계량의 분포에서, 대립가설의 방향으로 검정통계량의 관찰값보다 더 극단적인 값이 나올 확률로 계산됨.
4. 의사결정의 오류 <br>

   | |𝙃₀ 사실 |𝙃₁ 사실|
   |---|---|---|
   |𝙃₀ 기각못함|올바른 의사결정|제2종 오류 (확률:𝛽)|
   |𝙃₀ 기각|제1종 오류 (확률:𝛼) |올바른 의사결정

   𝛼와 𝛽는 상충관계로 동시에 줄이기 어려움. <br>
   더 위험한 제1종 오류를 일정수준을 넘지 못하도록 제한하면서, <br>
   제2종 오류를 최소로 하는 검정법을 찾도록 함. <br>
  * 유의수준 : 제1종오류를 범할 확률의 최대 허용 한계
    - 자료로부터 계산된 유의확률 (p-value)이 주어진 유의수준 𝛼 보다 작은경우에 귀무가설을 기각함, 결국 p-value는 제1종오류가 발생될 확률이며, 그 확률이 유의수준을 넘지 않을때 기각함.
  
5. 결론 <br>
    검정통계량 𝒁 = (𝑿 bar -𝒎) / (𝜎²/𝒏) 식을 통하여,
    𝒁₀ 경계값을 구한다. 이 𝒁₀ 경계값 보다 작을 확률 (왼꼬리) 또는 클 확률을 (오른꼬리) p-value 또는 유의확률 이라고 부른다. p-value값은 작으면 작을수록, 대립가설을 지지하며, 값이 유의수준 𝛼 를 넘기지 않는다면 귀무가설을 기각 할 수 있다. 
<br><br>
