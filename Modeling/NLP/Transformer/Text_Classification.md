# Text Classification
<b>감정분류</b> <br>
BERT모델을 훈련시키기 위해 체크포인트만 변경 <br>
체크포인트 : 트랜스포머 아키텍처로 로드되는 일련의 가중치 <br>
<b>Pipe Line</b>
1. 데이터셋 : 데이터셋 로드하고 전처리하기
2. 토크나이저 : 입력텍스트를 토큰화하기
3. 모델을 로드, 훈련, 추론하기
4. 데이터셋 : 측정도구를 로드하고 모델을 평가하기 
<br><br>

### 1. Data Set

트윗이 주어지면 분노(Anger), 혐오(Disgust), 두려움(Fear), 기쁨(joy), 슬픔(Sadness), 놀람(Surprise)의 여섯개 감정으로 분류하는 모델을 훈련시킴. <br>

데이터 출처 : https://oreil.ly/959YT <br>
list_datasets()함수를 활용하여 데이터셋 목록 출력 <br>

허깅페이스 데이터셋은 아파치 애로우(Apache Arrow)에 기반한다. <br>
아파치 애로우는 기본 파이썬보다 훨씬 더 메모리 효율적인 열기반 포맷을 사용한다.<br>


```python

#!pip install datasets

# 1. 허깅페이스 제공 데이터셋 리스트 조회
from datasets import list_datasets

all_datasets = list_datasets()
print(f'현재 허브에는 {len(all_datasets)} 개의 데이터셋이 있습니다.')
print(f'처음 10개 데이터셋 : {all_datasets[:10]}')

#2. 데이터셋 로드 및 확인
from datasets import load_dataset

emotions = load_dataset('emotion')
emotions
emotions['train']['text'][0]


#3. 새로운 Dataset객체 만들기 및 확인
train_ds = emotions['train']
train_ds
len(train_ds)
train_ds[0]
train_ds.column_names
print(train_ds.features)
print(train_ds[:5])
train_ds[:5]
train_ds['text'][:5]
```
포멧에 따른 데이터셋 로딩 방법 <br>

csv <br>
load_dataset('csv', data_files = 'my_files.csv')

text <br>
load_dataset('text', data_files = 'my_files.txt')

json <br>
load_dataset('json', data_files = 'my_files.jsonl) 

### 2. Text to Token

### 3. Classification Training

