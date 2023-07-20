# Tokenizer


1. 전통적인 통계 방식 : 단어의 빈도수로 Bow(Bag of Words) > 순서를 유지못함, N-gram사용시 피처수가 기하급수적으로 증가 <br>
--> TF-IDF(전체문서에서 공통으로 사용되는 단어는 낮음, 특정문서에서 자주사용되는 단어는 중요도 가 높아 높음) 사용 <br>
Scikit-Learn의 TfidfVectorizer Method 사용 <br>
2. 현재 방식 : Vocabrary 사전화 하여 One-hot encoding 후 (나머지, unk)
