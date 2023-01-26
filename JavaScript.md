# Java Script
> ECMAScript(ES)

<br>

### *모든 로직은 입력 / 로직 / 출력으로 나뉜다!*

<br>

### 이벤트

### 타입 / 변수 / 함수

1. 타입 : undefined (선언만 되어있는 상태), string, number(int, float를 대체), boolean, object, function <br>
2. 변수 : JS가 점차 프로그래밍 기능을 갖추면서 변수 사용에 제약조건을 기능을 준 변수가 let, const이다. (기존 var만 존재) <br>
지역변수 (스코핑) 등의 기능을 활용하기 위해선 let 사용을 해야한다.
   - var : 재선언, 재할당 가능 
   - let : 재선언 불가, 재할당 가능 
   - const : 재선언, 재할당 모두 불가) <br>
  
1. 함수 : 셀렉터 하나에 다수개 함수 작성 가능



### scorping

### hoisting

### operator

### 제어문
- for문과 다르게 중첩 while에서 내부 반복구문 (j)을  
1로 다시 초기화 해주는 단계가 중요하다!

- 결과값을 짝수에 해당 되는 숫자만 산출하기 위해서는
  증감연산자에서 ++i 대신 i = i+2 를 해주면 된다. 


### BOM
window 객체의 대화형 메소드
  - alert() : 경고, 코드 디버깅 (return값 미존재)
    <button on click ="alertFunc()">확인</button>
  - confirm() : 확인/취소 (return값 존재 : true/false)
    <button on click ="confirmFunc()">확인</button>
  - prompt() : 텍스트 박스, 확인/취소버튼 (return값 존재 : 텍스트/null)
    <button on click ="promptFunc()">확인</button> <br>
    
### 함수
- closure : 외부함수의 값을 내부함수에 저장하고 있음
- class : 클래스도 함수와 동일한 function으로 정의됨
         객체에서 속성을 사용하려면
         클래스에서 this.속성명 으로 선언 되어야한다.<br>
         그렇지 않고 (var,let) 단순 변수로 선언되었다면,
         변수를 return 하는 함수를 밑에 함께 작성해 줘서,<br>
         호출시 this.와 함께 함수를 불러 와야 한다.      
         =>this.함수명 = function(){return 변수명;}<br>
         (this. 대신 클래스 객체 명을 적어줘도 된다.
         this.는 파이썬에서 self와 같은 역할을 한다.)


### DOM

### Object
        //파이썬에서의 객체는 클래스(설계도)를 가지고 메모리에 실제 만들어놓은 것
        //Javascript ES6에서 클래스가 추가되었음
        //변수와 속성 값 구분, 메소드 기능 확인
       - property : 속성
         - function(method) : 기능
         - this : 객체 내부의 메서드나 속성을 정의 
         <!-- java, python등 모든 언어에서 동일한 의미로 사용 -->
         - new : new를 통해 객체를 생성
    </pre>
