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
            {%if list.number == i %}
                <a>{{i}}</a>
            {% else %}  
                <a href="?page={{i}}">{{i}}</a>   
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
   1) views.py
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
   2) Templates
   
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
          ```python
              MEDIA_URL = '/media/'
              MEDIA_ROOT = BASE_DIR/'media' 

            ###해당 위치에 media 디렉토리 만들기 
          ```
      * installed_apps: 'updown'
      

    ##1. urls.py 

    ```python
      urlpatterns = [
      path('admin/', admin.site.urls),
      path('', views.index, name='index'),
      path('upload/', views.upload_proc, name='upload'),
      ]
    ```
    ##2. views.py
    ```python
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
    ```python
    <form action="{%url 'upload'%}" method="post" enctype="multipart/form-data"> 
    ```
  <br>

2. 다운로드 <br>
 
    ##0.  urls.py
    ```python
    path('download/<str:filename>', views.download_proc, name='download'),
    ```

 
    ##1. views.py
    ```python
    from django.http import HttpResponse
    
    def download_proc(request,filename):
        return  HttpResponse(default_storage.open(filename).read(), content_type ='application/force-download')
    ```
    ##2. Template
    ```html
      <input type="button" value = '다운로드' onclick="loaction.href ='/download/{{filename}}'">
    ```
<br><br><br>

### 모델 폼 만들기 (##9번부터 해당내용시작)

##0. 프로젝트(myphoto) 생성
```python
django-admin startproject myphoto
```

##1. app 생성 (photo)
  
```python 
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

##4. migration
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

```python

{% if obj.imagefile %}
                <p>
                  <img src="/media/{{obj.imagefile}}" alt="" width="300">
                </p>
              {% endif %}
# TIPS: 웹화면에서 F11 눌러 해당 코드가 객체들을 잘 불러왔는지 확인 필요
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

```
