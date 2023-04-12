
## Cloud Infra Structure
<br>

기본적으로 시스템 아키텍처는 1개의 하드웨어에
1개의 운영체제가 사용가능한 구조라 하드웨어의 사용 효율성이 떨어진다.
하드웨어의 사용량을 극대화하기 위해서
OS를 여러개 올릴 수 있게 해주는 하이퍼 바이저 프로그램을 통해 
그위에 여러 가상 머신을 만들어 사용한다. 가상머신도 머신이기 때문에 하드웨어 리소스가 필요하다.

pkg&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  |  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pkg <br> 
python3.9&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      | &nbsp;&nbsp;&nbsp;&nbsp;python 3.8   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                           &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  ==> 가상환경 별로 다른 장비처럼 활용가능 <br>
*base &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;myEnv (사용자 가상환경)             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;              (virtual env)  <br>
<br>
+++++++++++++++++++++++++++ <br>
┌──────────┐<br>
&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; APP &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; │    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;아나콘다(Jupyter Notebook IDE) , 파이참, chrome <br>
└──────────┘<br>
┌──────────┐<br>
&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    OS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  [Linux] h/w제어를 위해 VM위에 ubuntu os 설치 &  ssh (putty를 통한 access가능) <br>
└──────────┘ <br>
┌──────────┐<br>
&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;VM   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  vm (vcpu, vmemory, vdisk, vlan)<br>
└──────────┘<br>
┌──────────┐<br>
&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hyperviser&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│   <br>
└──────────┘<br>
┌──────────┐<br>
&nbsp;│ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; OS    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; │   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [window/ mac] 하드웨어 제 __logical / app 이 동작하기 위해 os가 하드웨어 리소스를 할당<br>
└──────────┘<br>
┌──────────┐<br>
&nbsp;│ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HardWare &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; h/w (cpu__'processor', memory___'ram', disk___'ssd') __physical<br>
└──────────┘<br>
<br>
* VM, OS, APP = OVA file
<br><br>

윈도우에서 vm(ubuntu) ip로는 직접적 접근이 불가하여
hypervisor 내에서 port forwarding 역할을 담당하는 
NatNetwork (Nat : Network Address translation) 을 활용한 네트워크 환경구성 필요

윈도우에서 → 하이퍼바이저까진 접근 가능 →
하이퍼바이저가 포트포워딩으로 우분투로 보내줌

- installation : 외부에 있는 프로그램을 디스크에 위치시키는것
- booting : os가 메모리에 올리는 것 (부트로더가 해줌)
- login : 쉘을 사용할 수 있도록 인증하는 과정
- execute : Hard Disk 에 프로그램을 메모리에 올리는것 (os가 해줌)
 

-----------------------------------------

## 리눅스 기본 명령어

<br>

[option] <br>
 \- : 약자  
 -- : full word

[command]<br>
ps (process show) <br>
man ls <br>
ls -l <br>
id (사용자 정보) <br>
gid (primary group, secondary group) <br>
who #하나의 장비를 여러 조원이 같이 동시 접속 사용자 확인  <br>
who -q <br>
who -H <br>
who am i <br>
passwd username <br>
users <br>
finger <br>
last (login log) <br>
cat /etc/os-release <br>
uname -a( kernel info) <br>
su - root (switch User) * su - default : root <br>
su - ubuntu <br>
pwd <br>
su root # without dash : 환경은 유지, 계정만 변경 _ pwd 확인 <br>
su - root # wirh dash : 바뀌는 계정의 환경으로 바꿔줌 _ pwd 확인 <br>
exit <br>
sudo (switch user do)  <br>
sudo  (실행자의 패스워드를 입력필요)  <br>
su (전환되는 계정의 패스워드를 입력필요) <br>
**installation 은 관리자 권한으로 가능하고, 이를 위해 sudo를 사용 <br>
**sudo 자체가 슈퍼유저가 아니라, <br>
뒤에 빈칸이니까 디폴트값(root)이 적용되어, 관리자 권한인 것<br>

