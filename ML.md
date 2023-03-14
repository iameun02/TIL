# ML
> Machine Learning 심화학습

<br>

#### 리눅스 명령어
```python
!ls - l  #해당위치에서의 디렉토리 확인
!lscpu #할당된 CPU 확인
!nvidia-sml #할당된 GPU정보 확인

!pip list  #설치된 패키지확인
!pip list | grep numpy # 설치된 패키지들 중 특정 패키지 확인

#[기존 코랩에 설치된 버젼을 변경해야하는 경우]
!pip remove
!pip install
```

## <b>Data Analytics and Visualization</b>
### <b>1. Data Type and Operations</b>

1. Data Type
 - NUMERIC
    -  복소수(허수) : 제곱해서 마이너스가 나오는 수 (√-1) <br>
       파이썬에서는 j로 표현
        ```python
        print(8 + 9j)
        print(type(8 + 9j))
        ```
    -  Exponential을 활용한  과학적 표기법
        ```python
        print(5e+4) #output: 5에 대하여 10의 1/4승 = 0.0005
        print(type(5e+4)) #output= 50000
        ```


2. Type and Operation (타입과 연산) <br>
- 데이터타입에 따라서 적용가능한 연산의 차이가 있어서 타입구분이 중요
  
    |파이썬|통계변수|적용가능연산|
    |:---:|:----------:|:---:|
    |문자|명목형| ==, !=
    |문자|순서형| >, <, >=, <=
    |숫자|이산형 (등간변수로, 0이 의미를 가지지 않음 ex.온도)|+,-
    |숫자|연속형 (비율변수로, 0아 의미를 가짐) ex. 속도, 무게, 돈) |+, -, *, /


    [결론] <br>
    통계분석에서는 통계변수별로 적용가능연산이 4가지로 나뉘지만, <br> ML분석(Python)에서는 2가지로만 연산을 알면된다. <br>
    문자 : 명목형 / 숫자 : 연속형

<br><br>

### <b>2. Data Structure</b>
Python의 기존함수만으로는 연산이 복잡해질 수 있는데, <br> Numpy 또는 Pandas 라이브러리를 통해 쉽게 연산 할 수 있다. <br>
예를들면, 두 리스트끼리 List + List 연산을 수행할 때 <br>
np.array 또는 pd.DataFrame를 활용하면
쉽게 Broadcasting 연산이 가능

```python
L1 = ['Red', 'Green', 'Blue']
L2 = [255, 127, 63]

for i in zip(L1, L2):
  print(i)

D2 = {x : y for x, y in zip(L1, L2)}
print(D2)
```
<br><br>

### <b>3. Function and Module</b>

0. Computer Architecture 
  - CPU  (연산담당): 프로세서 안에 여러개의 CPU 존재
  - CPU는 메모리 (RAM) 에만 접근가능 <br>
  - DISK에는 직접 접근이 불가
  - 기본적으로 프로그램 (파이썬 등) 은 디스크에 저장되어 있다가 (이 상태에서는 'program' 이라고 부른다.) 실행을 (execute) 시켜서 메모리에 올려 사용하고, 이 상태를 'process'라고 부른다. 
  - OS도 마찬가지로 기본적으로 SSD(디스크)에 저장되어 있지만, memory에 올려 사용되고 이 작업을 '부팅'이라고 한다.
  - 스토리지 (디스크 +SSD + 외장 등등)
  <br><br>

1. Function, Module and Package
   

 - Function : 파이썬 실행시 , 함께 메모리에 올라 와 있는 함수
    - 내장함수 :  파이썬이 실행될 때 기본적으로 함께 메모리에 올라와 있는 내용
    - 사용자 정의 함수 : def 명령어를 통해 메모리 특정공간에 바로 파이썬에 함수를 할당한 다음 cpu가 접근해서 연산 (디스크에 저장 X) <br>
  <br>
 -  Module : 파이썬이 실행되었지만, 메모리에 올라와 있지 않은 함수 
     - Module : 사용자 정의 함수를 포함하고 있는 파이썬 스크립트(*.py) 의 파일형태로 되어있다. 
     - Module을 메모리에 올려 사용하기 위해서는 import 한다.
       - import :   파이썬 스크립트에 정의된 함수를 메모리로 호출
     - 모듈 안에는 여러개의 함수가 있다. <br>
