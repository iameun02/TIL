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
#### Data Load
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

```python
#example
dataset_url = 'https://www.dropbox.com"

emotions_remote = load_dataset('csv', data_files = dataset_url,
sep = ';', names = ['text','label'])
```
#### Data Preprocessing
1. from Dataset to DataFrame

    ```python
    import pandas as pd


    emotions.set_format(type= 'pandas')
    df = emotions['train'][:]
    df
    ```
    ClassLabel 클래스 객체에는 int2str(), str2int()메서드가 있음
    ```python
    df['label_name'] = emotions['train'].features['label'].int2str(df['label'])
    ```

2. 클래스 분포 살펴보기 <br>
   샘플링 전략을 사용할때는 일반적으로 훈련세트에만 사용하기 때문에
   train/test 분할 전에는 샘플링 전략을 적용하지 않음
   ```python
   import matplotlib.pyplot as plt
   df['label_name'].value_counts(ascending=True).plot.barh()
   ```

3. 트윗 길이 확인<br>
   트랜스포머 모델은 최대 문맥길이(Maximum context size)라는 최대 입력 시퀀스 길이가 존재 <br>
   텍스트가 모델의 문맥 크기보다 길면 잘라내야 하는데, 잘린텍스트에 중요한 정보가 있을 경우 성능에 손실이 생길 수 있음.
    ```python
    df['Words Per Tweet'] = df['text'].str.split().apply(len)
    df.boxplot('Words Per Tweet', by = 'label_name' ,grid = False,
           showfliers = False, color = 'black')
    ```
4. 데이터셋의 출력 포맷 초기화 <br>
   ```python
   emotions.reset_format()
   ```

### 2. Text to Token (정수인코딩)
트랜스포머 모델은 원시문자열을 입력으로 받지 못하기 때문에 텍스타가 토큰화되어, 수치벡터로 인코딩필요
토큰화 : 문자열을 기본단위로 분할하는 단계, 단어를 부분단위로 나누기 위한 최적분할은 일반적으로 말뭉치에서 학습됨. 문자토큰화와, 단어토큰화는 극단적인 토큰화 방식 중 하나. 하지만 단어같은 언어구조를 주어진 데이터내에서 학습해야한다는 큰 단점으로 문자수준의 토큰화는 거의 사용하지 않음. 대신 텍스트의 일부구조가 유지되는 단어 토큰화를 사용 <br>
    1) 문자토큰화
   
    text ='Tokenizing text is a core task of NLP'
    tokenized_text= list(text)
    tokenized_text

    token_idx = {ch : idx for idx, ch in enumerate(sorted(set(tokenized_text)))}  

    input_ids = [token_idx[token] for token in tokenized_text]
    input_ids
    
    2) 단어토큰화

### 3. Make it Tensor and One-hot encoding
    1) 문자토큰화
   
    import torch
    import torch.nn.functional as F

    input_ids= torch.tensor(input_ids)
    input_ids

    onehotencoding = F.one_hot(input_ids, num_classes= len(token_idx))
    onehotencoding.shape

    print(f'token : {tokenized_text[0]}')
    print(f'tensor idx : {input_ids[0]}')
    print(f'onehot encoding :  {onehotencoding[0]}')

   2) 단어토큰화

### 4. Classification Training

