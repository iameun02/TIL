# Algorithm
> Python을 활용한 Web Framework

<br>

### Intro
1. 알고리즘 연습 url (for 코딩테스트) 

  + 사이트

     https://www.acmicpc.net/
     https://swexpertacademy.com/main/main.do
     https://programmers.co.kr/
  
  + 도서 Introduction to Alogorithm


2. Work Flow <br>
   ##1. 공유 Repository의 우측 code 버튼 클릭 후 http주소 복사 <br>
   ##2. (alt+f11) 터미널 : git clone 복사한주소붙여넣기 <br>
   ##3. 파이참 셋팅 (Tools- Terminal : bash) <br>
   ##4. <br>
       ❶ git pull origin master 업데이트된 문제파일 받아오기 <br>
       ❷ git switch -c 브랜치명 <br>
         (혹시 브랜치 수정이 필요한 경우, 삭제후 재생성 <br>
	   git switch master <br>
	   git branch -D 잘못된브랜치명 <br>
       확인을 위해 git branch <br>
        ❸ 문제파일 우측파일 클릭 후 내 이름으로된 파일 생성 후 문제풀기 <br>
        
     *  프로그래머스 : 제공하는 기본 소스코드를 파이참에 복붙 후, <br>
 			 test를 위해 구현 함수를 호출하고, <br>
             호출시 화면에서 제공된 샘플 입출력 데이터를 파라미터로 넣어준다. <br>

    * 백준 :
             ``` import sys
		sys.stdin =open('input.txt') 
             	소스코드를 상단에 쓰면 계속해서 input을 안넣어줘도 된다. 
        	단 소스제출시 위 코드는 제거후 제출``` <br>

    ❹ 소스를 add + commit <br>
    ❺ (주의! 브랜치명으로 push) git push origin 브랜치명 <br>
    ❻ PR(Pull Request : 병합)



#3. 소스코드
``` python

1. a,b = ____.split()
2. List 중복 제거시 : (set) 
3. List comprehension
4. Enumerate (index를 함께 발생시켜줌)
5. 변수명은 boolean값이 리턴될경우 is__로 시작하며, 리스트와 튜플은 복수형으로 지어준다. 함수명은 동사형
   (파이참에서 shift+F6 을 누르면 변수명을 일괄변경 가능하다.)
6. For inx in range(N-1, -1, -1) : N개까지 끝에서부터 하나씩 차례로 읽어옴

```