모든 함수를 한번에 다 가지고 오는 것 또한 메모리의 낭비가 되니, <br> 특정함 수만 메모리를 올리고 싶을 경우 <br>
```From 모듈명 import 함수명``` 으로 가져오면 된다.
     - 사용자 모듈 : 사용자 모듈은 디스크에 저장하고 필요시 메모리에 올려서 사용 <br>
  

        ```[Colab 에서 사용자 모듈 활용법]```
        - 코렙에서 사용자 모듈을 정의하고 사용하기 위해선,
        - 사용자 모듈 파일을 내 로컬에 저장하고,
        - 로컬에 저장된 모듈파일을 다시 Colab의 디스크 공간에 위치시켜 놓은 뒤에 (왼쪽에 파일모양 클릭후 파일을 해당 디렉토리에 드래그 하여 위치 시켜준다.)
        - Colab 디스크에 올라와 있는 모듈을 사용하기 위해선, import를 해줘야 실제 메모리에 올리게 된다.
        - Colab에의 위치 확인 (/content)
          - !pwd 
          - import sys <br> 
            sys.path

        - Colab에서의 '연결' 의미 : (Ram) 메모리에 파일구조를 올리겠다.





- Package : 모듈 파일들을 묶어서 디렉토리로 관리 <br>
   - install : 외부에 있는 프로그램 (패키지 : 넘파이, 판다스)을 내부 디스크에 넣는 행동_ !pip install <br><br>
   
- 함수 > 모듈 > 패키지


<br><br>
### <b>4. Class and Package</b>
- Class : 기본적으로 독립적 메모리 공간 지정하며, 함수와 변수를 하나의 객체로 관리한다. <br>
  
   |종류|내용|
   |---|---|
   |클래스 메서드|클래스 내에서 선언된 함수|
   |클래스 멤버 |클래스 내에서 선언된 변수|
   |인스턴스 멤버 | 클래스 내 함수에 선언된 변수|
   
   <br>
  

   - 기본적으로는 함수를 담을수도 있고 변수를 담을 수도 있다는 점에서 Module과 비슷
   - 하지만, 모듈은 디스크에 파일 시스템 구조의 형태로 저장되어 호출하여 사용되고, 클래스는 메모리공간에 올려 바로 생성 할수도 있다는  차이점이 있다. ```클래스는 모듈로 만들수도 있고, 패키지로 만들수도 있다.```
   - 클래스는 메모리에 direct로 선언 및 생성이 가능하지만, 직접적인 사용은 불가하다. 
   - 클래스를 사용하려면 Instance를 생성하여 사용하여야된다.
   - 	Class로 생성된 Object(객체) 자신을 참조하는 매개변수
self를 사용하여 Class Member에 접근 (self: 첫 번째 매개변수 self는 Class로 생성한 Instance 자체를 지정) <br>
   - <b>클래스의 장점</b>
  
      - 클래스 기반으로 새로운 메모리영역을 할당하고 독립적으로 기능을 가지고 다르게 동작시킬 수 있다 (오버라이딩) , <br> <br>하나의 클래스를 각각 인스턴스를 생성하여 여러개 동작 구현이 가능 (그렇지 않고는 함수를 각각 여러가지를 만들어야한다.) <br><br>

       -  상속 가능 : 클래스는 클래스를 상속받아 재사용 단위를 키워 나갈 수 있다. 


   - 예로 sklearn에서 모델로 사용되는 클래스 객체들은 바로 사용불가하여 인스턴스를 생성하여 모델링을 하고, 평가시 사용되는 metric는 클래스 객체가 아니기 때문에 바로 사용가능하다.

<br><br>
- Package : 관련된 모듈을 디렉토리 구조를 사용하여 계층적으로 관리 <br>

   - 디렉토리 이름 자체가 패키지 이름이 된다.
   - 디렉토리명.파일명(모듈명).함수명 
   - 디스크에 저장되는 것 (코랩에서 작업된 패캐지는 코랩디스크 에 저장됨) > 즉, import를 통해 메모리에 올려주는 과정 필요
   - From import구문으로 호출
   -  \_\_init\_\_.py 파일을 사용하여 해당 디렉토리가 Package에 사용됨을 알려줌
   -  패키지 설치는 pip를 통해 디스크에 올리고 > 그중 클래스사용시에는 인스턴스를 찍어내고
