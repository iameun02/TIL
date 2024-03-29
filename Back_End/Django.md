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
     ① import : from django.urls import path, include <br>
     ② url patterns 작성<br>
     [예시] <br>
      - path('hello01/',include('hello01.urls')) <br>
      - https://127.0.0.1/hello01/로 시작하는 모든 하위폴더를 포함하여 처리 <br>
      - https://127.0.0.1/hello01/blog 등.. <br>
 
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

``` 
def index(request):
    return render(request,'프로젝트명/index.html',{'name':'Lee'})  
```
  BASE_DIR + 프로젝트명/index.html 
   프로젝트명의 폴더를 하나 만들고 그 안에 html을 만드는 이유는
   안 만들어도 동작은 되지만, 
   해당 탬플릿이 어느 app에서 사용되는 것인지 직관적으로 이해하기 위함
 
<br><br>
##4. Template 만들기 <br>
    앱 level과 동일한 레벨에서 templates 디렉토리 생성후 > <br>프로젝트명으로 된 폴더 생성후 > html 문서 작성
 
[예시]
```python
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
  (1) 프로젝트 생성 : django-admin startproject  dbtest <br>
  (2) Setting  <br>
     - (dbtest app) Installed_Apps 에 'dbtest' 추가작성 <br>
  (3) model.py 파일 생성(앱 생성시 뷰와 동일하게 자동생성) <br>
      - Myboard 클래스 생성 (table) + myname, mytitle, my content, mydate라는 컬럼 생성 <br>


```python
  from django.db import models
  class Myboard(models.Model): #models 상속받아 클래스 생성 , 클래스 생성시 상속파일들이 함께 생성됨
      myname = models.CharField(max_length= 100) 
      mytitle = models.CharField(max_length=500)
      mycontent = models.CharField(max_length=2000)
      mydate = models.DateTimeField()

 # admin 페이지에서 저장될 파일명 지정하는 방법 - 오버라이딩
 # object row 출력시 메모리 출력 대신 정의된 것을 출력하도록 작성
      def __str__(self):
        return str({'mytitle' : self.mytitle})
                      컬럼명        객체.컬럼값		 
  ```		

  (4) cd dbtest (manage.py 있는 dbtest app 위치로 이동) <br>
  (5) migration 파일 생성해줌 (쿼리생성단계) <br>
     python manage.py makemigrations dbtest <br>
    -> PK가 없을시에 장고에서 알아서 id 컬럼을 생성해서 PK를 부여한다. <br>
  (6) python manage.py migrate dbtest (sqlite 등 db에 실제 테이블 생성) <br>
   > (5),(6) 진행시에는 무조건 app명을 사용해서 특정 app만 마이그하는 것이 좋다.. <br>
   그렇지 않고 전체 migration 진행 후, 다음번의 migrate 진행시에 <br>
   기존에 만들어져 있는 것과 충돌하여 작업이 이미 되어있다고 인지하고 수행이 안된다. 그럼 초기화 등 추가작업필요

  (7) admin 으로 확인하기 <br>
   * detest app내에 admin.py 작성 <br>
   * admin.py 에 작성 <br>
    
  ```python
      from django.contrib import admin  
      from .models import Myboard 
      admin.site.register(Myboard) 
       #Myboard Table을 볼수 있음(해당 코드 없어도 접속은 가능)
       #여기서 Myboard는 models.py 파일에 만들어놓은 클래스를 호출하는 것이다.
  ```
  <br>

   * admin 계정 생성 <br>
      ```python manage.py createsuperuser```
  <br>
   * python manage.py runserver 
  <br> <br>


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

12. CREATE <br>
c = 클래스명.objects.create()
```python
        name = request.POST['name']
        pw = request.POST['pw']
        email = request.POST['email'] 

        result = Mymember.objects.create(myname = name, mypassword = pw, myemail = email)
```
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
 
5. CRUD <br>
 (참고 : ** Myboard속성 = new작성된값) <br>

   5-1) Create <br>

```python
    insert_proc(request):
    myname=request.POST['myname']
    mytitle=request.POST['mytitle']
    mycontent=request.POST['mycontent']

    result = Myboard.objects.create(myname=myname, mytitle=mytitle,mycontent=mycontent, mydate =timezone.now())


    print('===========')
    print(result)
    print('===========')

    if result:
        return redirect('index')
    else :
        return redirect('insertform')
```
<br>

   5-2) Update <br> 
```python    
   mycontent =request.POST['mycontent']
   id=request.POST['id']
   mytitle = request.POST['mytitle']

   myboard = Myboard.objects.filter(id=id)
   result_title = myboard.update(mytitle = mytitle)
   result_content = myboard.update(mycontent = mycontent)


   if result_title + result_content ==2:
        return redirect('/detail/'+id)
   else :
        return redirect('/updateform/'+id)
``` 
<br>
   
   5-3) Delete <br>  
``` python
    def delete_proc(request, id):
    result = Myboard.objects.filter(id=id).delete()

    if result[0]:
        return redirect('index')
    else:
        return redirect('/detail/' +id)
