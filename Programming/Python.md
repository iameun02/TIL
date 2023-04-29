## PYTHON
<br/>

### 1. 문자열 포매팅 4가지 방법
```python
#출력물

name = 'Lee'
age= 30
email = 'Lee@hotmail.com'

# +연산자
print('이름 : ' + name + ',' + ' 나이 : ' + str(age) + '세, ' + 'email : ' + email)

# 표식
print("이름 : %s, 나이 : %d세, email : %s" %(name, age, email))

# Format 메서드
print("이름 : {}, 나이 : {}세, email : {}".format(name, age, email))

# f문자열
print(f"이름 : {name}, 나이 : {age}세, email : {email}")
```
----

### 2. 파일 입출력
<br/>

|모드|수행|설명|
|:---:|:---:|:---:|
|r|읽기모드|파일을 읽기만 할때 사용
|w|쓰기모드|파일에 내용을 쓸 때 사용
|a|추가 모드|파일의 마지막에 새로운 내용을 추가 할 때 사용|
<br/>

  1) 파일쓰기


    
```python
f = open('filewr.txt','w')

f.write('This is first line.\n')
f.write('This is second line.\n')
f.write('This is third Line.\n')

f.close()
```
1) 파일 읽기
+ READ()
  ```python
  f = open('filewr.txt','r')
  
  contents = f.read()
  print(contents)

  f.close()
  ```
+ READLINE()
  ```python
  f= open('filewr.txt','r')

  while True:
      line = f.readline()
      if line:
        print(line, end='')
      else:
        break
  f.close() 
  ```
+ READLINES()
    ```python
   f = open('filewr.txt', 'r')
  
   lines = f.readlines()
   for line in lines:
       print(line, end='')

  f.close()
 

3) 내용추가
```python
f = open('filewr.txt','a')
    
f.write('This is fourth line.\n')
f.write('This is fifth line.\n')
    
f.close()
```


4) WITH 구문
```python
with open('filewr.txt','a') as f :
f.write('with구문으로 파일 자동 close함. \n')
```
