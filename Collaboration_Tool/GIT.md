## Why Git & Github?
---

![Git로고](https://user-images.githubusercontent.com/49775540/168756716-68f9aebb-380f-4897-8141-78d8403f6113.png)

### Git

 - 분산 버전 관리 프로그램
 - 백업, 복구, 협업을 위해 사용
 - [Git 공식문서](https://git-scm.com/book/ko/v2)

### Github

- Git을 사용하는 프로젝트의 협업을 위한 웹호스팅 서비스
- 포트폴리오를 자랑할 수 있는 공간
- 1일 1커밋 하기
- [이동욱님 Github 계정](https://github.com/jojoldu)


## CLI
---
> CLI (Command Line Interface, 커맨드 라인 인터페이스)는 터미널을 통해 사용자와 컴퓨터가 상호 작용하는 방식을 뜻한다.

<br>

#### 터미널 명령어 
  - pwd : 현재위치 절대경로
   - mkdir : 폴더 만들기
   - cd : 폴더 이동
   - touch : 파일 만들기 
   - open : 파일 열기
   - start : 파일 열기 
   - mv 
     1) 파일명 변경 
     2) 파일 이동 >> 이동할 경로가 존재하지 않을 경우 파일명 변경
   - ls : 현재 디렉토리 내용의 리스트 출력
   - rm : 파일 삭제
   - clear : screan clean up




#### 단축키
- 위, 아래 방향키 : 과거에 작성했던 명령어 조회
- tab : 폴더/파일 이름 자동 완성
- ctrl + a : 커서가 맨 앞으로 이동
- ctrl + e : 커서가 맨 뒤로 이동
- ctrl + w : 커서가 앞 단어를 삭제
- ctrl + l : 터미널 screen scroll up
- ctrl + insert : 복사
- shift + insert : 붙여넣기

> 예시
```python
$ mkdir test

$ touch a.txt

$ ls
$ ls -a

$ cd ..
$ cd test

$ rm a.txt
$ rm -r test
```

<br><br>

## Visual Studio Code
---
> Visual Studio Code (비주얼 스튜디오 코드)는 마이크로소프트에서 개발한 텍스트 에디터의 한 종류이다.

### 장점

- Windows, Mac, Linux 운영체제를 모두 지원한다.
- 기존 개발 도구보다 빠르고 가볍다.
- Extension을 통해 다양한 기능을 설치할 수 있어서, 무한한 확장성을 가진다.
- 무료로 사용 가능하다.

### Git Bash 연동하기

1. 터미널을 연다. (Ctrl + `)
2. 화살표를 누르고 Select Default Profile을 클릭한다.
3. Git Bash를 선택한다.
4. 휴지통을 눌러서 터미널을 종료하고, 재시작한다.
   + 휴지통은 Kill Terminal 로써, 터미널 자체를 아예 종료한다.
   + 닫기는 Close Terminal 로써, 터미널을 종료하지 않고 창만 보이지 않게 만든다.
5. 기본 터미널이 Git Bash로 열리는지 확인한다.

<br>

## Markdown
---
> Markdown (마크다운)은 일반 텍스트 기반의 경량 Markup (마크업) 언어이다.

### Markup (마크업) 이란?

- 마크(Mark)로 둘러싸인 언어를 뜻한다. 마크란 글의 역할을 지정하는 표시이다.
- HTML도 마크업 언어인데, 글에 제목의 역할을 부여할 때 `<h1>제목1</h1>` 과 같이 작성한다.

### 마크다운의 장점과 단점

1. 장점
   + 문법이 직관적이고 쉽다.
   + 지원 가능한 플랫폼과 프로그램이 다양하다.
2. 단점
   + 표준이 없어서 사용자마다 문법이 상이하다.
   + 모든 HTML의 기능을 대신하지는 못한다.

### 주의 사항

+ 마크다운의 본질은 글에 역할을 부여하는 것이다.
+ 반드시 역할에 맞는 마크다운 문법을 작성한다. 글씨를 키우고 싶다고 해서 본문에 제목의 역할을 부여하면 안된다.

<br>

## Github README Profiles
### How To do
#### Setting
- Public Repository
-  Repository name : Github User name
- File name : README.md

#### Precess
1. 홈폴더에서 `username` 폴더 생성
2. `username` 폴더를 local 저장소로 초기화
3. README.md 파일 만든 후 자기소개 작성
4. 커밋하여, 변경사항을 기록
5. github 에서도 본인의 Github `username`으로 저장소를 생성
6. 원격 저장소를 로컬 저장소와 연결
7. 변경 사항 Push
<br>
<br>

#### git/index.lock': File **exists** 에러발생
1. 다른 Git 프로세스 확인: 먼저, 동일한 저장소에서 다른 Git 프로세스가 실행 중인지 확인하십시오. 이는 진행 중인 Git 커밋, Git 병합 또는 Git에 의해 열린 편집기와 같은 것을 포함할 수 있습니다.

2. 비활성화된 Git 프로세스 종료: 다른 Git 프로세스가 실행 중이 없지만 이 오류가 계속 발생한다면 Git 프로세스가 충돌하거나 잠금을 제대로 해제하지 않았을 수 있습니다. 비활성화된 Git 프로세스를 수동으로 종료할 수 있습니다. Unix 기반 시스템에서는 ps 명령을 사용하여 프로세스 ID를 찾고, kill을 사용하여 해당 프로세스를 종료할 수 있습니다. 

   ```python
   ps aux | grep git
   # 이렇게 하면 PID와 함께 모든 Git 관련 프로세스가 나열됩니다.
   # 그런 다음 실제 프로세스 ID로 바꿔서 해당 프로세스를 종료할 수 있습니다.
   kill -9 <PID>
   ```
3. 잠금 파일 삭제: 다른 Git 프로세스가 실행 중이 아니지만 이 오류가 계속 발생하는 경우 문제를 일으키는 잠금 파일을 수동으로 삭제할 수 있습니다. Git 저장소의 루트에서 다음 명령을 실행하십시오
   ```python
   rm -f .git/index.lock
   ```

### 참고 자료

* [Markdown Guide](https://www.markdownguide.org/basic-syntax/)
* [마크다운 문법 정리](https://gist.github.com/ihoneymon/652be052a0727ad59601)