```  
<br><br><br>

### Paging
1. 페이지 작업 환경을 위해 데이터 만들어넣기 <br>
   (1) 터미널 명령어 <br>
    -  ```python manage.py shell ``` <br>
    
   (2) shell 내에서 작업 <br>
    ```python
    [1] from django.utils import timezone
    [2] from dbtest.models import Myboard #Myboard 클래스 객체를 가리킴
    [3]  for i in range(1,101):
         temp = Myboard(myname= i , mytitle= i, mycontent = i , mydate = timezone.now())
   
         temp.save()
    [4] quit 
    ```
<br>

2. views.py 작성
   ```python
   from django.core.paginator import Paginator
   
   def index(request):
    myboard_all = Myboard.objects.all() #.order_by('-id')
    
    paginator = Paginator(myboard_all,10)
    page_num = request.GET.get('page','1') #page값이 없으면 디폴트가 1이다.
    page_obj = paginator.get_page(page_num)

    #총게시물 수
    print('-------count------')
    print(page_obj.count)
    print('-------현재페이지번호------')
    print(page_obj.number)
    print('-------총페이지수------')
    print(page_obj.paginator.num_pages)
    print('-------총페이지 range 객체------')
    print(page_obj.paginator.page_range)

    print('-------다음페이지, 이전페이지------')
    print(page_obj.has_next())
    print(page_obj.has_previous())


    try:
        print('----다음페이지가 없으면 에러------')
        print(page_obj.next_page_number())

        print('----이젠페이지가 없으면 에러------')
        print(page_obj.previous_page_number())
    except:
        pass

    print('-------start_index---------')
    print(page_obj.start_index())

    print('------end_index--------')
    print(page_obj.end_index())


    return render(request, 'index.html',{'list' : page_obj})
   ```

   <br>
3. HTML 문서 body 내 작성 
   ```html
   <a href="?page=1">First page</a> 
         <!-- 처음페이지 :request의 get방식 쿼리스트링으로 page값을 넘김 -->

        {% if list.has_previous %}
            <a href="?page={{list.previous_page_number}}">◀︎</a> 
            <!-- 이전페이지 -->
             
        {% else %}
            <a>◀︎</a>
        {% endif %}
       

       

        {% for i in list.paginator.page_range %}
            {% if i >= list.number|add:-3 and i <= list.number|add:+3 %} 
            <!-- 아래위 +3page만 노출 -->

            {%if list.number == i %} 
            <!-- 현재페이지에 있으면 링크없애기 -->
                <span style="color:lightslategrey;">{{i}}</span>
            {% else %}  
                <a href="?page={{i}}">{{i}}</a>   
            {% endif %}

            {% endif %}
        {% endfor %}


        
        
        {% if list.has_next %}
         <a href="?page={{list.next_page_number}}">▶︎</a> 
         <!-- 다음페이지 -->                                       
        {% else %}
         <a>▶︎</a>
        {% endif %}
  
        
        <a href="?page={{list.paginator.num_pages}}">Last page</a> 
         <!-- 끝페이지 -->

   ```
<br><br><br>  

### login/ logout
1. 세션만들기
 ##1. views.py
      - register
      ```python
      def register(request):
      #obj =  Mymember.objects.all()
      if request.method == 'GET':
        return render(request, 'register.html')
      elif request.method =='POST':
        name = request.POST['name']
        pw = request.POST['pw']
        email = request.POST['email'] 

        result = Mymember.objects.create(myname = name, mypassword = pw, myemail = email)

      if result:
            return redirect('index')
      else:
            return redirect('register')
      ```
      - login
      ```python
      def login(request):
      if request.method == 'GET':
        return render(request, 'login.html')

      elif request.method =='POST':
        name= request.POST['name']
        pw= request.POST['pw']

        obj = Mymember.objects.get(myname=name)
        if pw == obj.mypassword:
            request.session['name'] = obj.myname
            return redirect('index')
        else:
            return redirect('login')
      ```
      - logout
      ```python
      def logout(request):
      del request.session['name'] 
      return redirect('index')
      ```
 ##2.  Templates
   
       ```python 
       #세션 유무에 따라 화면 뿌려주기
      {% if request.session.name %}
          <h3><input type="button" value ="로그아웃" onclick ="logouthref()"></h3>
      {% else %}
          <h3><input type="button" value ="로그인" onclick ="loginhref()"></h3>
          <h3><input type="button" value ="회원가입" onclick ="registerhref()"></h3>
      {% endif %} 
      ```
    
  
<br><br><br>

### 이미지 업로드, 다운로드
1. 업로드 <br>
    ##0. Setting
      * template path 설정
      * media url 작성
          ```
              MEDIA_URL = '/media/'
              MEDIA_ROOT = BASE_DIR/'media' 
            ###해당 위치에 media 디렉토리 만들기 
          ```
      * installed_apps: 'updown'
      

    ##1. urls.py 

    ```
      urlpatterns = [
      path('admin/', admin.site.urls),
      path('', views.index, name='index'),
      path('upload/', views.upload_proc, name='upload'),
      ]
    ```
    ##2. views.py
    ```
    from django.core.files.storage import default_storage
    from django.core.files.base import ContentFile

    def upload_proc(request):
        file = request.FILES['uploadfile']
        upload = default_storage.save(file.name, ContentFile(file.read()))

        #default_storage : settings.py에서 설정한 MEDIA_ROOT 즉, BASE_DIR /'media'
        #default_storage.save(파일명, 파일)
        #upload_file.name : random을 파일명에 추가해서 올림(덮어쓰이지않도록)
    ```

    ##3.Template - Form tag 작성
    ```
    <form action="{%url 'upload'%}" method="post" enctype="multipart/form-data"> 
    ```
  <br>

2. 다운로드 <br>
 
    ##0.  urls.py
    ```
    path('download/<str:filename>', views.download_proc, name='download'),
    ```

 
    ##1. views.py
    ```
    from django.http import HttpResponse
    
    def download_proc(request,filename):
        return  HttpResponse(default_storage.open(filename).read(), content_type ='application/force-download')
    ```
    ##2. Template
    ```
      <input type="button" value = '다운로드' onclick="loaction.href ='/download/{{filename}}'">
    ```
<br><br><br>

### 모델 폼 만들기 (##9번부터 해당내용시작)

##0. 프로젝트(myphoto) 생성
```
django-admin startproject myphoto
```

##1. app 생성 (photo)
  
``` python 
cd myphoto
python manage.py startapp photo
```

##2. settings.py #project에만 존재

 * INSTALLED_APP : 'photo'
 * TIME_ZONE = 'Asia/Seoul'
 * DB연결


##3. models.py
```python
from django.db import models

class Photo(models.Model):
    title =models.CharField(max_length=50)
    author = models.CharField(max_length=50)
    image = models.CharField(max_length=200)
    description = models.TextField()
    price = models.IntegerField()

    def __str__(self):
        return str(self.title)
```

##4. migration <br>
##5. admin.py 작성
```python
from django.contrib import admin
from .models import Photo

admin.site.register(Photo)

 * 터미널 명령어: python manage.py createsuperuser
```
##6. (settings.py) ROOT URL은 
프로젝트 레벨의 urls.py로 기본 설정 되어있기 때문에,
app으로 작업시에는
app단위의 urls.py로 이동시켜주는 작업을 최초에 해줘야한다.
그 후 photo(app level)에서 urls.py 파일 생성후 작성
```python
from django.urls import path,include

