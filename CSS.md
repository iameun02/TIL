## CSS
> Cascading Style Sheet

- 기능
    1. 선택자
    2. 스타일  
   [참고사이트](https://www.w3schools.com) 
- 스타일
  1. 브라우저 기본 스타일
  2. 사용자 스타일
      * 인라인 스타일 : 스타일을 적용할 대상에 직접 표시
      * 내부 스타일시트 : 웹 문서 안에서 사용할 스타일을 같은 문서 안에 정리
      * 외부 스타일시트 : 웹문서에 사용한 스타일을 별도 파일로 저장해놓고 필요시마다 사용
- 그 외 (태그)
  1. class는 여러 요소를 띄어쓰기를 통해 동시 적용 가능 / id 태그는 한번에 하나씩만 사용 가능
  2. 자식 태그는 바로 밑 자식 까지 지정 (> 이용)
  3. div 태그 : 해당 줄 전체 영역 / span 태그 : 해당 글자 영역
- 참고 <br>
  [구글폰트 사이트](https://fonts.google.com/)
<br><br>

#### <b>실습코드</b>

![실습결과물](./1%EC%9B%94%EB%8B%AC%EB%A0%A5.png){:width="50" height ="100"}

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