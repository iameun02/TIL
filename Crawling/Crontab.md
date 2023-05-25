# Crontab

[참고사이트1](https://velog.io/@svstar94/AWS-EC2-python-%EC%A3%BC%EA%B8%B0%EC%A0%81%EC%9C%BC%EB%A1%9C-%EC%8B%A4%ED%96%89-Cron-%EC%9E%A1-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%AC)


[참고사이트2](https://jeon2devel.tistory.com/126)

<br>

1. 시간설정 <br>
    crontab.guru 사이트 이용 <br>

2. 기본 명령어

    ```python
    1. 크론탭 편집
        crontab -e

    2. 크론탭 작업 내용 확인
        crontab -l

    3. 크론탭 삭제 (삭제시 전체 작업 삭제)
        crontab -r
    
    4. 크론탭 시작
        service cron start

    5. 크론탭 중지
        service cron stop  

    6. 작동확인
        service cron status 
    
    7. 크론탭 재시작
        service cron restart
    ```
3. .ipynb 파일을 .py파일로 변환후 저장 <br>
    ```python
    jupyter nbconvert --to script test123.ipynb && python test123.py
    ```

#### 예시

> tty 명령어를 통해 현재 세션 확인 후, 해당 세션으로 출력을 리디렉션 하여 보여주는 명령어

26 16 * * * jupyter nbconvert --to script 경로/파일명.ipynb && python3 경로/파일명.py >> 세션 


26 16 * * * echo -e "hello" > 세션정보

26 16 * * * python3 경로/파일명.py > 세션정보


### 참고

1. 목표 경로에 패키지 설치하고 싶을떄 <br>
    pip install beautifulsoup4 --target=/경로/ <br>
2. 패키지 설치 위치 확인 <br> 
   pip show beautifulsoup4 <br>
3. python2,3 이 둘다환경에 설치되어있고, 패키지 설치시 파이썬2로 설치될 경우<br>
   pip uninstall 패키지명으로 파이썬 2에 설치된 패키지를 다시 지우고,<br>
   pip3으로 installation 다시설치 , 실행시에는 python3로 실행<br>
   pip3 install beautifulsoup4<br>
<br><br>

<b>최종실행코드</b><br>
/파이썬절대경로/python3 절대경로/파일명.py <br>


<br><br>
내일 확인할것
- 1406, "Data too long for column 'writer' at row 290")
- 데이터 삭제 코드
<br><br>

4. DB 저장 _ df.to_sql 사용

    df.to_sql 각 매개변수에 대한 설명
        •	index=False: 이 매개변수는 DataFrame의 인덱스를 데이터베이스 테이블에 별도의 열로 포함하지 않도록 합니다.
        •	name=table_name: table_name은 데이터베이스에서 테이블에 할당할 이름을 나타냅니다.
        •	con=engine: engine 매개변수는 데이터베이스 연결 또는 엔진 객체를 지정하여 데이터베이스에 연결하는 데 사용됩니다.
        •	if_exists='append': 이 매개변수는 테이블이 이미 데이터베이스에 존재하는 경우 어떻게 처리할지를 결정합니다. 'append'는 테이블이 이미 존재하는 경우 새 데이터를 추가하도록 지정합니다. 'replace'는 테이블을 삭제하고 새 데이터로 새로 만들고, 'fail'은 테이블이 이미 존재하는 경우 오류를 발생시킵니다.
        method과 chunksize 매개변수는 대용량 DataFrame 작업에 대한 최적화를 위해 사용될 수 있습니다. method='multi'는 병렬로 insert 문을 실행하도록 합니다. chunksize는 각 배치에 삽입할 행의 수를 지정합니다.