cd .. : 한단계 상위 디렉토리로 이동  <br>
cd /  : 최상위 디렉토리로 이동 <br>
cd ~  또는 cd : 자신의 홈 디렉토리 이동<br>
cd ~사용자 계정 : 지정된 사용자 계정의 홈디렉토리 <br>
cd - 작업 디렉토리 이전 작업 디렉토리로 변경<br>


ls : 디렉토리 리스트 <br>
ls -a : 숨김파일까지 출력 <br>
ls -l : 파일의 정보를 자세히 출력  <br>
ls -la : a+l <br>
ls -aF :  파일 / 디렉토리 구분 <br>
ls -aFl : (=ll) <br>

ls -ali (i : 고유번호) <br>

.으로 시작한 파일은 숨겨진 파일 <br>
ls -a 로 명령어를 쳐야 hidden file 까지 모두 조회됨 <br>
-로 시작하는건 파일 <br>
d로 시작하는건 디렉토리 <br>


------------
## Directory
<br>

```root``` directory : ```/``` <br>
Linux는 단일 파일시스템으로 ```루트``` 밑에 마운트 (/mnt/) 하는 구조 <br>
Window는 각각 알파벳 directory별로 저장 장치마다 개별 트리구조 <br>

관리자 계정 홈 디렉토리 : ```/root``` <br>
일반유저 홈 디렉토리 : ```/home/user명``` <br>
/etc :환경설정 관련 파일 <br>
/usr/bin (#bin : binary) <br>

상대경로 :  현재 사용자 위치 기준으로 디렉토리 하에 있는 경로 접근 <br>
절대경로 : 최상위노드 (```/```)를 기준으로 경로 접근 <br>


../ 하나 상위 디렉토리  <br>
./ 현재 디렉토리  <br>
~ (Tild) : / ~ 사용자의 홈디렉토리의 절대경로  <br>



--------------

## vi 편집기
<br>

### <b>Last Line mode</b> <br>
> esc → : 


1. 그냥 끝내기 (변경사항이 없을 때) <br>
     esc → : → q

2. 저장안하고 강제로 끝내기( 변경사항이 있을 때) <br>
    esc → : → q!

3. 저장하고 종료안함 <br>
    esc → : → w
   
4. 저장하고 종료 <br>
    esc → : → wq

### <b>Command Mode</b><br>
> vi file경로
1. 커서이동 (hjkl) {또는 화살표키)
2. file open
     - file명이 없으면 생성 , file명이 있으면 오픈 <br>

3. ^ : 커서가 위치한 라인의 시작
4. $ : 라인의 끝
5. x  : delete key 
6. X : backspace key
7. dd : line delete 
8. [n]G : 문서의 마지막 라인으로 이동
9. ctrl+g : 몇번째 라인인지 확인
10. dG : 전체 삭제
11. D: 현재위치다음부터 해당 라인전체 삭제
12. cw : 한단어변경 후 escape key로 나오기
13. c$ : 문장의 끝까지 변경 후  escape key로 나오기
14. 복사 (단어) yw (라인) yy
15. 붙여넣기 p (커서뒤) P(커서앞)
16. u : 실행취소 1번만 가능
17. U : line의 최초상태 원복
18. ? : 검색  + n (next_backward) | N (foreward)
19. / : 검색  + n (next_backward) | N (foreward)








<br>

### <b>Insert Mode</b><br>
> 키보드를 통해 문자를 입력하는 모드<br>
1. i : 커서가 현재 있는 위치에서 입력모드
2. a :커서가 한칸 앞으로간다
3. o :밑에 줄로

4. I : 커서 라인 앞에 문자 입력
5. A : 커서 라인끝에 문자 입력
6. O :윗줄에 삽입


  <-> esc <br>
        - back space → esc : 입력한 부분 다시 삭제


--------------------


## 파일시스템관리
<br>

#1. 접근권한
파일의 종류 c,b,l,d(디렉토리),-(파일) <br>
#2. 링크수 <br> 
#3. 파일의 소유자 <br>
#4. 파일의 소유그룹 <br>
#5. 파일의 크기 (기본단위는 바이트) <br>
#6. 파일의 생성일자나 최근수정일자 <br>
#7. 파일의 이름이나 디렉토리 이름 (i- node number) <br>

mkdir -p : 한번에 여러개의 파일 생성 (하위폴더까지) <br>
ls - R : 하위폴더까지 모두 보여줌 <br>
rmdir : 하위폴더가 없을때만 폴더 삭제가능 <br>
rm -r : 한번에 하위폴더까지 삭제 <br>
cat : 파일전체를 한번에 출력 <br>
less : page단위로 끊어서 보여줌 (q로 나옴) <br>
more : page단위로 끊어서 보여줌 (q로 나옴) <br>
head -5 : 5줄 보여줌 (q로 나옴) / default : 10 줄<br>
tail -5 : 5줄 보여줌 (q로 나옴) / default : 10 줄<br>

touch <br>
1) file명이 존재할때 : 해당 파일 시간 업데이트
2) file명이 존재하지 않을때 : 해당 파일명으로 파일이 생성

