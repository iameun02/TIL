## HTML

 
<br>

#### <b>정의</b>
클라이언트가 서버에 http에 맞추어 요청했을때 서버가 문서를 구조화 하여 응답하며, 이때 문서를 구조화 할때 사용하는 HTML언어.
HTML에서 데이터를 구조화 시키기 위해 태그와 텍스트를 이용한다.
<br>

#### <b>역할</b>  
> w3schools 사이트 참고!
   - 기능적 역할 : form, input, a, iframe, select, img...
     * 가장 중요한 개념 : form, action, method, submit, name

 -  데이터 구조화, 구분자 역할 : layout div, span, section, header 
<br>

#### <b>구성</b>
 -   태그 안 속성
 -   태그와 태그 사이의 텍스트 
 -   태그 안 태그
<br>

#### <b> 그 외 </b>
- Name은 Python에서 Key:value의 키값과 비슷한 개념의 역할을 한다.
- ID 는 #으로 
- Form Method 중 Get 방식은 헤더로 전달하게 되어있고
헤더는 사이즈가 제한 되어 있기 때문에 (255)
용량이 큰 메모 타입 등을 보내는데 한계가 있다.
- Muliple Select 는 Ctrl 누르고 선택시 중복 선택이 가능하다.
- id / class / name 의 차이점
  |id|class|name|
  |:---:|:---:|:---:|
  |하나의 요소만 가능|여러 요소에 적용가능|여러요소에 적용가능|
  |CSS 식별자로 사용가능(#id)|CSS에서 식별자로 사용가능(.클래스명)|CSS에서 사용불가
  
<br><br>
#### <b>실습코드</b>
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name = "author" content ="Ko">
    <title>HTML REVIEW</title>
    <style>
        table,
        th,
        td {
            border: 1px solid black;
        }

        fieldset {
            width: 500px;
        }

        fieldset legend {
            font-weight: bold;
        }

        li {
            list-style: none;
            margin: 10px;
        }

        label {
            width: 80px;
            float: left;
        }

        div {
            width: 500px;
            text-align: center;
            margin-top: 10px;
        }
    </style>
</head>
<body>
        <h1> 1. 텍스트 및 이미지 삽입 실습 </h1>
        <img src="/image/작두콩차.jpeg" alt="작두콩차">
        <h2> 작두콩 차의 효능 </h2>
        <p><h3>호흡기 건강 지킴이</h3>작두콩 차의 대표적인 효능은 기관지 질환을 치료/예방하는 것입니다.</p>
        <p> <h3> 신장 건강 지킴이</h3>작두콩차는 몸에 쌓이는 노폐물을 배출하고 염증을 감소시켜 신장을 건강하게 만들어 줍니다. <blockquote><em>
        꾸준히 마시면 신장의 기능을 강화시켜 주기때문에 <br> 신장염, 신부전 등을 앓고 있는 환자에게 특히나 좋다고 합니다.</em></blockquote></p>    
        <p> <h3> 눈 질환 예방 </h3>또한 비타민 A와 B가 풍부하게 들어가 있어 눈 건강은 물론,<br> 
        안구건조증을 예방하는 데도 탁월합니다.</p> 
       
    <br><br>
        <h1> 2. 표 실습 </h1>
       
        <caption>선물용과 가정용 상품구성</caption>
        <table>
        <tr>
            <th style = "background-color: cadetblue;">용도</th>
            <th>중량</th>
            <th>개수</th>
            <th>가격</th>
        </tr>
        <tr>
            <td rowspan="2" style = "background-color: cadetblue;">선물용</td>
            <td>3kg</td>
            <td>11~16과</td>
            <td>35,000원</td>
        </tr>
        <tr>
            <!-- <td>선물용</td> -->
            <td>5kg</td>
            <td>18~26과</td>
            <td>52,000원</td>
        <tr>
            <td rowspan="2"  style = "background-color: cadetblue;">가정용</td>
            <td >3kg</td>
            <td>11~16과</td>
            <td>30,000원</td>
        </tr>
        <tr>
            <!-- <td>가정용</td> -->
            <td>5kg</td>
            <td>18~26과</td>
            <td>47,000원</td>
        </tr>
        </table>

    <br><br>
        <h1> 3. 링크 실습 </h1>
        <a href="https://github.com/iameun02/">Github 구경가기 ! :) </a>

        <h1> 4. 폼 실습 </h1>
        
        <form action="https://www.google.com/search" method ="get">
        <span><strong>검색어</strong></span> 
        <input type="text" name ="q">
        <input type="submit" value ="검색">
    <br><br><br>   
        </form>
        <form action="html10-formsres.html" method ="get"></form>
        <fieldset>
            <legend>로그인</legend>
            
            <label for="uid">아이디</label> 
            <input type="text" id = "uid" name ="uid" autocomplete="on"><br>
            <label for ="upw">비밀번호</label>
            <input type="password" id ="upw" name ="upw">
            <br><br>
        
            <input type="submit" value ="로그인">
            <input type="reset" value ="취소">
        </fieldset>
        </form>
    <br><br>
        <form action="html10-formsres.html" method ="get"></form>
        <fieldset>   <!-- 폼 안에서 섹션 나누기 -->
          <legend>배송정보</legend>  <!-- fieldset의 타이틀 -->
     
        <ul>
            <li>
                <label for="prod">주문상품</label>
                <input type="text" id="prod" name ="prod" value ="상품용 3kg">
            </li>
            <li>
                <label for="prod">이름</label>
                <input type="text" id="uname" name ="username">
            </li>
            <li>
                <label for="prod">연락처</label>
                <input type="text" id="phone" name ="phone" placeholder="하이픈 없이 입력하세요">
            </li>
            <li>
                <label for="d_day">배송정보</li></label>
                <input type="date" id="d_day" name ="d_day">
                <small>(주문일로 부터 최소 3일 이후)</small>
            </li>
            <li>
                <label for="memo">메모</li></label>
                <textarea  id="memo" name ="memo" rows ="10" cols ="40"></textarea>
            </li>
        </ul>
     </fieldset>      
     <div>
        <input type="submit" value ="주문">
        <input type="reset" value ="취소">
     </div>
    </form>

</body>
</html>
```