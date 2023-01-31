# Django
> Python을 활용한 Web Framework

<br>

### Django Process

##0. Setting 설정 <br>
  (1) DIR 작성 : Template 사용시 호출될 기본경로 설정 <br>
     'DIRS': [BASE_DIR(=프로젝트명)/'templates'] <br>
      #기본적으로는 [BASE_DIR(=프로젝트명)/앱명/'templates']으로 설정되어있다.

##1. 프로젝트 만들기 <br>
  (1) 프로젝트 생성 : django-admin startproject mysite(프로젝트명) <br>
       - 프로젝트명 아래로 여러개의 앱 (단위단위 서비스)들이 생기는 구조 <br>
       - 주의!   프로젝트 생성시 무조건 최상위 root 디렉토리로(project단을 지칭) 이동 후 생성! 
<br>
  (2) 프로젝트로 이동 : cd mysite<br>
  (3) 장고 서버 시작 : python manage.py runserver
      http://127.0.0.1:8000/  : 8000번포트를 사용하는 장고에서 제공하는 웹페이지
<br><br>
##2. (프로젝트단) urls.py 작성<br>
  (1) From . import view (현재 디렉토리에서 view 접근)<br>
  (2) urlpatterns 작성<br>
       - path('test/',views.test) : test로 들어온건 view 파일의 test함수로 보내라 <br>
       - path('',views.index) : 공백 즉, 첫 화면에 접근시 view 파일 index함수로 보내라

  (3) include <br>
     ① import : from django.urls import path, include
     ② url patterns 작성<br>
     [예시] <br>
      - path('hello01/',include('hello01.urls'))
      - https://127.0.0.1/hello01/로 시작하는 모든 하위폴더를 포함하여 처리
      - https://127.0.0.1/hello01/blog 등..
 
##3. (프로젝트단) views.py 작성<br>

  ✓ HttpResponse / render<br>
    Render는 HttpResponse 객체를 반환하는 함수로, <br>
    template을 context와 엮어서 HttpResponse객체로 쉽게 반환해 주는 함수
<br><br>
    render(request(필수), template_name(필수), 
    context=None, content_type=None, status=None, using=None)
<br><br>
   ✓ TIP<br>
     ```HttpResponse("<h1><a href='/'> Hello, World : )!</a></h1>")<br>
     '/' 는 index 첫 화면을 다시 호출해 주는 역할 = path 에서 '' 임
     ```
<br><br>

  (1)<br>

    def index(request):
    return render(request,'프로젝트명/index.html',{'name':'Lee'})   

<br>

> BASE_DIR + 프로젝트명/index.html 
   프로젝트명의 폴더를 하나 만들고 그 안에 html을 만드는 이유는
   안 만들어도 동작은 되지만, 
   해당 탬플릿이 어느 app에서 사용되는 것인지 직관적으로 이해하기 위함
 
<br><br>
##4. Template 만들기 <br>
    앱 level과 동일한 레벨에서 templates 디렉토리 생성후 > <br>프로젝트명으로 된 폴더 생성후 > html 문서 작성
 
[예시]
```
	<body>
	    <h1>hello, {{name}}</h1>
	</body>
```

##5. 확인 <br>
  (1) manage.py가 위치하는 경로로 이동 : cd 프로젝트명 <br>
  (2) python manage.py runserver <br>
   -> http://127.0.0.1:8000/test/ 로 확인 가능  <br>
  (3) ctrl+c : run server 종료 <br>
<br><br>

##(6). 앱 만들기 <br>
   (1) 앱 생성 : python manage.py startapp hello01(앱명) <br>
      - 앱에는 기본적으로 views.py 파일이 함께 생성된다 <br>