cp 원본경로 사본경로 : 파일복사<br>
cp -r : 디렉토리 하위의 내용을 모두 복사 <br>
mv 파일 이동경로 : 이동 <br>
df -h : (Disk Free) 저장공간 확인

-----------

 
## file Systmem 
> Address / Index
<br>

파일시스템은 논리적인 파일을 물리적인 디스크에 저장하여 관리하기 위한 구조며 <br>
디스크 내 ```i-node-table``` 공간이 각각의 논리적인 주소를 가지고 있다. <br>
관리적으로 논리주소체계를 생성하는 것을 Window에서는 ```포맷``` <br>
Linux에서는 ```mkfs``` 또는 ```newfs```라고 부른다.<br>
또한 포인터(주소)와 ~ 데이터블록이 연결된 구조를 ```링크```라고 부른다.
<br>
우리가 흔히 사용하는 rm 명령어는 사실 파일을 지우는게 아니라, <br>
이 링크를 끊는것이다 (해당 파일에 접근 방법이 없어지는것)<br>
또한 파일 복구프로그램은 링크되어 있지 않은 파일까지 포함하여 <br>
디스크에 저장 되어있는 모든 곳을 물리적으로 탐색 하는 것이다.<br>

--------------------------------


## 파일관리 
<br>

<b>소유권 (inode정보)</b> <br>
 - u : 소유자
 - g : 소유그룹
 - o : other
 - a : u+g+o
  
<b>허가권</b> <br>
 - r (read) 
 - w (write)
 - x (execute)

|user |group|others|
|---|---|---|
|rwx |rwx|rwx|

<br>

<b>sudo권한으로 계정 생성하여 소유권 이전하기 </b><br>
sudo useradd testusr <br>
sudo passwd testusr <br>
chown testusr text.txt <br>
chown testusr:testusr testfile   ```소유주와 소유그룹을 한번에 변경 가능```

<br><br>
<b>명령어</b> <br>
chown root test.txt ```test.txt파일을 root에게 소유권 이전```<br>
chgrp 그룹명 test.txt ```test.txt파일을 그룹명에게 소유권 이전```<br>
chmod g+w test.txt ```group에 w권한 부여```<br>
chmod g-w test.txt ```group에 w권한 제거```<br>
chmod u-w test.txt ```user에 w권한 제거``` <br>
chmod o-w test.txt ```others에 w권한 제거``` <br>
ls -ld ```디렉토리 권한 확인``` <br>
ls-d /tmp ```tmp 파일에는 others에도 rwx권한이 모두 있어 보통 이 공간에서 작업하면된다```) <br>



<br>

### Default Permission

1) file (666) - umask(002) = 664 <br>
  (기본)               rw-rw-rw-    <br> 
  (After Umask)       rw-rw-r--     <br> 

1) Directory (777) - umask(002) = 775 <br> 
  (기본)               rwxrwxrwx  <br> 
  (After Umask)       rwxrwxr-x  <br> 
directory는 대부분 rwx중 x가 있다.<br> 
x가 없으면 cd가 안되기 때문<br> 

> umask <br> 
보안을 위해 마스킹 처리하는 부분 <br> 
0002  (원래 비트는 4비트로 구성되어있음, 첫번째 비트는 논외로..!)<br> 
002 = w , 마지막 Others에 write권한 제거를 의미<br> 

