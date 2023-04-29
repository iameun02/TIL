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
  
3. 함수 : 셀렉터 하나에 다수개 함수 작성 가능
함수를 인라인으로 작성할때는 javascript : 함수명()

:bulb: 중요! <br>
- null : 값이 없음 <br>
- '' : 공백의 값이 있음 <br>
- undefined : 선언만 됨 <br>
- Nan : 오류아님, 숫자가 아님 <br>


### scorping
<pre>지역변수 scorping
지역변수 사용은 let을 활용 (var지양)
let 지역변수는 블록 "{}" 내 선언하여 사용함
이것을 블록{} scorping이라고 함 </pre>


### hoisting
<pre>변수의 메모리 공간을 선언 전에 미리 할당하는 것
변수의 선언과 초기화를 분리 한후, 선언만 코드의 최상단으로 옮기는 것
let과 const는 호이스팅 대상이지만, undefied로 변수를 초기화 하지않음
따라서 변수의 초기화를 수행하기 전에 읽는 코드가 먼저 나타나면 에외가 발생함</pre>



### operator

### 제어문
  1) if문
     if(조건식){if 조건식 true시 수행문} else if(조건식){else if 조건식 true시 수행문}
     else{그외 수행식}

  2) switch-case문
     switch(입력값을 담은 변수명){case '입력값1' : 수행문 break
			     case '입력값2' : 수행문 break
			     default : 수행문 break}

  3) for문
     for(let 초기값 ; 조건식 ; 증감식){반복할 명령문}

  4) while문
     i 변수 선언
     while(조건식){수행문 증감식}
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

### string
```javascript
 console.log("indexOf:" +str.indexOf(inputName)) //첫번째 검색되는 문자열의 첫번째 인덱스
 console.log("lastIndexOf:" +str.lastIndexOf(inputName)) / 마지막으로 검색되는 문자열의 첫번째 인덱스
 ```
### sort
```javascript
  let arr = [1,5,66,3,22,8,5]
      arr.sort(compareNum) //숫자는 문자열 기준으로 정렬되기때문에 compareNum 함수 활용

  function compareNum(a,b){
      return a-b
```

### array
push()
shift() 인덱스가 0인값을 가져옴
pop() : 마지막 입력값
shift(queue) 콜센터 대기시간, 프린터 출력, 예약작업
pop(stack) :: 페이지 뒤로가기 ,ctrl_z

### 그 외 
- 객체.style.margin : 10px (상하) 5px (좌우); 
- InnerHTML (tag를 html기능처럼사용) / textContent
- Onload 펑션은  본문내용을 다 읽어들인다음 시행
document를 읽어오기 전에 선언을 하면 오류발생을 해서 load 완료 후 작성하는 영역
