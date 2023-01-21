# CSS
> Cascading Style Sheet

<br><br>
- 기능
    - 선택자
    - 스타일   [  (참고사이트)](https://www.w3schools.com) 

<br/>

- 스타일
  - 브라우저 기본 스타일
  - 사용자 스타일
      * 인라인 스타일 : 스타일을 적용할 대상에 직접 표시
      * 내부 스타일시트 : 웹 문서 안에서 사용할 스타일을 같은 문서 안에 정리
      * 외부 스타일시트 : 웹문서에 사용한 스타일을 별도 파일로 저장해놓고 필요시마다 사용
  <br/>
- 그 외 (태그)
  - class는 여러 요소를 띄어쓰기를 통해 동시 적용 가능 / id 태그는 한번에 하나씩만 사용 가능
  - 자식 태그는 바로 밑 자식 까지 지정 (> 이용)
  - div 태그 : 해당 줄 전체 영역 / span 태그 : 해당 글자 영역
  - span이나 list는 인라인 태그기 때문에 기본적으로 너비나 높이를 지정 불가능
     * display:block; 스타일을 작성하여 사용

  - Float 사용시 tip
    * Float :오른쪽 정렬시 정렬이 거꾸로 되는 경우 해결방법 
             Ul {float:right}
             Li {float:left}
    * Float은 문서의 흐름과 별개로 작동하기 때문에 "Footer"가 딸려올라오며 뒤로 겹치는 경우 해결방법
      (Clear속성을 사용해서 Float속성에서 제외 시켜줘야함)
      Footer{ Clear : left
 	  Float : left}
  - radius 사용시 브라우저마다 조금 다르게 표현될 수 있기때문에 아래와 같이 사용
```css
        webkit-border-radius : 50px 50px 50px 50px;
        moz-border-radius : 50px 50px 50px 50px;
        ms-border-radius : 50px 50px 50px 50px;
        o-border-radius : 50px 50px 50px 50px;
       
        /*webkit : 구글 사파리
        moz : 파이어폭스
        ms : Edge, IE
        o : 오페라*/

```
<br/>
- 참고 <br>
  [구글폰트 사이트](https://fonts.google.com/)
<br><br>

#### <b>실습코드</b>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto+Condensed&display=swap" rel="stylesheet">
    <style>
        *{margin : 3px;}
        body{
            background-color:white;
        }
        th{
            border: none;
            font-size: 30px;
            font-family: "Roboto Condensed"; 
        }
        h1{ text-align:center;
            font-style:italic;
            font-weight: bold;
            font-size :105px;
            line-height : 170%;
            font-family: "Roboto Condensed";  }

        a:link{color:cornflowerblue;
        font-size:20pt}
        a:visited{color:slategray;
        }
        div{
            border: 3px solid black;
            background-color: rgb(217, 231, 236);
            width : 800px;
            padding: 30px;
        }
        nav{
            text-align: right;
            font-size : 30px;
            font-family: "Roboto Condensed"; 
            color :darksalmon
        }
        a{
            text-decoration: none;
        }
        td,tr{
            border : 1px solid black ;
            width : 110px;
            height: 120px;
            text-align: center;
            font-family: "Roboto Condensed"; 
            font-size: 20px;
        }
        #jan{
            font-size: 35px;
            text-decoration: underline;
            color :steelblue;
            font-family: "Roboto Condensed"; 
        }
        
    </style>
</head>
<body>
<div>

    <h1> 2023 CALENDER</h1>
    <nav>
        <span ><a href=""id ="jan">1월</a></span>
        <span><a href="">2월</a></span>
        <span><a href="">3월</a></span>
        <span><a href="">4월</a></span>
        <span><a href="">5월</a></span>
        <span><a href="">6월</a></span>
        <span><a href="">7월</a></span>
        <span><a href="">8월</a></span>
        <span><a href="">9월</a></span>
        <span><a href="">10월</a></span>
        <span><a href="">11월</a></span>
    </nav>
    <br><br><br><br>
    <table>
        <tr>
            <th style="color: firebrick;">SUN</th>
            <th>MON</th>
            <th>TUE</th>
            <th>WED</th>
            <th>THU</th>
            <th>FRI</th>
            <th>SAT</th>
        </tr>
        <tr>
            <td style="color: firebrick;" >1일</td>
            <td>2일</td>
            <td>3일</td>
            <td>4일</td>
            <td>5일</td>
            <td>6일</td>
            <td>7일</td>
        </tr>
        <tr>
            <td style="color: firebrick;">8일</td>
            <td>9일</td>
            <td>11일</td>
            <td>12일</td>
            <td>13일</td>
            <td>14일</td>
            <td>15일</td>
        </tr>
        <tr>
            <td style="color: firebrick;">16일</td>
            <td>17일</td>
            <td>18일</td>
            <td>19일</td>
            <td>20일</td>
            <td>21일</td>
            <td>22일</td>
        </tr>
        <tr>
            <td style="color: firebrick;">23일</td>
            <td>24일</td>
            <td>25일</td>
            <td>26일</td>
            <td>27일</td>
            <td>28일</td>
            <td>29일</td>
        </tr>
        <tr>
            <td style="color: firebrick;">30일</td>
            <td>31일</td>
            <td style="color:slategray; font-style: italic;">1일</td>
            <td style="color:slategray; font-style: italic;">2일</td>
            <td style="color:slategray; font-style: italic;">3일</td>
            <td style="color:slategray; font-style: italic;">4일</td>
            <td style="color:slategray; font-style: italic;">5일</td>
        </tr>
    </table>
</div>
</body>
</html>
```