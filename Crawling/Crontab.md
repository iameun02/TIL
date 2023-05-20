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