urlpatterns = [
    path('', include('photo.urls')),
# 127.0.0.1/포함 모든 url은 photo.urls로 보내기
```

##7. views.py 작성

```python
from django.shortcuts import render, get_object_or_404, redirect
from .models import Photo

def photo_list(request):
    photo = Photo.objects.all()
    return render(request, 'photo/photo_list.html', {'photos':photo})
```

##8. (photo level) templates 디렉토리 생성 <br>
     > photo 디렉토리 생성 > html 문서 (photo_list) 작성

  * DB에서 list를 가져올 때는 클래스명.objects.all()로 가지고 온후 <br>
    template 에서 For 문으로 뿌려줘야한다. <br>
    {*for i in range 객체명*}
    {{i.title}}
    {*endfor*}

```html
    <section>
        {% for i in photos %} 
        <div>
            <h2><a href="{%url 'photo_detail' pk=i.pk %}">{{i.title}}</a></h2>
            <img src="{{i.image}}" alt="{{i.title}}" width ="300">
            <p>{{i.author}}, {{i.price}}</p>
        </div>

        {% endfor %}
    </section>
```

##9. 모델폼 사용을 위해 forms.py 파일 생성 후 작성
```python
from django import forms
from .models import Photo

class PhotoForm(forms.ModelForm):
    class Meta :
        model = Photo
        fields = ('title', 'author','image','description','price')
        
```


##10. views.py 작업

```python
from .forms import PhotoForm

##1. 수정
def photo_edit(request,pk):
    photo = get_object_or_404(Photo, pk=pk)
    if request.method =='GET':
        form = PhotoForm(instance=photo)
    elif request.method == 'POST':
        form = PhotoForm(request.POST, instance= photo)
        #폼 생성: 폼 _PhotoForm 사용, instance _Photo 클래스로부터 가져온 photo objects
        if form.is_valid():
        # form.is_valid(): #Django Form 클래스에서 제공하는 유효성 체크 함수
            photo = form.save(commit = False)
            photo.save()

       
    return render(request, 'photo/photo_post.html',{'form':form})
#속성하나하나 일일이 업데이트 시켜주지 않아도, 폼 메소드에서 제공하는 기능으로 일괄 처리를 할 수 있다. 
#Form을 생성했으면, return 값으로 밑에 폼을 뿌릴 template path를 설정해주고 (urls path안거침) 생성된 form 을 함께 전달해주면된다.

##2. 등록
def photo_post(request):
    if request.method == 'GET':
        form = PhotoForm()
        return render(request, 'photo/photo_post.html',{'form':form})


    elif request.method =="POST":
        form = PhotoForm(request.POST) #기존 title = ruquest.POST[title] 코딩구문
        if form.is_valid():
            photo = form.save(commit = False)
            photo.save()
            return redirect('photo_detail', pk= photo.id )

#신규 Post 코드는 Edit 코드에서 form = PhotoForm(instance=photo) instance만 제외하여 빈 폼을 생성 해주면 된다.

##3. 삭제
def photo_delete(request, pk):
    result = Photo.objects.filter(pk=pk).delete()
    
    if result[0]:
        return redirect('photo_list')
    else:
        return redirect('photo_detail', pk)
```


##11. Html(template)

``` python
<form action="" method ="post">
                {%csrf_token%}
                {{form.as_p}} 
                <!-- p tag로 form을 생성해라 -->
                <button type="submit"> Completed! </button>
            </form>
```
위처럼 form에 action을 안적고 submit을 하게 되면, <br>
현재 위치한 url을 그대로 재호출하게된다. <br>
즉 해당 url로 다시 request 가 가게되고, views.py에서 다시 처리를 하게된다.<br>
그러면 photo_edit 함수에서 이번에는 get방식이 아닌 <br>
post방식 로직으로 수행을 하게된다.

<br><br><br>

### 파일형식의 이미지 필드 생성하기


#0. settings.py
```python
MEDIA_URL = '/media/'
MEDIA_ROOT =BASE_DIR/'media'
```
작성후 해당 위치에 media 디렉토리 생성하기 <br>

##1. models.py (모델변경 : ImageField 추가)
```python
from django.conf import settings
imagefile = models.ImageField(upload_to=settings.MEDIA_ROOT,blank=True, null=True)
```

##1-1. 터미널 명령어 입력 
```
(django level에서) python -m pip install Pillow
(app level 에서) python manage.py makemigrations todo 
(app level에서) python manage.py migrate
```

<br>
##2. urls.py <br>

```python
from django.conf import settings
from django.conf.urls.static import static
## urlpatterns [] 뒤에 작성
 + static(settings.MEDIA_URL,document_root =settings.MEDIA_ROOT )
  ```

<br>
#3. forms.py ('imagefile' 추가 ) <br>

```python
class TodoForm(forms.ModelForm):
    class Meta:
        model = Todo
        fields = ('title' , 'description','important','complete','imagefile')
```

<br>

##3. Template Form 에 enctype 추가작성
```<form method="POST" enctype="multipart/form-data">```

##4. Views.py

```python

from django.core.files.storage import default_storage
from django.core.files.base import ContentFile



def todo_post(request):
    if request.method == "GET":
        form = TodoForm()
        return render(request, 'todo/todo_post.html',{'form':form})

    else :
        form = TodoForm(request.POST)
        if form.is_valid():
            todo = form.save(commit=False)
            todo.save()

###추가작성 시작부분
            upload_file = request.FILES['imagefile']
            upload = default_storage.save(upload_file.name,ContentFile(upload_file.read()))

#default_storage = /media 에 파일 업로드

Todo.objects.filter(id=todo.id).update(imagefile=upload)

#신규로 저장한 todo의 id를 참조해서 image 값을 update함

###~추가영역 끝부분

return redirect('todo:todo_list')
```

##5. 화면에 이미지 사진 보여지게 하기
  * 방법 1. Template 에 if문 넣기
```python

{% if obj.imagefile %}
                <p>
                  <img src="/media/{{obj.imagefile}}" alt="" width="300">
                </p>
              {% endif %}
# TIPS: 웹화면에서 F11 눌러 해당 코드가 객체들을 잘 불러왔는지 확인 필요
```
  * 방법 2 . views.py 함수에 if문 넣기

```python
if 'imagefile' in request.FILES.key():
            upload_file = request.FILES['imagefile']
            upload = default_storage.save(upload_file.name,
            ContentFile(upload_file.read()))
         
            Todo.objects.filter(id=todo.id).update(imagefile=upload)          
```

### TIPS!
```python
#1. urls.py 파일 : urlpatterns 상단에 app_name을 지정 해줄때 url 호출시 app명: 을 필수로 함께 작성, 그렇지 않으면 No Reverse Error 발생

    app_name ='todo'
    urlpatterns = []
    <a href="{% url 'todo:todo_list' %}" class="">Home</a>

#2. models. 여러가지 자료형
    a = models.DateTimeField(auto_now_add=True)
    b = models.BooleanField(default = False)
    c = models.BooleanField(default = False)

#3. visual studio tool 에서 'Django template' 확장 설치가능
#4. Restful api

    지금껏 다뤄온 방식은 웹서비스를 위해
    Html document로 응답 및 통신을 한다면,

    restful은 웹서비스가 목적이 아니라서 json으로 요청/답변을 한다. 

    그러므로 restful에는 template 절차가 없고 대신

    Views 요청 json >db로 바꿔주는 'deserializers'
    Db > json로 바꿔주는 'serializer' 작업절차가 있다.

```
<br><br><br>

### 두개의 테이블을 활용 : 투표 프로젝트 만들기


#0. Setting 
 Installed apps 에 'polls' 추가

#1. models.py

```python

from django.db import models

# Create your models here.

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.question_text


class Choice(models.Model):
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
    question_id = models.ForeignKey(Question, on_delete=models.CASCADE)

    def __str__(self):
        return self.choice_text

```


#1-1. migrations

#2. admin.py

 python manage.py createsuperuser

``` python
from django.contrib import admin
from .models import Question,Choice

admin.site.register(Question)
admin.site.register(Choice)
```



#4. urls.py

 * mypolls.urls.py
```python
from django.contrib import admin 
from django.urls import path,include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('polls/', include('polls.urls')),]
```
    

 * polls.urls.py
```python
from django.urls import path
from . import views

