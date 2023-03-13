# ML
> Machine Learning 심화학습

<br>

### 리눅스 명령어
```python
!ls - l  #해당위치에서의 디렉토리 확인
!lscpu #할당된 CPU 확인
!nvidia-sml #할당된 GPU정보 확인
```

## Data Analytics and Visualization
### 1. Data Type and Operations

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

### 2. Data Structure
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

### 3. Function and Module

<b>0. Computer Architecture </b>
  - CPU  (연산담당): 프로세서 안에 여러개의 CPU 존재
  - CPU는 메모리 (RAM) 에만 접근가능 <br>
  - DISK에는 직접 접근이 불가
  - 기본적으로 프로그램 (파이썬 등) 은 디스크에 저장되어 있다가 (이 상태에서는 'program' 이라고 부른다.) 실행을 (execute) 시켜서 메모리에 올려 사용하고, 이 상태를 'process'라고 부른다. 
  - OS도 마찬가지로 기본적으로 SSD(디스크)에 저장되어 있지만, memory에 올려 사용되고 이 작업을 '부팅'이라고 한다.
  <br>

<b>1. Function, Module and Package</b>
   

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


하나의 함수를 여러가지 방식으로 활용하려면 클래스





[참고] <br>
[통계교육원 통계 학습 사이트](https://sti.kostat.go.kr/coresti/site/main.do)
