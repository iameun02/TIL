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
<br><br><br>

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
  
##7. 모델만들기 <br>
  (1) Setting : 
     - (dbtest app) Installed_Apps 에 'dbtest' 추가작성 <br>
 
  (2) 프로젝트 생성 : django-admin startproject  dbtest <br>
  (3) model.py 파일 생성(앱 생성시 뷰와 동일하게 자동생성) <br>
      - Myboard 클래스 생성 (table) + myname, mytitle, my content, mydate라는 컬럼 생성 <br>


```python
  class Myboard(models.Model):
      myname = models.CharField(max_length= 100) 
      mytitle = models.CharField(max_length=500)
      mycontent = models.CharField(max_length=2000)
      mydate = models.DateTimeField()

 * admin 페이지에서 저장될 파일명 지정하는 방법
      def __str__(self):
        return str({'mytitle' : self.mytitle})
                      컬럼명        객체.컬럼값		 
  ```		

  (4) cd dbtest (manage.py 있는 dbtest app 위치로 이동) <br>
  (5) migration 파일 생성해줌 (쿼리생성단계) <br>
     python manage.py makemigrations dbtest <br>
    -> PK가 없을시에 장고에서 알아서 id 컬럼을 생성해서 PK를 부여한다. <br>
  (6) python manage.py migrate (sqlite 등 db에 실제 테이블 생성) <br>
  (7) admin 으로 확인하기 <br>
     (1) detest app내에 admin.py 작성 <br>
     (2) admin.py 에 작성 <br>
    
  ```python
      from django.contrib import admin  
      from .models import Myboard 
      admin.site.register(Myboard) 
       #Myboard Table을 볼수 있음(해당 코드 없어도 접속은 가능)
  ```
  <br>
     (3) admin 계정 생성 <br>
         python manage.py createsuperuser
  <br>
     (4) python manage.py runserver 
  <br>


  6-1 ) ORM 사용을 위해 DB 연결_ client tool (dbeaver연결) <br>
    (1)  terminal 창에 설치 명령어 입력 <br>
            pip install mysqlclient <br>
   
  (2) detest 내 settings.py 에서 DB 작성 
  <br>
```python
       DATABASES = { 
      	    'default': {
        	 'ENGINE': 'django.db.backends.mysql',
       		 'NAME' : 'employees',    #디비명
        	 'USER' : 'root',         
     		 'PASSWORD' : '1234',
       		 'PORT' : '3306',
       		 'HOST' : 'localhost',
 	 		}
		      } 
``` 

   6-2 ) migrations 하위 폴더내 파일들 모두 삭제 후 다시 실행
```python
     python manage.py makemigrations dbtest
     python manage.py migrate
```

  * (Migration) 'DIRS': [], 는
      -> detest/dbtest.templates를 뜻한다. (그대로진행)

   * 참고 : [BASE_DIR/'templates'] : dbtest/templates를 뜻함



<br><br><br>

### Django Model API에서 기본적으로 제공하는  주요 메서드 

1. 클래스명.objects.all() : 테이블 데이터 전부 가져오기<br>

2. 클래스명.objects.get() : 하나의 Row만 가져오기 <br>
   - 클래스명.objects.get(pk=1) : Primary Key가 1인 row를 가져오기 <br>

3. 클래스명.objects.filter() : 특정 조건에 맞는 row들을 가져오기 <br>
   - 클래스명.objects.filter(name='Lee')<br>

4. 클래스명.objects.exclude() : 특정 조건을 제외한 나머지 row들을 가져오기 <br>
   - 클래스명.objects.exclude(name='Lee')<br>

5. 클래스명.objects.count() : 데이터 row 수 세기<br>

6. 클래스명.objects.order_by() : 키에 따라 데이터 정렬<br>
   - 클래스명.objects.order_by('id', '-name') #id 오름차순 name내림차순<br>

7. 클래스명.objects.distinct() : 중복된 값은 하나로만 표시<br>
   - 클래스명.objects.distinct('name')<br>

8. 클래스명.objects.first() : 데이터 중 첫번째 row만을 리턴한다. <br>
   - 클래스명.objects.order_by('name').first() <br>
9. 클래스명.objects.last() : 데이터 중 마지막에 있는 row만을 리턴한다. <br>
   - 클래스명.objects.order_by('name').last()<br>


10. UPDATE<br>
a = 클래스명.objects.get(pk=1)<br>
a.name = 'Kim'<br>
a.save()<br>

11.  DELETE<br>
b = 클래스명.objects.get(pk=1)<br>
b.delete()<br>

<br><br><br>

### STATIC 
> css,js 문서를 저장하는 곳

##0. Setting 에 작성 <br>
```STATICFILES_DIRS = [BASE_DIR/'static'] ```

##1. base_dir에 물리적인 static 폴더 생성 -> 하위에 css 폴더 / js폴더 생성 -> 각각 파일을 하나씩 생성 후 저장 <br>

##2. 프로세스 cycle 진행 (화면에서 확인할 버튼 만들기)
<br>
##3. template 문서 내 head영역 내 아래 작성 <br>
``` 
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
<script src ="{% static 'js/test.js' %}" ></script>
```
<br><br><br>

### Django Model Form

1. Form vs Model Form (폼과 모델폼의 차이점) <br>
Form (일반 폼) : 직접 필드 정의, 위젯 설정이 필요 <br>
Model Form (모델 폼) : 모델과 필드를 지정하면 모델폼이 자동으로 폼 필드를 생성 <br>

2. request.POST.get('content')는 POST로 전송된 폼(form) 데이터 항목 중 content 값을 의미한다. <br>
3.  폼태그 사용시 암호화를 위해 무조건 인풋 태그 위에 {%csrf_token%} 함께 작성 <br>
   
4. form tag 의 action 속성에는 urls.py 중 request(url)을 지정해주고 , method 를 통해 'get', 'post'  방식을 정해준다. <br>
 
5. CRUD

1) Create <br>
   
   ```result = Myboard.objects.create(myname=myname, mytitle=mytitle,mycontent=mycontent, mydate =timezone.now())```

3) Update <br> ```myboard = Myboard.objects.filter(id=id)
    result_title = myboard.update(mytitle = mytitle)
    result_content = myboard.update(mycontent = mycontent)```
   
4) Delete <br>  
```result = Myboard.objects.filter(id=id).delete()```