app_name = 'polls'
urlpatterns = [
    path('', views.index, name ='index'),
    path('<int:question_id>/', views.detail, name ='detail'),
    path('<int:question_id>/vote/',views.vote, name ='vote'),
    path('<int:question_id>/result/',views.result, name ='result'),

]

```



#5. views.py

```python
from django.shortcuts import render, get_object_or_404
from .models import Question,Choice
from django.http import HttpResponseRedirect
from django.urls import reverse
# Create your views here.


def index(request):
    question_list = Question.objects.all()
    return render (request, 'polls/index.html' , {'question_list':question_list})

def detail(request, question_id):
    question = get_object_or_404(Question, id= question_id)
    return  render(request, 'polls/detail.html', {'question':question})

def vote(request, question_id):
    question = get_object_or_404(Question, id=question_id)
    try:
        select_choice = question.choice_set.get(id=request.POST['choice'])
    except(KeyError, Choice.DoesNotExist):
        return render(request, 'polls/detail.html', {'question':question, 'error_message':'아무것도 입력되지 않았습니다.'})
    else:
        select_choice.votes += 1
        select_choice.save()

    return HttpResponseRedirect(reverse('polls:result', args = (question_id,)))

def result(request, question_id):
    question = get_object_or_404(Question, id=question_id)
    return render(request, 'polls/result.html',{'question':question})

```

#6. Template_index
```html
    {% if question_list %}
        <ul>
            {% for i in question_list %}
                <li> 
                    <a href="{%url 'polls:detail' i.id %}">{{i.question_text}}</a></li>
            {% endfor %}
        </ul>
    {% else %}
        <strong> 투표항목이 존재하지 않습니다. </strong>
    {% endif %}
```
#7. Template_detail

```html  
    <h1>{{question.question_text}}</h1>
    {% if error_message %}
    <p><strong>{{error_message}}</strong></p>
    {%endif%}

    <form action="{%url 'polls:vote' question.id %}" method="post">
        {%csrf_token%}
        {% for i in question.choice_set.all %}
            <input type="radio" name="choice" value = {{i.id}}
                id = 'choice{{forloop.counter}}' >
            <label for="choice{{forloop.counter}}">{{i.choice_text}}</label>
          <!-- forloop.counter : 인덱스가 1부터 시작 -->
          <!-- forloop.counter0 : 인덱스가 0부터 시작 -->
          <!-- choice1부터 ~ id가 생성되며 labeling 에 사용 -->

        {% endfor %}
        <input type="submit" value="Vote!">  
    </form>
    <!-- _set은 고정이며, choice는 연결된 고정명(소문자) -->
```

> 참고 <br> 
기본적으로 객체에 접근할 수 있는 매니저의 이름은 모델명(소문자)_set 으로 지어진다고 한다.<br>
ForeignKey로 어떠한 모델 A(Question)를 참조하고 있는 모델 B(Choice)는 <br>
모델 A에 접근할 때 미리 ForeignKey로 지정 해두었던 변수 (question)를 통해 접근할 수 있고, <br>
>> c= Choice.objects.get(pk=1) <br>
    c.question.question_text 

>참조되고 있는 모델 A는 모델 B에 접근할 때 모델명(소문자)_set의 형태로 접근한다. <br>
>>q = Question.objects.get(pk=1) <br>
q.choice_set.all()

#8. Template_result
```html
   <h1>{{question.question_text}}</h1>
    <ul>
        {%for i in question.choice_set.all %}
            <li>{{i.choice_text}} - {{i.votes}} votes</li>
        {% endfor %}
    </ul>
```
<br><br><br>

### Django에서 제공하는 USER Model을 사용해보기

##0. Settings
  - installed app :  'mymember',
  - templates 디렉만들기

##1. model.py : 작성필요없음 (django의 User 모델 사용)

##2. forms.py

```python
from django import forms
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth.models import User

class MymemberForm(UserCreationForm):
    class Meta : 
        model = User
        fields = ('username','password1','password2','email','first_name','last_name')

