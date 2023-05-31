```python

from wordcloud import WordCloud
import matplotlib.pyplot as plt
from collections import Counter
from konlpy.tag import Okt
from PIL import Image
import numpy as np
import pandas as pd
import konlpy


df = pd.read_csv('News_s20230531.csv',dtype= {'press_id': 'object', 'section_id': 'object'})
kkma = konlpy.tag.Kkma() #형태소 분석기 꼬꼬마(Kkma)

nouns = df['content'].apply(kkma.nouns)
nouns
nouns = nouns.explode()
nouns

df_word = pd.DataFrame({'word' : nouns})
df_word['count'] = df_word['word'].str.len()
df_word = df_word.query('count >= 2')
df_word

df_word = df_word.groupby('word', as_index = False).count().sort_values('count', ascending = False)
df_word

dic_word = df_word.set_index('word').to_dict()['count']
dic_word

wc = WordCloud(random_state = 123, font_path = '/usr/share/fonts/truetype.ttf', width = 400,height = 400, background_color = 'white')

img_wordcloud = wc.generate_from_frequencies(dic_word)

plt.figure(figsize = (10, 10)) # 크기 지정하기
plt.axis('off') # 축 없애기
#plt.imshow(img_wordcloud) # 결과 보여주기
```