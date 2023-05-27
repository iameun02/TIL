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
[한국어 언어모델 모델크기](https://github.com/deepseasw/nlp_model_list)
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
   https://github.com/AIRC-KETI/ke-t5-downstreams <br>
   https://huggingface.co/KETI-AIR-Downstream/long-ke-t5-base-summarization (pytorch호환모델)
   <br><br>

   - BART <br>
   https://github.com/SKT-AI/KoBART
   https://huggingface.co/spaces/gogamza/kobart-summarization/blob/main/app.py
   https://github.com/seujung/KoBART-summarization
   https://huggingface.co/gogamza/kobart-summarization
   https://huggingface.co/gogamza/kobart-base-v2/blob/main/config.json  - encoder, decoder 정보 config 파일로 확인
   https://github.com/seujung/KoBART-summarization/blob/main/train.py - downstreamed model optimizer 확인



   
>T5 (Text-To-Text Transfer Transformer)과 BART (Bidirectional and AutoRegressive Transformer)는 요약 작업에서 강력한 성능을 보여준 두 가지 인기 있는 트랜스포머 기반 모델입니다. 이러한 모델이 요약 분야에서 대표적인 이유는 다음과 같습니다:
	1.	트랜스포머 아키텍처: T5와 BART는 트랜스포머 아키텍처를 기반으로 구축되었습니다. 트랜스포머는 긴 거리의 종속성과 문맥 정보를 효과적으로 포착하는 데 능하며, 이러한 특성으로 인해 요약 작업에 적합합니다.
	2.	사전 훈련과 세부 조정: T5와 BART는 다양한 텍스트 데이터에 대해 사전 훈련되어 일반적인 언어 패턴과 표현을 학습합니다. 이 사전 훈련은 Common Crawl과 같은 대규모 데이터셋에서 수행되며, 이를 통해 이 모델들은 언어의 넓은 이해력을 습득합니다. 그런 다음 이 모델들은 요약 작업에 맞게 세부 조정되어 정확하고 일관된 요약을 생성하는 능력을 특화시킬 수 있습니다.
	3.	인코더-디코더 아키텍처: 두 모델은 인코더-디코더 아키텍처를 사용합니다. 인코더는 입력 텍스트를 처리하여 정보를 숨겨진 표현으로 인코딩하고, 디코더는 이 표현을 기반으로 요약을 생성합니다. 이 구조를 통해 모델은 입력에서 중요한 정보를 효과적으로 포착하고 간결한 요약을 생성할 수 있습니다.
	4.	마스크된 언어 모델링: T5와 BART는 사전 훈련 과정에서 마스크된 언어 모델링을 사용합니다. 여기서 입력의 일부 토큰이 마스크되고, 모델은 주변 문맥을 기반으로 해당 토큰을 예측하도록 훈련됩니다. 이 접근 방식은 모델이 누락된 정보를 채워 넣는 능력을 학습하게 하여, 핵심 콘텐츠를 담은 요약을 생성하는 데 유용합니다.
	5.	전이 학습과 세부 조정: T5와 BART는 특정한 요약 데이터셋에 대해 효과적으로 세부 조정될 수 있습니다. 이 전이 학습 접근 방식을 통해 모델은 사전 훈련된 지식을 활용하여 제한된 레이블 데이터를 기반으로 요약 작업을 잘 수행할 수 있습니다. 세부 조정을 통해 모델은 입력에 충실하면서 간결하고 일관된 요약을 생성할 수 있도록 학습할 수 있습니다.       요약하면, T5와 BART는 트랜스포머 아키텍처, 대규모 다양한 데이터셋에서의 사전 훈련, 인코더-디코더 구조, 마스크된 언어 모델링, 효과적인 전이 학습과 세부 조정 기능 등을 통해 요약 분야에서 우수한 성능을 보이고 대표적인 모델로 인정받았습니다. 이러한 요소들이 이 모델들이 다양한 맥락에서 고품질 요약을 생성할 수 있는 능력을 갖추게 합니다.

   
<br><br>

<b>2. Performance metric</b> 

   
   - ROUGE<br>
      - Recall-Oriented Understudy for Gisting Evaluation
      - Rouge1, Rouge2, Rouge-l <br>
      -  https://velog.io/@jochedda/Rouge-Score-Text-Summarization%EC%9D%98-%ED%8F%89%EA%B0%80%EC%A7%80%ED%91%9C
   - BLEU<br>
      - ngram <br>
      - Individual N-Gram Scores
           - 1-gram BLEU : weights=(1, 0, 0, 0)
           - 2-gram BLEU : weights=(0, 1, 0, 0)
           - 3-gram BLEU : weights=(0, 0, 1, 0)
           - 4-gram BLEU : weights=(0, 0, 0, 1)
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
4. 추가 학습 데이터셋 
   - 네이버 뉴스기사 IT/과학 섹션 50개<br>
      https://github.com/theeluwin/sci-news-sum-kr-50
   - AI HUB_ 요약문 및 레포트 생성 데이터_뉴스기사 10,800개 <br>
     https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100 <br><br>
   

1.  Train_Test set 분리 <br>
   검증 단계에서는 학습 모드가 아닌 평가 모드(model.eval())로 설정해야 합니다. 이를 통해 드롭아웃이나 배치 정규화와 같은 정규화 기법이 비활성화되고, 모델이 검증 데이터를 기반으로 파라미터를 업데이트하지 않습니다.
   검증 데이터의 배치를 가져와 모델에 전달한 후, 출력과 손실을 계산합니다. 손실을 평가 손실에 누적하고, 검증 데이터의 배치 수로 나누어 평균 평가 손실을 계산합니다. 이렇게 계산된 평가 손실은 업데이트하거나 모델의 성능을 모니터링하는 데 사용할 수 있습니다.
   model.train()을 호출하면 모델이 학습 모드로 전환되어 드롭아웃과 배치 정규화 레이어가 정상적으로 작동합니다. 반대로 model.eval()을 호출하면 모델이 평가 모드로 전환되어 일관된 평가를 위해 드롭아웃과 배치 정규화가 비활성화됩니다.
   학습 데이터는 모델의 파라미터를 업데이트하기 위한 역전파를 통해 사용되며, 검증 데이터는 평가 목적으로만 사용됩니다.

2. Fine-Tuning (BERTSUM) <br>
   http://ki-it.com/xml/30744/30744.pdf)

   ```python
   #Decoder
   1. length_penalty=2.0은 BERTSUM에서 사용되는 길이 패널티입니다. 길이 패널티는 생성된 요약의 길이를 조절하는 데 사용되는 하이퍼파라미터입니다. 길이 패널티는 생성된 요약의 길이에 대한 보상 또는 벌점을 조절하여 원하는 요약의 길이를 제어합니다. 값이 1.0보다 크면 길이가 긴 요약이 보다 높은 점수를 받게 되어 더 긴 요약이 생성될 가능성이 높아집니다. 반대로 값이 1.0보다 작으면 길이가 짧은 요약이 선호되어 더 짧은 요약이 생성될 가능성이 높아집니다.
   2. num_beams: Beam search에서 생성되는 후보 요약의 개수를 조정하는 파라미터입니다. 더 많은 후보 요약을 생성하면 다양성이 높아지지만 실행 시간이 늘어날 수 있습니다.
   3. max_length: 생성된 요약의 최대 길이를 제한하는 파라미터입니다. 이를 통해 원하는 요약의 길이를 조절할 수 있습니다.
   4. min_length: 생성된 요약의 최소 길이를 제한하는 파라미터입니다. 이를 통해 너무 짧은 요약이 생성되는 것을 방지할 수 있습니다.
   5. temperature: Softmax 샘플링에서 사용되는 온도(Temperature) 파라미터입니다. 값이 낮을수록 보수적인 샘플링이 이루어지고, 값이 높을수록 탐색적인 샘플링이 이루어집니다.
   6. num_return_sequences: 반환되는 요약 시퀀스의 개수를 조정하는 파라미터입니다. 여러 개의 요약 시퀀스를 생성하고 선택할 수 있습니다.

   #Optimizer
   7. adam_epsilon
   adam_epsilon는 BERT 및 다른 모델에서 Adam 옵티마이저의 수치적 안정성을 위해 사용되는 입실론 값입니다. 이 값은 업데이트 규칙의 분모에 더해져서 0으로 나누는 것을 방지하기 위한 작은 값입니다. 일반적으로 adam_epsilon의 값은 1e-8로 설정되며, 대부분의 경우에 좋은 수치적 안정성을 제공합니다.
   이 값을 필요에 맞게 조정할 수 있지만, 기본값인 1e-8은 대부분의 경우에 잘 작동하며 좋은 수치적 안정성을 제공합니다.
   adam_epsilon을 더 작은 값으로 설정하면 수치적 안정성을 더 개선할 수 있지만, 옵티마이저의 수렴 속도가 느려질 수도 있습니다. 반대로 더 큰 값으로 설정하면 안정성이 떨어질 수 있습니다. 따라서 특별한 이유가 없는 한 기본값인 1e-8을 사용하는 것이 좋습니다.


   8. weight _Decay
   weight_decay는 옵티마이저의 가중치 감쇠(weight decay)를 설정하는 매개변수입니다. 가중치 감쇠는 모델의 가중치를 제한하여 과적합을 방지하고 일반화 성능을 향상시키는 데 도움을 줍니다.
   weight_decay 값은 일반적으로 0과 1 사이의 작은 값으로 설정됩니다. 값이 0에 가까울수록 가중치 감쇠의 효과가 없어지고, 값이 1에 가까워질수록 가중치 감쇠의 효과가 강해집니다. 일반적으로 0.01 정도의 작은 값을 사용하여 가중치 감쇠를 설정합니다.
   가중치 감쇠는 모델의 복잡성을 조절하고 일반화 성능을 향상시키는 중요한 하이퍼파라미터입니다. 적절한 가중치 감쇠 값을 찾기 위해서는 실험과 검증을 통해 모델의 성능을 평가하고 비교하는 과정이 필요합니다.

   9. num_trainig_steps
   num_training_steps는 학습에 사용되는 총 스텝(step) 수입니다. 스텝은 모델의 매개변수를 업데이트하는 단위이며, 일반적으로 배치(batch) 단위로 진행됩니다. 따라서 num_training_steps는 총 배치 수에 해당합니다.
   num_training_steps 값을 설정할 때는 주어진 데이터셋을 몇 번의 에폭(epoch) 동안 반복하는지와 배치 크기(batch size)를 고려해야 합니다. 예를 들어, 데이터셋이 1000개의 샘플로 이루어져 있고 배치 크기가 10이라면, 한 에폭당 100번의 배치가 생성됩니다. 따라서 num_training_steps는 에폭 수에 배치 수를 곱한 값이 됩니다.
   이 값을 설정하는 것은 학습을 얼마나 진행할지 결정하는 중요한 하이퍼파라미터입니다. 일반적으로는 데이터의 양과 모델의 복잡성을 고려하여 충분한 학습을 수행할 수 있도록 설정해야 합니다. 적절한 num_training_steps 값을 찾기 위해서는 실험과 검증을 통해 모델의 성능과 과적합 여부를 평가하고 비교하는 과정이 필요합니다.

   10. warm_up step
   warmup_steps는 학습 초기에 적용되는 웜업 스텝의 수를 나타냅니다. 웜업 스텝은 초기 학습 단계에서 학습률을 점진적으로 증가시켜 모델이 안정적으로 학습할 수 있도록 도와줍니다.
   일반적으로 모델 초기에는 학습률을 낮게 설정하고, 웜업 스텝을 통해 점진적으로 학습률을 증가시키는 것이 좋은 결과를 얻을 수 있습니다. 웜업 스텝은 학습률을 낮추는 효과를 가지며, 초기에는 모델이 불안정하게 학습될 수 있는 문제를 완화시키고 빠른 수렴을 도모합니다.
   warmup_steps 값을 설정할 때는 데이터셋의 크기, 모델의 복잡성, 학습률의 스케줄 등을 고려해야 합니다. 보통 적절한 값은 총 학습 스텝 수에 비례하여 설정됩니다. 일반적으로 전체 학습 스텝의 약 10-20% 정도를 웜업 스텝으로 설정하는 것이 일반적이지만, 최적의 값은 실험과 검증을 통해 찾아내야 합니다.
   원하는 학습 속도와 모델의 안정성을 고려하여 warmup_steps 값을 설정하면 좋습니다. 값이 너무 작으면 모델이 불안정하게 학습될 수 있고, 값이 너무 크면 웜업 단계가 길어져 모델의 학습이 더디게 진행될 수 있습니다. 실험을 통해 최적의 warmup_steps 값을 찾아내어 모델의 성능을 향상시키는 것이 좋습니다.



   'AdamW'의 'max_steps'와 'warmup_steps'는 일반적으로 학습 프로세스에서 사용되는 매개변수입니다.
	1	'max_steps': 'max_steps'는 학습을 진행할 최대 스텝(step) 수를 의미합니다. 스텝(step)은 매개변수 업데이트를 수행하는 단위로, 일반적으로 한 번의 매개변수 업데이트는 하나의 스텝으로 간주됩니다. 'max_steps'를 설정하여 학습을 원하는 스텝 수만큼 진행할 수 있습니다. 예를 들어, 'max_steps'가 1000이라면 학습은 1000개의 스텝을 수행한 후 종료될 것입니다.
	2	'warmup_steps': 'warmup_steps'는 학습 초기에 learning rate를 조절하기 위해 사용되는 스텝 수를 의미합니다. 웜업 기간 동안 learning rate는 점진적으로 증가하며, 이를 통해 초기에 불안정한 학습을 방지하고 더 안정적인 수렴을 도모할 수 있습니다. 'warmup_steps'를 설정하여 웜업 기간을 정의할 수 있습니다. 예를 들어, 'warmup_steps'가 100이라면 처음 100개의 스텝 동안 learning rate가 증가하는 웜업 기간이 있을 것입니다.
   이러한 매개변수들은 모델 학습 과정에서 사용되는 것이므로, 구체적인 상황에 따라 적절한 값으로 설정해야 합니다. 주어진 모델과 데이터셋의 특성을 고려하여 실험하고, 성능 및 수렴 동작을 평가하여 최적의 값을 찾는 것이 좋습니다.

   ```

6. Filtering Data based on Summarized Quaility
   ```python
	
   1.토큰 빈도 기반 필터링: 요약에서 토큰의 빈도를 분석하고, 지나치게 반복되는 토큰을 식별합니다. 최대 허용 빈도에 대한 임계값을 설정하고, 이 임계값을 초과하는 요약을 필터링합니다. 이 접근 방식은 반복되거나 중복된 정보를 포함한 요약을 제거하는 데 도움이 될 수 있습니다.
   
   2.N-gram 분석: ROUGE 또는 BLEU 점수만 의존하는 대신, 요약에서 N-gram(연속된 단어의 시퀀스)을 분석합니다. 지나치게 반복되는 N-gram이나 비정상적인 패턴으로 나타나는 N-gram을 찾습니다. 이러한 패턴을 가진 데이터 포인트를 제거하여 요약의 품질을 개선할 수 있습니다.
     
   n = n-gram의 크기, n-gram은 주어진 텍스트 내에서 연속적인 n개의 항목(토큰)으로 이루어진 시퀀스를 말합니다. n의 값을 지정함으로써 분석하고자 하는 n-gram의 길이를 조절할 수 있습니다.
   예를 들어, n이 2로 설정된다면, bigram(두 개의 연속적인 토큰으로 이루어진 시퀀스)을 분석하는 것을 의미합니다. n이 3으로 설정된다면, trigram(세 개의 연속적인 토큰으로 이루어진 시퀀스)을 분석하는 것을 의미하며, 이와 같은 식으로 계속됩니다.

   n의 선택은 데이터의 특성과 캡처하고자 하는 세부 패턴의 수준에 따라 달라집니다. 더 높은 차수의 n-gram(예: trigram 또는 4-gram)을 분석하면 더 구체적인 패턴을 포착할 수 있지만, 희소한 데이터와 일반화의 어려움을 초래할 수도 있습니다. 적합한 n의 값은 과제에 따라 다를 수 있으므로, 실험을 통해 가장 적합한 값을 찾아야 할 수 있습니다.

      # Sample Code 
      from collections import Counter
      from nltk.util import ngrams

      def filter_repeated_ngrams(summaries, n, max_allowed_freq):
         filtered_summaries = []
         for summary in summaries:
            summary_ngrams = list(ngrams(summary, n))
            ngram_freq = Counter(summary_ngrams) # Counter : 주어진 n-gram 시퀀스(summary_ngrams)의 요소들의 빈도를 계산하는 파이썬 내장 함수
            if max(ngram_freq.values()) <= max_allowed_freq:
                  filtered_summaries.append(summary)
         return filtered_summaries

      
      summaries = ['This is a good summary.', 'This is a repetitive repetitive repetitive summary.', 'This is another good summary.']
      n = 2
      max_allowed_freq = 2
      filtered_summaries = filter_repeated_ngrams(summaries, n, max_allowed_freq)
      print(filtered_summaries)


	3.패턴 매칭: 낮은 품질의 요약을 나타내는 특정 패턴이나 정규 표현식을 정의합니다. 예를 들어, 반복되는 구문이나 문장에 일치하는 패턴을 정의할 수 있습니다. 이러한 패턴과 일치하는 데이터 포인트를 제거합니다.

	4.수동 검사: 낮은 품질의 요약이 의심되는 요약을 수동으로 검사합니다. 반복되거나 중복된 정보, 문법 오류 또는 낮은 요약 품질을 나타내는 기타 지표를 찾습니다. 이러한 관찰을 기반으로 요약을 필터링하는 데 도움이 되는 규칙이나 지침을 작성합니다.
   
    
   5.https://koreascience.kr/article/JAKO201820540191674.pdf
   ```




<br><br>

### <b>Memo to study</b> <br> 

1. torch.no_grad() <br>
PyTorch에서 제공하는 문맥 관리자(context manager)입니다. 이 문맥 안에서는 기울기(gradient) 계산이 비활성화됩니다. 즉, 이 문맥 안에서 수행되는 연산은 PyTorch가 기울기를 추적하지 않으며, 메모리 사용량을 크게 줄이고 연산 속도를 높일 수 있습니다.
with torch.no_grad(): 블록 안에서 수행되는 연산은 기울기가 계산되거나 저장되지 않습니다. 이는 모델의 평가 또는 추론 과정에서 유용하며, 계산된 기울기에 기초하여 모델의 매개변수를 업데이트할 필요가 없을 때 사용됩니다.
코드 조각에서 제공된 내용과 관련하여, with torch.no_grad():는 각 훈련 에폭(training epoch) 이후에 평가 단계에서 사용됩니다. 이를 통해 평가 과정에서 기울기가 계산되거나 저장되지 않으며, 일반적으로 기울기는 매개변수 업데이트를 위해 훈련 단계에서만 필요합니다.
with torch.no_grad():를 사용함으로써 기울기가 필요하지 않은 경우 불필요한 연산과 메모리 사용을 줄일 수 있습니다.
<br><br>

2. RuntimeError: CUDA error: device-side assert triggered
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
<br><br>

3. Bert vs Bart <br>

   BERT 모델의 경우, 생성된 출력을 텍스트로 디코딩하기 위해 tokenizer.decode를 사용해야 합니다. 이는 BERT 모델이 단순히 인코딩된 표현을 반환하고, 이를 텍스트로 변환하는 작업은 토크나이저의 역할입니다.
   BART 모델과 달리, BERT 모델은 디코더 스택을 가지고 있지 않으므로, 요약 또는 텍스트 생성 작업을 수행하는 데에는 추가적인 후처리 작업이 필요합니다. model.generate를 통해 생성된 출력은 토큰 ID의 시퀀스로 표현되며, 이를 tokenizer.decode를 사용하여 사람이 읽을 수 있는 텍스트로 변환합니다.
   따라서 BERT 모델을 사용할 때는 model.generate로 생성된 출력을 tokenizer.decode를 통해 텍스트로 디코딩해야 하며, 이는 BART 모델과는 조금 다른 점입니다.

   하지만 BART에서 디코딩 과정은 모델 자체에서 처리되며, 다른 모델에서와 같이 별도로 디코더에 액세스할 필요가 없습니다.
   BART에서는 디코더가 별도의 속성이나 구성 요소로 노출되지 않습니다. 대신, 디코더 기능은 BART 모델 자체에 통합되어 있습니다. BART는 인코더-디코더 아키텍처로 구성된 시퀀스 투 시퀀스 모델이며, 인코더와 디코더가 함께 훈련됩니다. 따라서 디코더를 따로 액세스할 필요가 없습니다. BART 모델에서 디코더 구성 요소에 직접 액세스하거나 조작하려고 할 때 'decoder' 속성이 없다는 것을 나타내는 오류가 발생됩니다. BART를 사용하여 요약 생성이나 디코딩을 수행하려면 BART 모델 자체의 generate 메서드를 사용할 수 있습니다.


4. eos_token_id <br>
eos_token_id=1는 BERTSUM에서 사용되는 특수 토큰인 "End of Sentence" (EOS) 토큰을 나타냅니다. EOS 토큰은 요약 또는 문장의 끝을 나타내는 역할을 합니다. BERTSUM에서는 요약 생성 시 요약의 끝을 표시하기 위해 EOS 토큰을 사용합니다.
eos_token_id=1의 값이 1인 이유는 토크나이저가 사용하는 특정 토큰 인덱스에 해당하기 때문입니다. 각 토큰은 고유한 인덱스를 가지고 있으며, 이 코드에서는 EOS 토큰의 인덱스를 1로 설정했습니다. 실제로 사용하는 토크나이저에 따라서 EOS 토큰의 인덱스는 다를 수 있습니다.


5. scheduler = get_linear_schedule_with_warmup(optimizer, num_warmup_steps=warmup_steps, num_training_steps=max_steps) <br>
get_linear_schedule_with_warmup 함수는 사전에 정의된 학습률 스케줄러를 반환하는 함수입니다. 
학습률을 직접 변경하는 것이 아니라, 이 함수를 사용하여 학습률 스케줄러를 생성하고 이를 옵티마이저와 함께 사용하여 학습률을 조정합니다.
get_linear_schedule_with_warmup 함수는 optimizer, num_warmup_steps, num_training_steps를 인자로 받습니다. optimizer는 최적화 알고리즘으로 초기화된 모델의 옵티마이저입니다. num_warmup_steps는 워밍업 단계 수로, 학습률을 선형적으로 증가시키는 단계의 수를 나타냅니다. num_training_steps는 총 학습 단계 수를 나타내며, 이는 모델을 훈련시키는 데 필요한 전체 배치의 수를 의미합니다. <br>
get_linear_schedule_with_warmup 함수가 반환하는 학습률 스케줄러를 사용하면, 옵티마이저의 학습률은 워밍업 단계에서 선형적으로 증가한 후, 훈련 단계에서 선형적으로 감소합니다. 따라서, 학습률을 조정하기 위해서는 num_warmup_steps와 num_training_steps를 적절하게 설정해주어야 합니다. 이를 통해 원하는 학습률 스케줄을 구현할 수 있습니다.<br>
get_linear_schedule_with_warmup 함수에서 초기 학습률은 옵티마이저를 초기화할 때 설정한 학습률입니다. get_linear_schedule_with_warmup 함수는 지정된 워밍업 단계와 훈련 단계에 따라 자동으로 학습률을 조절합니다.
워밍업 단계에서 학습률은 초기 학습률에서 시작하여 지정된 워밍업 단계 수만큼 선형적으로 증가합니다. 워밍업 단계 이후에는 학습률은 선형적으로 감소하며 남은 훈련 단계에 비례합니다.
따라서, 시작 학습률은 설정한 초기 학습률이며, 워밍업 단계와 훈련 단계에 따라 조정되어 원하는 학습률 스케줄을 달성하게 됩니다.<br>


6. '#' of head <br>

   "# of heads"라는 용어는 모델의 헤드 개수를 일반적으로 나타냅니다.
   자연어 처리(NLP) 및 트랜스포머 기반 모델에서, 어텐션 헤드는 모델이 동시에 입력 시퀀스의 다른 부분에 집중할 수 있도록 돕는 구성 요소입니다. 각 어텐션 헤드는 입력의 다른 측면에 주의를 기울이고 다른 표현을 학습하여 모델이 다양한 관계와 종속성을 포착할 수 있게 합니다.
   모델에서의 헤드 개수는 동시에 사용되는 병렬 어텐션 메커니즘의 수를 결정합니다. 헤드의 수가 높을수록 모델은 더 세밀한 패턴과 종속성을 포착할 수 있는 능력을ß 갖추게 됩니다. 그러나 헤드의 수를 늘릴수록 모델의 계산 복잡성과 메모리 요구 사항도 증가합니다.
   요약하면, 모델의 "# of heads"라고 할 때, 일반적으로 모델의 어텐션 메커니즘에서 사용되는 어텐션 헤드의 개수를 나타냅니다.

7. ffn_dim <br>

   "ffn_dim"은 transformer 기반 모델에서 Feed-Forward Network dimension 또는 Feed-Forward dimension을 의미합니다.
   Transformer 아키텍처에서, feed-forward network(FFN)은 다중 헤드 셀프 어텐션 레이어 뒤에 위치한 구성 요소입니다. 이는 두 개의 선형 레이어와 그 사이에 비선형 활성화 함수를 포함합니다. Feed-forward network의 목적은 어텐션 메커니즘으로부터 얻은 표현에 비선형 변환을 적용하는 것입니다.
   "ffn_dim"은 feed-forward network의 은닉층의 차원 또는 크기를 나타냅니다. 이는 은닉층의 뉴런이나 유닛의 개수를 결정합니다. "ffn_dim"의 값이 높을수록 더 많은 매개변수를 가진 더 큰 은닉층을 의미하며, 이는 모델이 입력과 출력 표현 사이의 더 복잡한 매핑을 학습할 수 있도록 합니다.
   "ffn_dim"의 선택은 모델 설계와 훈련 과정에서 조정할 수 있는 하이퍼파라미터입니다. 모델의 용량과 계산 효율성 사이의 균형을 맞추는 것이 중요합니다. 차원을 증가시키면 보다 강력하지만 계산 비용이 더 많이 드는 모델이 될 수 있기 때문입니다.


8. Hidden_dim <br>
   "hidden_dim"은 모델에서 사용되는 숨겨진(hidden) 차원 또는 크기를 의미합니다.
   모델의 "hidden_dim"은 일반적으로 각 레이어의 표현(representation)의 차원을 나타냅니다. 이는 모델이 내부적으로 사용하는 숨겨진 상태, 임베딩, 또는 특성 벡터의 차원을 결정합니다.
   "hidden_dim"의 크기는 모델의 용량과 표현 능력을 결정하는 중요한 요소입니다. 더 큰 "hidden_dim"은 모델이 더 복잡한 패턴과 표현을 학습할 수 있는 능력을 높일 수 있습니다. 그러나 큰 "hidden_dim"은 더 많은 파라미터와 계산 비용을 필요로하므로 모델의 훈련과 실행에 더 많은 리소스가 필요합니다.
   "hidden_dim"의 선택은 모델 설계 및 문제의 복잡성에 따라 달라질 수 있습니다. 적절한 "hidden_dim"을 선택하는 것은 모델의 표현 능력과 계산 효율성 사이의 균형을 유지하는 데 중요합니다.


9. Adam vs Adamw <br>
   ADAM (Adaptive Moment Estimation)과 AdamW는 신경망을 훈련시키는 데 일반적으로 사용되는 최적화 알고리즘입니다. <br>
   두 알고리즘은 유사한 점이 있지만, 다음과 같은 중요한 차이점이 있습니다: <br>
      1.	Adam <br>
             - Adam은 AdaGrad와 RMSprop과 같은 적응형 학습률 방법과 모멘텀 방법의 이점을 결합한 최적화 알고리즘입니다.
             - Adam은 각 매개변수에 대한 적응적인 학습률을 유지하며, 과거 기울기와 기울기 제곱의 지수적으로 감소하는 이동 평균을 사용하여 매개변수를 업데이트합니다.
             - Adam은 첫 번째 및 두 번째 모멘트의 추정값 초기화 편향을 처리하기 위해 편향 보정 항을 포함합니다.
             - Adam의 학습률은 전통적인 확률적 경사 하강법(SGD)에 비해 하이퍼파라미터 선택에 대해 일반적으로 덜 민감합니다.

      2.	AdamW <br>
            -	AdamW는 Adam의 확장으로 가중치 감쇠 문제를 해결합니다. 가중치 감쇠 문제는 신경망의 가중치가 훈련 중에 과도하게 벌점화되는 경우 발생합니다.
            -	AdamW는 가중치 감쇠를 손실 함수의 L2 정규화 항에 의존하는 것이 아닌 매개변수 업데이트에 직접 추가합니다.
            -	AdamW의 이러한 수정은 가중치 감쇠가 적응적인 학습률 추정 과정에 미치는 영향을 완화하여 더 나은 수렴 및 일반화를 가능하게 합니다.
   
   <br>
   요약하면, Adam과 AdamW의 주요 차이점은 가중치 감쇠가 최적화 과정에 어떻게 통합되는지에 있습니다. AdamW는 매개변수 업데이트에 가중치 감쇠를 명시적으로 처리하여 Adam보다 더 나은 최적화 성능을 제공할 수 있습니다, 특히 적응적 학습률 방법과 함께 가중치 감쇠를 사용하는 경우에 유용합니다.

10. Optimizer
사전 훈련된 모델은 일반적으로 최적화기(optimizer)를 포함하지 않습니다. 사전 훈련된 모델은 학습된 파라미터를 포함하고 있지만, 학습 과정에서 사용된 최적화기는 모델과 함께 저장되지 않습니다.
사전 훈련된 모델을 세부 조정하거나 특정 작업을 위해 훈련할 때, 사용자는 별도로 최적화기를 정의하고 초기화해야 합니다. 최적화기는 훈련 과정에서 계산된 그래디언트를 기반으로 모델의 파라미터를 업데이트하는 역할을 담당합니다.

	1	Adam: Adam은 AdaGrad와 RMSProp과 같은 적응형 그래디언트 알고리즘의 장점을 결합한 인기 있는 최적화기입니다. Adam은 각 매개변수의 학습률을 유지하고 그래디언트의 일차 및 이차 모멘트에 기반하여 학습률을 조정합니다.
	2	AdamW: AdamW는 최적화 과정에서 가중치 감소(weight decay)를 포함하는 Adam의 변형입니다. 가중치 감소는 모델의 가중치를 정규화하여 과적합을 방지하는 데 도움을 줍니다.
	3	Adafactor: Adafactor는 Transformer 모델에서 자주 사용되는 다른 최적화기입니다. Adafactor는 Adam의 적응형 방법과 SGD(확률적 경사 하강법)의 메모리 효율성을 결합하여 인자화된 이차 모멘트 추정기를 사용합니다.

11. torch.optim.Adam vs transformers의 Adam

   torch.optim.Adam과 transformers의 Adam은 동일하지 않습니다.
   torch.optim.Adam은 PyTorch에서 제공하는 일반적인 목적의 내장 최적화기로, 딥 러닝 모델을 훈련하는 데 사용됩니다.
   반면에 transformers의 Adam은 특히 자연어 처리(NLP) 작업을 위해 설계된 Adam 최적화기의 사용자 지정 구현입니다. 특히 BERT, GPT 및 Hugging Face의 transformers 라이브러리에서 제공되는 기타 모델과 같은 transformer 기반 모델을 훈련하는 데 사용됩니다.
   두 최적화기는 Adam 알고리즘의 기본 원리를 공유하지만, 구현 세부 사항과 기능은 다를 수 있습니다. transformers의 Adam 최적화기는 NLP 작업과 transformer 아키텍처에 맞게 추가 기능과 수정 사항을 포함할 수 있습니다. 이에는 그래디언트 클리핑, 가중치 감쇠(weight decay), 학습률 스케줄 등이 포함될 수 있으며, 이러한 기능은 NLP 분야에서 흔히 사용됩니다.
   transformers 라이브러리에서 transformer 기반 모델을 사용하는 경우, NLP 작업에 특화된 transformers의 Adam 최적화기를 사용하는 것이 좋습니다. 이를 통해 더 나은 호환성과 NLP 작업을 위해 제공되는 특별한 기능을 활용할 수 있습니다. 일반적인 NLP 영역 이외의 일반적인 딥 러닝 작업에는 torch.optim.Adam을 사용할 수 있습니다.



<br><br>

#### 기타


추가기능 아이디어
https://github.com/lee040118/summarization_model_serving


파인튜닝 참고자료
https://towardsdatascience.com/fine-tuning-the-bart-large-model-for-text-summarization-3c69e4c04582



<디비실행 명령어>
docker start mariadb
docker ps -a
docker ps -a 명령어로 실행중인 목록 확인