```

##3. Migration
```python manage.py makemigrations 절차필요 없음. Python manage.py migrate 만 진행```


##4. urls.py

```python 
from django.contrib import admin
from django.urls import path
from . import views
from django.contrib.auth import views as auth_views #기존 views와 명이 동일하여 alias 사용

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.index, name='index'),
    path('register/', views.register, name='register'),
    path('login/', auth_views.LoginView.as_view(template_name ='login.html'), name ='login'),
path('result/', views.result, name='result'),
path('logout/', auth_views.LogoutView.as_view(), name ='logout'),]

#'login'의 경우 django에서 제공하는 view함수를 사용하고 있으며, 

#get방식일때는 template_name에 들어가있는 'login.html'문서를 보여주고,

#post 방식일 때는 settings.py에 선언된 LOGIN_REDIRECT URL를 호출하게 된다. 

#이때 LoginView 함수를 직접 핸들링 할 수 없으니, return 값을 setting에서 지정 해준다. 로그인 성공시 객체세션정보를 추가하여 리턴하게 된다.

#'logout'도 동일한 방식이며 get방식일때 '/' 화면으로 이동하게 된다.

```

##5. settings.py

```html
LOGIN_REDIRECT_URL ='/result'
LOGOUT_REDIRECT_URL = '/' 
```


##6. views.py

```python
from django.shortcuts import render, redirect
from .forms import MymemberForm

def index(request):
    return render(request, 'index.html')


def register(request):
    if request.method == 'GET' :
        return render(request, 'register.html', {'form' : MymemberForm()})
    else :
        form = MymemberForm(request.POST)
        
        if form.is_valid():
            form.save()

        return redirect('index')


def result(request):
        return render(request, 'logout.html')
```

                                                                                                                

##7-1. Template_login

```html
<body>
    <form action="{%url 'login' %}" method= "post">
        {%csrf_token%}
        ID : <input type="text" name = 'username'>
        <br>
        PW : <input type="password" name ='password'>
        <br>

        <input type="submit" value ="login">

    </form>
</body>

<!-- Form. 의 다양한 활용법
#as_p
#as_ul
#as_table 
-->
```



##7-2. Template_logout
```html
<body>
    <h1> Hello {{user.username}}</h1>
    <h2>{{user.email}}</h2>
    <a href="/logout/"> logout </a>
</body>
```

<br><br><br>

### Final Project :bulb:!!!

myworld라는 프로젝트내에서 users와 board라는 두가지 앱을 생성할것이며, <br>

users에서는 로그인 프로세스를,
board에서는 게시판을 구현해 볼 것이다.<br>
<br>
장고에서 제공하는 모델을 오버라이딩,
폼은 모델폼을 사용해보자
<br>

비동기 방식인 ajax로 댓글구현까지해보자.<br>
ajax는 모든 폼 내용 을 100% 주고받지 않고, <br>
요청한 영역에 대한 부분만 통신하기때문에 <br>
효율적이며, 통신 중 에도 다른 작업을 병행해서 진행할수있게 해준다. <br><br>
ajax통신시에는 html문서가 아닌 xtml 또는 json파일로 주고 받는다. <br>
이 ajax를 객체화 한것이 리엑트나 뷰이다. <br>


--------------------------------------------------------

[0] Django

##0. project : myworld
     django-admin startproject myworld
     
     app : bbs, users
     cd lecture
     python manage.py startapp users
     python manage.py startapp board

[1] myworld

##1. Settings
 - installed apps :  'board','users'
 - templates: 'DIRS': [BASE_DIR/'templates'],
 - static
   STATICFILES_DIRS =[BASE_DIR/'static']
 - media
   MEDIA_URL = '/media/'
   MEDIA_ROOT = BASE_DIR/'media'
   <!-- MEDIA_ROOT는 리스트형태가 아닌것 주의! -->
 - auth
   AUTH_USER_MODEL = 'users.Member'
    <!-- 인증에 사용할 class를 users.Member로 지정, default는 auth_user로 되어있다.  -->

   AUTHENTIFICATION_BACKENDS = ['django.contrib.auth.backends.ModelBackend',]  
    <!-- 정해져 있음  대소문자 구분 됨 -->
  
  - DB


##2. urls.py
```python

from django.contrib import admin
from django.urls import path,include
from django.views.generic.base import TemplateView
from django.conf.urls.static import static
from django.conf import settings

urlpatterns = [
    path('admin/', admin.site.urls),
    path('users/',include('users.urls')),
    path('board/',include('board.urls')),
    path('', TemplateView.as_view(template_name = 'index.html'), name='home')
] +static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)

```



[2] users


##0. users_models.py <br>
     ❶ Django 에서 제공하는 user 모델을 오버라이딩 할때는 AbstractUser로 import하고 settings에 AUTH_USER_MODEL = 'users.Member'을 작성하여
     해당 모델로 바꿔줘야한다.


 ```python
from django.db import models
from django.conf import settings
from django.contrib.auth.models import AbstractUser


class Member(AbstractUser):
mobile = models.CharField(max_length=20)
image = models.ImageField(upload_to= settings.MEDIA_ROOT, blank = True, null = True)

#AbstractUser 모델을 상속받아서 mobile+image를 추가한 오버라이딩 클래스 Member를 생성한다.



```
 ❷ django 에서 제공하는 User 모델 그대로 사용 : 모델링 작업없이 바로 폼작업으로 가면됨 <br> <br> 

##1. migration <br>
    ```python manage.py makemigrations users``` <br>
    ``` python manage.py migrate```

##2. (Model 확인을 위해) Admins.py

```python 
from django.contrib import admin
from .models import Member
admin.site.register(Member)
```
```python manage.py createsuperuser```



##3. forms.py

Django에서는 내장폼으로 forms.Form과 forms.ModelForm을 제공한다.

Form을 HTML의 <form>태그를 다루기위한 도구라면 
ModelForm은 Form에 Model과 연동되어있다.

그렇기 때문에 Form은 코드를 통해 중복여부를 체크 해야하지만,
ModelForm은 속성을 통해 자체적으로 유효성 검사를 체크 해준다.


 ```python
from .models import Member
from django import forms
from django.contrib.auth.forms import UserCreationForm

#회원가입시에는 ModelForm을 상속받은 UserCreationForm 사용
class MemberForm(UserCreationForm):
    class Meta:
        model = Member
        fields =['username','password1','password2','email','mobile','image']

