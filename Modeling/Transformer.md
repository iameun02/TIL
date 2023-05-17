# Transformer


### <b>Transformer Introduction</b>
- 2017년 구글에서 시퀀스 모델링을 위한 새로운 신경망 아키텍처 '트랜스모퍼' 개발
- 기계 번역 작업의 품질과 훈련 비용 면에서 RNN(순환 신경망)을 능가
- 전이학습 방법인 ULMFiT가 매우크고 다양한 말뭉치에서 LSTM 신경망을 훈련해 <br>
  매우 적은 양의 레이블링된 데이터로도 최고수준의 텍스트 분류모델을 만들어냄
- 오늘날 가장 유명한 두 트랜스포머 'GPT' 와 'BERT' 의 촉매가 되었음
- 트랜스포머 아키텍처와 비지도학습을 결합해 작업에 특화된 모델을 밑바닥훈련의 필요성을 제거

<br>

#### <b>Transformer Timeline</b> <br>
```python
                                             RoBERTa   XLM-R        DeBERTa     
      transformer    ULMFIT  GPT  BERT    GPT-2   DistilBERT    GPT-3   T5    GPT-Neo  GPT-J 
           ▼            ▼     ▼    ▼        ▼     ▼  ▼ ▼          ▼   ▼ ▼        ▼      ▼ 
2017---------------2018---------------2019---------------2020---------------2021---------------
```
[한국어 언어모델 timeline](https://www.letr.ai/blog/tech-20221124)
<br><br>

### <b>Transformer Architechure</b>
1. Encoder
   - BERT - DistilBERT
   - RoBERta
   - XLM - XLM-R
   - ALBERT
   - ELECTRA
   - DeBERTa

<br>
  
2. Decoder
   - GPT
   - GPT-2 - CTRL
   - GPT-3
   - GPT-Neo - GPT-J

<br>

3. Encoder + Decoder
   - T5
   - BART
   - M2M-100
   - BigBird
  
<br><br>

### <b>Hugging Face</b>
매우 다양한 트랜스포머 모델에 표준화된 인터페이스를 제공하여 전이학습시 사용용이

1. Hub : 사전 훈련된 모델 가중치, 데이터셋, 평가지표를 위한 스크립트 등 제공
2. Library : 코드제공

<br><br>
### <b>Transformer_Summarization</b> <br> 
<b>1. Representative Model</b> <br>

   - T5 <br>
   https://github.com/AIRC-KETI/ke-t5 <br>
   https://github.com/AIRC-KETI/ke-t5-downstreams
   <br><br>

   - BART <br>
   https://github.com/SKT-AI/KoBART
   
   <br><br>

<b>2. Performance metric</b> 

   
   - ROUGE<br>
      - Recall-Oriented Understudy for Gisting Evaluation
      - Rouge1, Rouge2, Rouge-l <br>
      -  https://velog.io/@jochedda/Rouge-Score-Text-Summarization%EC%9D%98-%ED%8F%89%EA%B0%80%EC%A7%80%ED%91%9C
   - BLEU<br>
      - ngram <br>
      - https://ko.linux-console.net/?p=6105#gsc.tab=0
      - http://incredible.ai/nlp/2020/02/29/BLEU/
   - RDASS<br>

<br><br>

<b>3. Fine Tuning</b> <br>

   - https://colab.research.google.com/drive/1IHMJHPwoOvAKH7NvyzPjm9cZRSVbLeYR?usp=sharing

1. Trainable Layer 확인

   ```python

   for name, param in model.named_parameters():
      if param.requires_grad:
         print(name, "is trainable")
      else:
         print(name, "is not trainable")

   ```


   requires_grad 속성은 파라미터가 gradient 계산에 사용되는지 여부를 나타냅니다. 만약 requires_grad가 True인 경우에는 해당 파라미터가 trainable하다는 것을 의미합니다. <br><br>

2. Model Summary 확인
- Hugging Face Transformers 라이브러리의 summary 함수
   
   ```python
   from transformers import pipeline

   # 모델의 요약(summary)을 확인
   summary = pipeline('summarization', model=model, tokenizer=model.tokenizer)
   result = summary("This is a test sentence that we want to summarize.")
   print(result[0]['summary_text'])
   ```

3. Fine-tuning process
   ```python
   1. 데이터셋 로드: 학습에 사용할 데이터셋을 로드합니다. 
   2. 토크나이저 정의: T5 모델에 맞는 토크나이저를 정의합니다. 
   3. 모델 정의: transformers 라이브러리에서 T5 모델을 불러온 후, 필요에 따라 추가 레이어를 붙여 fine-tuning을 위한 커스터마이징을 할 수 있습니다.
   4. 학습 파라미터 설정: 학습에 필요한 하이퍼파라미터를 설정합니다. (예: learning rate, batch size, epoch 등)
   5. 데이터 전처리: 데이터셋에 포함된 텍스트 데이터를 토큰화하고, 입력과 출력 시퀀스로 분리합니다. 이때, 입력과 출력 시퀀스는 모두 문장으로 이루어져 있어야 합니다. 
   6. 데이터 로더 생성: 데이터 전처리된 데이터셋을 DataLoader로 변환합니다. 
   7. 손실 함수 정의: fine-tuning을 위한 손실 함수를 정의합니다. 
   8. 옵티마이저 정의: fine-tuning을 위한 옵티마이저를 정의합니다.
   9. 학습: DataLoader에서 배치 단위로 데이터를 가져와 모델에 입력하고, 손실 함수와 옵티마이저를 이용해 학습을 진행합니다. 
   10. 모델 저장: 학습이 끝난 모델을 저장합니다.
   ```
4. 추가 학습 데이터셋 (기사 50개)<br>
   https://github.com/theeluwin/sci-news-sum-kr-50

<br><br>

### <b>Memo to study</b> <br> 

1. torch.no_grad() <br>
PyTorch에서 제공하는 문맥 관리자(context manager)입니다. 이 문맥 안에서는 기울기(gradient) 계산이 비활성화됩니다. 즉, 이 문맥 안에서 수행되는 연산은 PyTorch가 기울기를 추적하지 않으며, 메모리 사용량을 크게 줄이고 연산 속도를 높일 수 있습니다.
with torch.no_grad(): 블록 안에서 수행되는 연산은 기울기가 계산되거나 저장되지 않습니다. 이는 모델의 평가 또는 추론 과정에서 유용하며, 계산된 기울기에 기초하여 모델의 매개변수를 업데이트할 필요가 없을 때 사용됩니다.
코드 조각에서 제공된 내용과 관련하여, with torch.no_grad():는 각 훈련 에폭(training epoch) 이후에 평가 단계에서 사용됩니다. 이를 통해 평가 과정에서 기울기가 계산되거나 저장되지 않으며, 일반적으로 기울기는 매개변수 업데이트를 위해 훈련 단계에서만 필요합니다.
with torch.no_grad():를 사용함으로써 기울기가 필요하지 않은 경우 불필요한 연산과 메모리 사용을 줄일 수 있습니다.
<br><br>

1. RuntimeError: CUDA error: device-side assert triggered
CUDA kernel errors might be asynchronously reported at some other API call,so the stacktrace below might be incorrect.
For debugging consider passing CUDA_LAUNCH_BLOCKING=1.
해결 방법

   ```python
   1. 문자길이 제한
   max_length = 512  # 최대 토큰 수

   # 입력 문장 길이 제한
   if len(input_ids) > max_length:
      input_ids = input_ids[:max_length]


   2. 문장 압축
   import re

   # 불필요한 공백 및 구두점 제거
   text = re.sub(r'\s+', ' ', text)  # 공백 제거
   text = re.sub(r'[^\w\s]', '', text)  # 구두점 제거

   # 단어 축약
   # 예: "can't"를 "cannot"으로 변경
   text = re.sub(r"can't", "cannot", text)


   3. 문장 요약
   from transformers import pipeline

   # 문장 요약 모델 초기화
   summarizer = pipeline("summarization")

   # 입력 문장 요약
   summary = summarizer(text, max_length=100, min_length=30, num_beams=4)


   4. 데이터 필터링
   min_length = 10  # 최소 문장 길이

   # 데이터 필터링
   filtered_data = [data for data in dataset if len(data) >= min_length]

   5. 데이터 샘플링
   import random
   sample_size = 100  # 샘플 크기

   # 데이터 무작위 샘플링
   sampled_data = random.sample(dataset, sample_size)
   ```