From import 로 특정 함수를 가져옴
   - import 또는 from ~ import 구문으로 호출하여 사용 
     - Package_Name.Module_Name
     - from Package_Name.Module_Name import Function_Name
  <br>

   - 코랩에서 Package 만들기
      * Colab에 디렉토리 생성
      * 'myPackage' 디렉토리 내에 생성
      * \_\_init\_\_.py에 version=1.0 작성 후 UTF-8 Encoding으로 저장
      * 파일(Module) 생성(UTF-8 Encoding)
      * myLibrary.py 내에 다양한 Fuction 및 Class 정의
      * myLibrary.py 파일을 'myPackage' 디렉토리로 이동



<br><br>
### <b>5. Numpy and Pandas</b>
1. Numpy
   1. 행렬 에서의 '차원' = 딥러닝에서 'Rank'
   2. 앞으로 array는 배열보다는 matrix (행렬)의 개념으로 이해하기
   3. Tensor : 다차원 행렬 (결국 array, matrix)
   4. Scalar (무게) = 0d array = Rank0 Tensor <br>
      Vector (무게 + 방향) = 1d array = Rank1 Tensor

2. Pandas



<br><br><br>

## <b>Data Preprocessing</b>
1. 결측치
   1. 확인
      - 막대그래프
       ```python
       !pip install missingno
       import missingno as msno
       msno.bar(df, figsize = (15,7), color = (0.2,0.2,0.8))
       ```
      - 매트릭스
       ```python
       msno.matrix(df, figsize = (15,7), color = (0.2, 0.2, 0.8))
      ```
  2. 삭제
     - 300개 이하 측정값(Non-Null)이 있는 ```열(Column)``` 삭제 <br> 
      ```.dropna(thresh = 300, axis = 1)```

      - 'age'행(Column) 기준으로 결측치가 있는 ```행(Row)``` 삭제 <br>
     ```.dropna(subset = ['age'], how = 'any', axis = 0)``` <br>
     how = 'all' : 모든 값이 결측치인 경우 삭제

2. groupby
  - groupby 객체 자체를 이용하기
      ```python
      grouped_TWO = TD.groupby(['class', 'sex'])
      grouped_TWO

      #get_group : 그룹필 된 그룹중 class = First, sex= female인 그룹의 데이터 조회
      grouped_TWO.get_group(('First', 'female')).head(3)

      #반복문을 통해 각 그룹핑 기준 키와 데이터 확인
      for key, group in grouped_TWO:
         print('* key :', key)
         print('* number :', len(group))
         print(group.head(3))
         print('\n')
            
      ```
  -  결과 filtering 하기
      ```python
      grouped.filter(lambda x : len(x) >= 200).head()
      ```


1. multi index
   
 - pv을 여러개의 index,column 으로  agg (집계)하면 Multi- index가 생성됨 (헤더가 다층) 
 - .xs( ): Cross Section을 이용하여 접근
[pv table 만들기]
   ```python
   #df는 타이타닉데이터
   PV = pd.pivot_table(df,
                        index = ['class', 'sex'],
                        columns = 'survived',
                        values = ['age','fare'],
                        aggfunc = {'age' : ['mean', 'std'], 'fare' : ['min', 'max']})

   ```
   [행 멀티인덱스]
   ```python
   PV.index 

   PV.xs('First', level = 'class', axis = 0) 
   PV.xs('male', level = 'sex', axis = 0)
   PV.xs(('First', 'male'), level = ['class', 'sex'], axis = 0)
   ```

   [열 멀티인덱스]
   ```python
   PV.columns 

   PV.xs(('fare', 'min'), level = ['Header', 'Fuction'], axis = 1)

   PV.xs(('age', 'mean', 'Dead'), level = ['Header', 'Fuction', 'Survived'], axis = 1)

   #헤더명칭 생성
   PV.columns.set_names(['Header', 'Fuction', 'Survived'], inplace = True)

   #특정 레벨로 접근하여 컬럼명 바꾸기 (Survived 0,1을변경)
   PV.columns.set_levels(['Dead', 'Alive'], level = 2, inplace = True)

   ```

<br><br><br>

[참고] <br>
[통계교육원 통계 학습 사이트](https://sti.kostat.go.kr/coresti/site/main.do)