#로그인에는 ModelForm 사용
class LoginForm(forms.ModelForm):
    class Meta:
        model = Member
        fields = ['username', 'password']

        labels={
            'username' : '사용자이름',
            'password' : '비밀번호'
        }

        widgets = {
            'username' : forms.TextInput(
                attrs ={
                    'class' : 'form-control',
                    'placeholder' : '사용자이름을 입력하세요'
                }
            ),
            'password' :forms.PasswordInput(
                attrs={
                    'class' : 'form-control',
                    'placeholder' : '비밀번호를 입력하세요'
                }
            )
        }

```


##4. Urls 작업

❶ myworld.urls.py

```python

from django.contrib import admin
from django.urls import path,include
from django.views.generic.base import TemplateView
from django.conf.urls.static import static
from django.conf import settings

urlpatterns = [
    path('admin/', admin.site.urls),
    path('users/',include('users.urls')),
    path('board/',include('board.urls')),
    path('', TemplateView.as_view(template_name = 'index.html'), name='home')
] +static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)


```
❷ users.urls.py

```python

from django.urls import path,include
from django.conf.urls.static import static
from django.conf import settings
from . import views

app_name ='users'
urlpatterns = [
    path('login/', views.login, name ='login'),
    path('signup/', views.signup, name='signup'),
    path('signupProcess/', views.signupProcess, name='signupProcess'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('loginProcess/', views.loginProcess, name='loginProcess'),
] + static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)

```





##5. users.views.py
```python
#signupProcess 소스 코드 : 맥에서는 Createuser를 통한 request.FILES 적용이 안됨


from django.shortcuts import render, redirect
from .models import Member
from .forms import MemberForm,LoginForm
from django.contrib.auth import login as django_login, logout as django_logout
from django.contrib.auth import authenticate
from django.http import HttpResponse
from django.core.files.base import ContentFile
from django.core.files.storage import default_storage

def login(request):
    login_form = LoginForm()
    return render(request, 'users/login.html',{'login_form' : login_form})



def loginProcess(request):
    if request.method =='POST':
        login_form = LoginForm(request.POST)
        username = login_form.data['username']
        password = login_form.data['password']

        user = authenticate(username= username, password=password) #장고에서 로그인 성공여부 확인해줌
        if user is not None:
            django_login(request,user)
            return redirect('home')
        else:
            return HttpResponse('Failed to Login, Try it again')
    return HttpResponse('인증실패, POST가 아닙니다.')



def logout(request):
    django_logout(request)
    return redirect('home')
    #장고에서 세션종료해줌


def signup(request):
    member_form = MemberForm()
    return render(request, 'users/signup.html',{'member_form':member_form})


def signupProcess(request):
    if request.method == "POST":
        member_form = MemberForm(request.POST)
        if member_form.is_valid():
    
            if 'image' in request.FILES.keys(): #이미지첨부된 경우
                new_user = member_form.save(commit=False)
                new_user.save()
                upload_file = request.FILES['image']
                upload = default_storage.save(upload_file.name,ContentFile(upload_file.read()))
                # default_storage = /media,  화일 업로드 기능
                Member.objects.filter(username=new_user.username).update(image=upload_file)

            else: # 이미지 첨부 안됨
                new_user = Member.objects.create_user(
                    username = member_form.cleaned_data['username'], #validation이 완료된 데이터
                    email=member_form.cleaned_data['email'],
                    password=member_form.cleaned_data['password1'],
                    mobile=member_form.cleaned_data['mobile'],
                )

            # from django.contrib.auth import login as django_login
            # 로그인 세션처리 함
            django_login(request,new_user)
            return redirect('home')
        else:
            return HttpResponse('isvaild하지 않습니다.')
            # redirect('users:signup')
```

##6. bootstrap4 설치를 위해 터미널 pip install django-bootstrap4 입력 및
     settings.py installedapps 에'bootstrap4'추가

##7. templates

 * index.html
  
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body class ='text-center'>
    <header>
        <div>
            <h3>Lecture Project</h3>
        </div>
    </header>
</body>
<main>
    <p>Django Framework</p>
    <p class='lead'>
        {%if request.user.is_authenticated %}
            <img src="/media/{{request.user.image}}" alt="" witdh = '50px', height = '50px'>
            {{request.user.username}}님 환영합니다. 
            <a href="/board/list" class = 'btn btn-lg btn-primary'>Enter BBS</a>
            <a href="/users/logout" class = 'btn btn-lg btn-danger'>Logout</a>
        {%else%}
            로그인이 필요합니다.
            <a href="/users/signup/" class = 'btn btn-lg btn-success'>회원가입</a>
            <a href="/users/login/" class = 'btn btn-lg btn-primary'>login</a>
        {% endif %}
    </p>
</main>
<img src="/static/notice.jpg" alt="" width ='1024'>
<footer>
    <div>
        <p>Copyright 2023</p>
    </div>
</footer>
</html>
```

 * base.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://code.jquery.com/jquery-2.2.4.min.js" crossorigin = 'anoymouse'></script>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>

    {% block html_header %}
    {% endblock %}
</head>
<body>
    
    {% block html_body %}
    {% endblock %}


</body>
</html>
```
* signup.html

```html
{% extends 'base.html' %}
{% load bootstrap4 %}

{% block html_header %}
<style>
  .bd-placeholder-img {
    font-size: 1.125rem;
    text-anchor: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    user-select: none;
  }

  @media (min-width: 768px) {s
    .bd-placeholder-img-lg {
      font-size: 3.5rem;
    }
  }
</style>

<!-- Custom styles for this template -->
<link href="/static/css/signin.css" rel="stylesheet">
{% endblock %}

{% block html_body %}

<main class="form-signin">
    <form action="/users/signupProcess/" method = "POST" enctype= "multipart/form-data">
        {%csrf_token%}
        <h1 class ='h3 mb-3 fw-normal' >Register Now!</h1>
        {% bootstrap_form member_form %}

        <br>
        <button type="submit" class = "w-100 btn blt-lg btn-primary">Registration</button>
    </form>
</main>

{% endblock %}
```
 * login.html 
  
```html
{% extends 'base.html' %}
{% load bootstrap4 %}

