---
layout: posts
title:  "문서분석과 한글 NLP"
excerpt: "문서분석 & KoNLPy"
date: 2024-07-07 21:34:00 +0900
categories:
  - Machine Learning
tags:
  - Document Data
  - KoNLPy

toc: true
toc_label: "Contents"
toc_sticky: true
toc_headings: "h1, h2, h3"
---
# 문서 분석

문서 군집화(Document Clustering)  
비슷한 텍스트  구성의 문서를 군집화하는 것  
텍스트 분류 기반의 문서 분류와 유사함  
차이점은 학습 데이터 세트가 필요없는 비지도 학습 기반으로 동작한다는 점이 있다.  
문서를 피처 벡터화한 데이터 세트에 군집화 알고리즘을 적용하여 수행  

문서 유사도  
- 유사도 측정 지표
 - Cosine Simlarity : 0~1 사이의 값 (1에 가까울수록 유사함)(피처 벡터 행렬은 음수값이 없으므로 음수가 나오지 않음)
   유사도 = cosX = A*B / |A| |B|
   sklearn.matrics.pairwise.cosine_similarity(X, Y=None, dense_output=True)
 - Jaccard Similarity
 - Manhattan Disatance
 - Euclidean Distance

`코사인 유사도`  
``` python
import numpy as np

def cos_similarity(v1, v2):
    dot_product = np.dot(v1, v2)
    l2_norm = (np.sqrt(sum(np.square(v1))) * np.sqrt(sum(np.square(v2))))
    similarity = dot_product / l2_norm     
    
    return similarity


from sklearn.metrics.pairwise import cosine_similarity
# feature_vect_simple : 피처 벡터
similarity_simple_pair = cosine_similarity(feature_vect_simple[0] , feature_vect_simple)

```

# 한글 NLP

한글 NLP 처리의 어려움  
- 띄어 쓰기
- 다양한 조사
- 주어/목적어가 생략되어도 의미 전달 기능
- 의성어/의태어, 높임말 등

한글 형태소 분석  
'단어로서 의미를 가지는 최소 단위'  
말뭉치를 형태소 어근 단위로 쪼개고 각 형태소에 품사 태깅(POS tagging)을 부착하는 작업
