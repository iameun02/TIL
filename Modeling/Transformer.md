# Transformer


#### <b>Transformer Introduction</b>
- 2017년 구글에서 시퀀스 모델링을 위한 새로운 신경망 아키텍처 '트랜스모퍼' 개발
- 기계 번역 작업의 품질과 훈련 비용 면에서 RNN(순환 신경망)을 능가
- 전이학습 방법인 ULMFiT가 매우크고 다양한 말뭉치에서 LSTM 신경망을 훈련해 <br>
  매우 적은 양의 레이블링된 데이터로도 최고수준의 텍스트 분류모델을 만들어냄
- 오늘날 가장 유명한 두 트랜스포머 'GPT' 와 'BERT' 의 촉매가 되었음
- 트랜스포머 아키텍처와 비지도학습을 결합해 작업에 특화된 모델을 밑바닥훈련의 필요성을 제거

<br><br>

##### <b>Transformer Timeline</b> <br>
```python
                                             RoBERTa   XLM-R        DeBERTa     
      transformer    ULMFIT  GPT  BERT    GPT-2   DistilBERT    GPT-3   T5    GPT-Neo  GPT-J 
           ▼            ▼     ▼    ▼        ▼     ▼  ▼ ▼          ▼   ▼ ▼        ▼      ▼ 
2017---------------2018---------------2019---------------2020---------------2021---------------
```


#### <b>Transformer Architechure</b>
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