{% block html_header %}


<!-- Custom styles for this template -->
<link href="/static/css/signin.css" rel="stylesheet">
{% endblock %}

{% block html_body %}

<main class="form-signin">
    <form action="/users/loginProcess/" method = "POST" >
        {%csrf_token%}
        <h1 class ='h3 mb-3 fw-normal' >Login!</h1>
        {{ login_form }}

        <button type="submit" class = "w-100 btn blt-lg btn-primary">Login</button>
    </form>
</main>

{% endblock %}
```

* static > css > signin.css 디렉토리 및 파일 생성후 작성<br>
  
```html
  
  html,
body {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
  background-color: #f5f5f5;
}

.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: auto;
}

.form-signin .checkbox {
  font-weight: 400;
}

.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
  ```
<br>
[3] board <br>
##0. urls.py

```python

from django.urls import path
from . import views

app_name ='boards'

urlpatterns = [
     path('list/', views.b_list, name='b_list'),
     path('create/', views.b_create, name='b_create'),
     path('<int:board_id>/detail', views.b_detail, name='b_detail'),
     path('<int:board_id>/update', views.b_update, name='b_update'),
     path('<int:board_id>/updateProcess', views.b_update_process, name='b_update_process'),
     path('<int:board_id>/like', views.b_like, name='b_like'),
     path('<int:board_id>/delete', views.b_delete, name='b_delete'),

    path('commentCreate/', views.c_create, name='c_create'),
] 
```

##1. models.py
```python
from django.db import models

# Create your models here.
class Board(models.Model):
    
    #b_no = models.IntegerField(primary_key=True)
    b_title = models.CharField(max_length=100)
    b_author = models.CharField(max_length=20)
    b_content = models.CharField(max_length=500)
    b_date = models.DateTimeField(auto_now_add=True)
    b_comment_count = models.IntegerField(default=0)
    b_like_count =models.IntegerField(default=0)

    def __str__(self):
        return self.b_title
    

class Comment(models.Model):
    c_author = models.CharField(max_length=20)
    c_content = models.CharField(max_length=500)
    board = models.ForeignKey(Board, on_delete=models.CASCADE)

    def __str__(self):
        return self.c_content

```

##2. migration <br>

##3. forms.py
```python
from django import forms
from .models import Board

class BoardForm(forms.ModelForm):
    class Meta:
        model = Board
        fields = ['b_title','b_author','b_content']

        labels = {
            'b_title' : '글제목',
            'b_author' : '글 작성자',
            'b_content' : '글 내용'
        }
        widgets= {
            'b_title' : forms.TextInput(
                attrs={
                    'class':'form-control w-50',
                    'placeholder':'글 제목을 입력하세요',
                }
            ),
            'b_author' : forms.TextInput(
                attrs={
                    'class':'form-control w-25',
                    'placeholder':'글 작성자를 입력하세요',
                }
            ),
            'b_content' : forms.Textarea(
                attrs={
                    'class':'form-control w-75',
                    'placeholder':'글 내용을 입력하세요',
                }
            )
        }

class BoardDetailForm(forms.ModelForm):
    class Meta:
        model = Board
        fields = '__all__'

        labels = {
            'b_title' : '글제목',
            'b_author' : '글 작성자',
            'b_content' : '글 내용',
            'b_comment_count' : '댓글 개수',
            'b_like_count' : '좋아요 개수'
        }

        widgets= {
            'b_title' : forms.TextInput(
                attrs={
                    'class':'form-control w-50',
                }
            ),
            'b_author' : forms.TextInput(
                attrs={
                    'class':'form-control w-25',
                }
            ),
            'b_content' : forms.Textarea(
                attrs={
                    'class':'form-control w-75',
                }
            ),
            'b_comment_count': forms.TextInput(
                attrs={
                    'class': 'form-control w-25',
                }
            ),
            'b_like_count' : forms.TimeInput(
                attrs={
                    'class' : 'form-control w-25',
                }
            )
        }


    def show_board_detail(self):
        fields= list(BoardDetailForm().base_fields)
        for field in fields:
            self.fields[field].widget.attrs.update({
                'readonly' : 'readonly'
            })

    def show_board_update(self):
        self.fields['b_like_count'].widget.attrs.update({
            'readonly':'readonly'
        })
        self.fields['b_comment_count'].widget.attrs.update({
            'readonly':'readonly'
        })
```
##4. views.py

```python
from django.shortcuts import render,redirect, get_object_or_404
from .models import Board, Comment
from .forms import BoardForm , BoardDetailForm
from django.http import JsonResponse

def b_list(request):

    if request.user.is_authenticated:
        posts = Board.objects.all()
        return render(request, 'board/list.html', {'posts' :posts})
    else : 
        return redirect('home')


def b_create(request):
    if request.method =="GET":
        board_form = BoardForm()

    else :
        board_form = BoardForm(request.POST)
        if board_form.is_valid():
            board_form.save()
            return redirect('board:b_list')
    return render(request, 'board/create.html',{'board_form':board_form})


def b_detail(request, board_id):
    post = get_object_or_404(Board, id=board_id)

    board_detail_form = BoardDetailForm(instance=post)
    board_detail_form.show_board_detail()

    return render(request, 'board/detail.html', {'board_detail_form' : board_detail_form})

def b_update(request, board_id):
    post = get_object_or_404(Board, id=board_id)

    board_detail_form = BoardDetailForm(instance=post)
    board_detail_form.show_board_update()

    return render(request, 'board/update.html', {'board_detail_form' : board_detail_form})


def b_update_process(request,board_id):
    post = get_object_or_404(Board, id=board_id) #수정처리 전 post
    if request.method =="POST":
        board_detail_form = BoardDetailForm(request.POST, instance=post)
        if board_detail_form.is_valid():
            board_detail_form.save()
            board_detail_form.show_board_detail()

            return render(request, 'board/detail.html', {'board_detail_form' : board_detail_form})
    return redirect('home')


