# ML
> Machine Learning 심화학습

<br>

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