<br> <br> 

### 8진수 변환법

r w x    r w x    r w x  <br> 
4 2 1    4 2 1    4 2 1  <br> 

chmod 777 aaa
          ugo

### chmod 활용예시
```
chmod u-x, g+w, o-rwx aaa
chmod 744 test.sh
#보통은 8진수 변환법을 사용한다.
```
<br> <br> 

### Directory Permission
- 파일의 소유주가 파일에 대한 허가권이 없는데도, <br> 
파일을 삭제할 수 있는데<br> 
그 이유는 파일을 만들거나 지우거나 이동하는 권한이<br> 
파일이 생성될(된) 디렉토리의 권한에 있기 때문이다.<br> 
<br> 
(but 관리자는 이와 상관없이 모두 가능하다.)<br> 
rm -f 명령어는 허가권없이, 확인절차도 없이 삭제하는 명령어 (위험)<br> 


-----------------------------------------------------------------
## 프로세스 관리
```
ps                 #나와 관련된 프로세스만 출력
ps -e | wc -l      #모든 프로세스 출력
ps -ef             #누가 뭘 실행하고 있는지
pstree
top : 프로세스별 CPU 등 리소스사용량 확인 (I :IDLE 작업안하고 있음)
kill : 프로세스에 신호를 전달
 [Signal]
 -sigterm(15) #default signal
 -sighup(0)
 -sigkill(9)

kill PID        #terminated
kill -9  PID    #killed
```
전면에서 돌고 있는 프로세스는 정리하고 싶을때 ctrl +C 로 취소 시키면 되지만,<br>
백그라운드에서 실행되고 있을 시 kill로 프로세스를 죽일수 있다. 

-----------------------------------------------------------------
## Shell

<br>

리눅스(커널)과 사용자의 인터페이스 역할 (명령어 인터프리터) <br>
종류
1. bash  - default
2. csh
3. tcsh
등등 많으며 install 가능하다

[명령어] --shell에 의해 실행됨
```
ps
sh
vi
ls
```
<br><br>
-----

### Shell Programming

*참고 linux는 확장자 개념이 없다

```실습
vi test.sh

pwd
sleep5
id
sleep 5
date

./test.sh
chmod 744 test.sh
ll
./test.sh
```
shell programming은 호출하는게 함수가 아닌 명령어를 순차적으로 호출하는 것 뿐이다. <br>
기본적으로 executive permission (실행권한) 이 요구되지만, <br>
```bash ./test.sh``` <br>
위 명령어와 같이 쉘을 실행시키면서 동시에 쉘스크립트를 실행시키면 <br>
강제로 실행시킬 수도 있다. <br>

<br><br>
-----

### Shell 입출력
```ls -l /dev/pts/0 ``` <br> 
→ 내가 할당받은 터미널 0  <br> 

기본적으로 키보드로 인풋을 받고, 터미널로 아웃풋을 받게됨<br> 

#0. stdin (표준입력) <br>
#1. stdout (표준출력) <br>
#2. stderr (표준에러출력) <br>


### <b>redirection (입출력의 방향을 바꿔줌)</b>
|>|2>| < | &>
|:---:|:---:|:---:|:---:|             
|#1|#2|#0|#1, #2|


[정상출력] <br> 
date > /dev/pts/1 ```date출력을 dev/pts/1 터미널로 리다이렉트시킴``` <br> 
date > date.out ```date출력을  date.out파일로 생성시킴``` <br> 
date >> date.out  ```파일에 내용을 누적시킴```<br> 

[비정상출력-에러 :2] <br> 
koo 2>> koo.err ```koo 입력시 발생하는 에러를 koo.err파일로 누적저장 ```<br> 
cat koo.err<br> 


### pipeline (|) :명령어의 실행결과를 다른 명령의 입력으로 사용되도록 하는 방법
[파이프라인 명령어]
1. ; <br>
기본적으로 한줄에 한 명령어써야하는데<br>
여러 명령어를 하려면 ; 로 명령어를 구분해서 입력하면됨<br>

2. || <br>
앞의 명령어가 실행되지 않아도 다음 명령어 실행<br>