def b_like(request, board_id):
    post = get_object_or_404(Board, id = board_id)
    post.b_like_count +=1
    #post.b_author= 'Lisa'
    post.save()

    # 트랜젝션처리를 하고 싶으면 모델이 아닌 모델폼객체를 사용하여 접근해야함
    # board_detail_form = BoardDetailForm(instance=post)
    # board_detail_form.b_like_count +=1
    # new_post = board.detail_form.save(commit = False)
    # board_detail_form.b_like_count =100
    # new_post.save

    board_detail_form = BoardDetailForm(instance=post)
    board_detail_form.show_board_detail()
    return render(request, 'board/detail.html', {'board_detail_form' : board_detail_form})




def b_delete(request, board_id):
    post = get_object_or_404(Board, id=board_id).delete()
    return redirect('board:b_list')


def c_create(request):
    
    # from .models import Board, Comment
    # from django.http import JsonResponse    
    comment = Comment()
    comment.c_author = request.GET['user_name']
    comment.c_content = request.GET['user_content']
    comment.board_id = request.GET['board_id']

    print ('---------------------------')
    print (request.GET['board_id'])
    print (comment.c_author)
    print (comment.c_content)
    print (comment.board_id)
    print ('---------------------------')

    comment.save()

    return JsonResponse({
        'comment_author': request.GET['user_name'],
        'comment_content': request.GET['user_content'],
        'comment_id': request.GET['board_id']
    }, json_dumps_params= { 'ensure_ascii' : True } )
  
```

##5. Template <br>
 * create.html
  ```python
  {% extends 'base.html' %}
{% load bootstrap4 %}

{% block html_body %}
   
    <div class='container'>
        <h1>새글 작성</h1>

        <form method="post">ß
        {% csrf_token %}
        {% bootstrap_form board_form %}

            <br>

            <button class="btn btn-primary" 
                    type="submit">등록</button>
            <button class="btn btn-secondary"
                    type="button"
                    id="board_list_btn" onclick="location.href='{% url 'board:b_list' %}'">리스트로 돌아가기</button>
        <form>    
    </div>

{% endblock %}
  ```
 * detail.html
  ```python
  {% extends 'base.html' %}
{% load bootstrap4 %}

{% block html_body %}
<script src="/static/js/c_comment.js"></script>
    <div class='container'>
        <h1>글 상세 보기</h1>
        글번호 : <span id = 'board_id'>{{board_detail_form.initial.id}}</span>
        {% bootstrap_form board_detail_form %}
    

    <br>

    <button class='btn btn-secondary' 
        onclick="location.href='{% url 'board:b_list'%}'" >리스트로 돌아가기</button>
    <button class='btn btn-info' 
        onclick="location.href='{% url 'board:b_update' board_detail_form.initial.id  %}'">수정</button>
    <button class='btn btn-danger' 
        onclick="location.href='{% url 'board:b_delete' board_detail_form.initial.id %}'">삭제</button>
    <button class='btn btn-warning'
        onclick="location.href='{% url 'board:b_like' board_detail_form.initial.id %}'">좋아요</button>

    </div>
    <br>
    <div class = 'container'>
        <div>
            <label for="c_name">이름</label>
            <input type="text" class='form-control w-25' id='c_name'>

            <label for="c_content">내용</label>
            <input type="text" class='form-control w-50' id='c_content'>
            <br>

            <button class = 'btn btn-primary' id ='comment_create_btn'>댓글등록</button>
            <br><br>

        </div>


        <table class ='table table-hover'>
            <thead>
                <tr>
                    <th>글 작성자</th>
                    <th>글 내용</th>
                    <th>삭제</th>
                </tr>
            </thead>

            <tbody>
                <tr>
                    <th></th>
                    <th></th>
                    <th></th>
                </tr>
            </tbody>




        </table>
    </div>
{% endblock %}
  ```
 * list.html
```python
{% extends 'base.html' %}


{%block html_body%}
    <div class ='container'>
        <h1>Bulletin Board System(BBS)</h1>
        <button class ='btn btn-primary' 
        onclick =" location.href ='{%url 'board:b_create' %}' ">새글작성</button>
       

        <table class = 'table table-hover'>
            <thead>
                <tr>
                    <th>#</th>
                    <th>글제목</th>
                    <th>작성자</th>
                    <th>작성일</th>
                    <th>댓글수</th>
                    <th>좋아요수</th>
                </tr>
            </thead>

            <tbody>
                {% for post in posts %}
                <tr>
                    <td>{{post.id}}</td>
                    <td><a href="{%url 'board:b_detail' post.id %}">{{post.b_title}}</a> </td>
                    <td>{{post.b_author}}</td>
                    <td>{{post.b_date}}</td>
                    <td>{{post.b_comment_count}}</td>
                    <td>{{post.b_like_count}}</td>
                </tr>
                {% endfor %}
            </tbody>
        </table>
    </div>

{%endblock html_body%}
```
 * update.html
```python
{% extends 'base.html' %}
{% load bootstrap4 %}
{%block html_body%}
    <div class='container'>
        <h1>글 수정하기</h1>
        <form action="{% url 'board:b_update_process' board_detail_form.initial.id  %}" method='post'>
            {%csrf_token%}
            {% bootstrap_form board_detail_form %}
       
        
 
 
    \
        <br>

        <button class='btn btn-secondary' 
            onclick="location.href='{% url 'board:b_list'%}'" >리스트로 돌아가기</button>
        <button class='btn btn-info' type = 'submit'>완료</button>  
    </div>
         </form>
{% endblock %}
```
### Ajax (비동기)방식으로 댓글 구현해보기

* base.html 구문추가
```python

<script src='https://code.jquery.com/jquery-2.2.4.min.js' crossorigin='anoymouse'></script>
```

* detail.html
```python
<script src="/static/js/c_comment.js"></script>
글번호 : <span id = 'board_id'>{{board_detail_form.initial.id}}</span>

```

* c_comment.js (script 디렉토리 > js 파일생성 후 작성)
  
```python

$(function(){ // onload function : 모두 로드되었을 때 
    $('#comment_create_btn').on('click',function(){ //comment_create_btn 클릭되었을때 실행함수

        $.ajax({
            async:true, // 비동기방식으로 ajax를 호출
            url : '/board/commentCreate/',  
            type : 'GET',
            //서버에 전송할 데이터
            data :{
                board_id : $('#board_id').text(),
                user_name : $('#c_name').val(),
                user_content : $('#c_content').val()
            }
        })
    })
    })

```
    

