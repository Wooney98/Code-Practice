## 첫 제출 (https://github.com/Wooney98/Code-Practice/blob/main/comp/dacon%26kaggle/%EC%9B%94%EA%B0%84%20%EB%8D%B0%EC%9D%B4%EC%BD%98%20%EB%B0%9C%ED%99%94%EC%9E%90%EC%9D%98%20%EA%B0%90%EC%A0%95%EC%9D%B8%EC%8B%9D%20AI%20%EA%B2%BD%EC%A7%84%EB%8C%80%ED%9A%8C/roberta_base_5Fold.ipynb)
  - public score : 0.38558
  - 형태소 분석기인 kiwi는 한국어에 특화된 분석기이다. nltk 등 영문에 특화된 분석기를 사용해야함.
  - 전처리과정중 Speaker와 Dialogue 컬럼을 어떻게 사용해야할지 고민해봐야할듯!
    - 무작정 라벨링을 하는게 맞을까? 아니면 drop하는게 나을까.. 
    - AutoGluon 이라는 모델도 좋아보임!
  - 영문을 제외한 특수문자(! , . ?)는 필요할것같다. 문장 길이가 짧은 구문들이 꽤나 있기에 포함하는게 좋을듯!(대부분 `중립`이다.)
