
## Cloud Infra Structure
<br>

기본적으로 시스템 아키텍처는 1개의 하드웨어에
1개의 운영체제가 사용가능한 구조라 하드웨어의 사용 효율성이 떨어진다.
하드웨어의 사용량을 극대화하기 위해서
OS를 여러개 올릴 수 있게 해주는 하이퍼 바이저 프로그램을 통해 
그위에 여러 가상 머신을 만들어 사용한다. 가상머신도 머신이기 때문에 하드웨어 리소스가 필요하다.

pkg            |  pkg
python3.9      |  python 3.8                                ==> 가상환경 별로 다른 장비처럼 활용가능 <br>
*base          |  myEnv (사용자 가상환경)                           (virtual env)  <br>
<br>
+++++++++++++++++++++++++++ <br>
┌──────────┐<br>
│&#160&#160&#160&#160 APP &nbsp;   │    아나콘다(Jupyter Notebook IDE) , 파이참, chrome <br>
└──────────┘<br>
┌──────────┐<br>
│    OS    │    [Linux] h/w제어를 위해 VM위에 ubuntu os 설치 &  ssh (putty를 통한 access가능) <br>
└──────────┘ <br>
┌──────────┐<br>
│    VM    │     vm (vcpu, vmemory, vdisk, vlan)<br>
└──────────┘<br>
┌──────────┐<br>
│Hyperviser│   <br>
└──────────┘<br>ㄱ
┌──────────┐<br>
│  OS      │    [window/ mac] 하드웨어 제 __logical / app 이 동작하기 위해 os가 하드웨어 리소스를 할당<br>
└──────────┘<br>
┌──────────┐<br>
│ HardWare │    h/w (cpu__'processor', memory___'ram', disk___'ssd') __physical<br>
└──────────┘<br>
<br>
* VM, OS, APP = OVA file
<br><br>

윈도우에서 vm(ubuntu) ip로는 직접적 접근이 불가하여
hypervisor 내에서 port forwarding 역할을 담당하는 
NatNetwork (Nat : Network Address translation) 을 활용한 네트워크 환경구성 필요


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

- <b>Last Line mode</b> <br>
esc → : 


   1. 그냥 끝내기 (변경사항이 없을 때) <br>
     esc → : → q

   2. 저장안하고 강제로 끝내기( 변경사항이 있을 때) <br>
    esc → : → q!

   3. 저장하고 종료안함 <br>
    esc → : → w
   
   4. 저장하고 종료 <br>
    esc → : → wq

- <b>Command Mode</b><br>
 vi file경로
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

- <b>Insert Mode</b><br>
키보드를 통해 문자를 입력하는 모드<br>
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
 - 소유자
 - 소유그룹
 - other

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