3. && <br>
앞의 명령어가 실행되면 다음 명령어 실행<br>

4. grep <br>
특정파일이나 명령어 수행결과로 부터 특정 문자열을 검색 <br>
해당 문자열이 포함된 라인만 화면에 출력<br>
```cat /etc/passwd|grep ubuntu``` <br>

5. wc <br>
-c : 문자의수 <br>
-w : 단어수  <br>
-l : 문장의수 <br>
*디폴트는 문장수의, 단어의수, 문자의 수  <br>

활용예시
```
cat /etc/passwd | head -3
cat /etc/passwd | wc
*wc :word count

cat /etc/passwd | sort
cat /etc/passwd | cut -f1,6 -d: 
*-d: (deliminator를 :로 지정 )
*f1,6 (1번째와 6번째)
```
<br><br>
-----

### <b> Shell Process Life Cycle </b>

(ps -f) 명령어 입력시 

fork() 라는 system call 발생 (fork() : 똑같이 생긴 쉘을 복사, pid도 동일함) <br>
exec() 라는 시스템 콜이 발생하면서 포크된 쉘의 code가 명령어로 변경됨 <br>
exit()시스템 콜이 발생 <br>
본 shell은 그동안 sleep 상태에 있다가 exit콜이 발생시 전면에 다시 나타남<br>
즉, 본 shell에서 포크가 되면서 각 프로세스들이 만들어 지는 것<br>
프로세스가 백그라운드에서 돌면 ps로 확인 가능하다 <br>
```
sleep 6000 & 
# & 은 background process로 실행시키는 명령어
```

* PID : user가 실행시키고 있는 프로세스 아이디 <br>
* PPID : 부모 프로세스 아이디 (본 shell) <br> 
* UID : user 아이디 <br>


<br><br>

### <b> Shell 구성 </b>

1) local memory (로컬) 영역 : 새로운 프로세스 영역까지는 상속되지 않음 <br>
2) env memory (환경변수) 영역 : 새로운 프로세스 영역까지 상속<br>

<br><br>

### <b>System Calls</b>

```applications('putty') →  shell →  system calls(aka 'API') [open, read, write, close] →  kernel ('OS') →   H/W```

<br>
user는 기본적으로 os를 통해서 디바이스를 제어 해야한다.<br>
만약 하드디스크 내에 저장된 파일을 오픈하려면 <br>
open() 콜이 발생 해야하고 <br>
권한이 확인되면, read() call이 발생 해야한다. <br>
그다음 write() , close() 등의 호출이 필요한데  <br>
이 모두가 system calls 라 불린다. <br><br><br>


### <b>변수선언</b>
쉘에서도 변수 선언이 가능하다.
```python
koo = 9
echo $koo

# local영역은 app까지 상속이 안되기 때문에 변수도 상속안됨
# 그래서 끝까지 상속되는 성격을 가진 환경변수로 변수를 export시켜야함

var = 8
echo $var #local 변수

sh #>> fork가 exec 된 shell로 변경
echo $var
exit
echo $var
export var #환경변수로 만들어줌
echo $var

#app은 본쉘에서 포크 - execute되서 생성되기때문에
#모두 환경변수를 만들어야 app이 생성될때 변수가 상속된다.

env #환경변수확인
set #지역변수확인 +환경변수 확인
```
<br><br>
-----

### <b>환경설정</b>

쉘은 로그인 할 때마다 히든파일 .bashrc 을 다시 읽기 때문에 <br>
만약 해당 파일에 path를 작성해 놓았다면 <br>
path를 임의 변경 후 로그아웃 및 재로그인해도 path가 다시 원복 된 것을 확인 할 수 있다. <br>
<br> 이처럼 사용자 개인의 쉘옵션을 영구적으로 적용 하려면  ~/.bashrc 에 작성 해줘야 한다.
<br>/etc/profile 파일은 시스템 전역 쉘 변수들을 초기화 하는거라 안 건들이는 것이 좋음
```python
alias c=clear
#memory에만 설정되어있음

vi .bashrc
alias c=clear

source ~/.bashrc #를 실행해줘야 바로 적용됨
#또는 source 대신 아래 명령어도 가능
. /.bashrc
```

