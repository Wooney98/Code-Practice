# 첫 시도
- roberta_base_5Fold.ipynb
  - public score : 0.38558
- 형태소 분석기인 kiwi는 한국어에 특화된 분석기이다. nltk 등 영문에 특화된 분석기를 사용해야함.
- 전처리과정중 Speaker와 Dialogue 컬럼을 어떻게 사용해야할지 고민해봐야할듯!
  - 무작정 라벨링을 하는게 맞을까? 아니면 drop하는게 나을까.. 
  - AutoGluon 이라는 모델도 좋아보임!
- 영문을 제외한 특수문자(! , . ?)는 필요할것같다. 문장 길이가 짧은 구문들이 꽤나 있기에 포함하는게 좋을듯!(대부분 `중립`이다.)

# 하이퍼파라미터 설정
- EPOCHS = 10 # 반복 횟수
- LR = 1e-5 # 학습률
- BS = 8 # 배치 크기
- SEED = 41 # 랜덤 시드

# 1.
- Utterance 컬럼의 텍스트 데이터만을 이용하여 학습 및 추론
- 3개의 사전학습 모델을 이용하여 학습 및 추론
- 3개의 사전학습 모델에서 나온 예측 확률을 csv로 저장하여 하드보팅으로 앙상블 하여 정답 예측 파일 생성
- 저장된 예측 확률을 앙상블하여 제출파일을 생성하는 ipynb
  - Inference_Voting.ipynb
  
# 2.
- 학습에 사용한 사전학습 모델
  - bert-base-uncased
  - tae898/emoberta-base
  - bert-large-uncased
- 각 사전학습 모델  last hidden states에서 cls 토큰의 hidden states를 사용하여 linear layer 통과 후 예측
- Optimizer는 Adam 사용
- 배치 사이즈는 8 or 16
- Learning rate는 2e-05

# 3.
- 앙상블
  - 하드보팅(Hard Voting)
  
# 아쉬운점.
- 여러 사전모델을 사용하지 않았음. -> 시간 부족
- 스페인어 / 프랑스어를 대체할 방법을 알지 못했음. -> 경험 부족

# 4. 데이터 증강 방식
- 1. Augmentation - RI(Random Insertion): 감탄사와 의성어를 문장 내에 추가하는 방식
ex) 나는 자전거 타는 것을 좋아한다. -> 와! 나는 자전거 타는 것을 좋아한다.
- 2. Back-Translation
원본) 나는 자전거 타는 것을 좋아한다. 

한국어 -> 프랑스어) J'aime faire du vélo. 

프랑스어 -> 한국어) 저는 자전거 타는 것을 좋아해요.
위의 예와 같이 특정 문장을 다른 언어로 번역한 후 다시 한국어로 번역하여 의미는 같지만 형태가 다른 문장을 생성하는 방식

- 3. 외부 API 활용
크롤링한 데이터(출처: 네이버쇼핑, 올리브영)에 대해 NAVER CLOVA Sentiment API를 이용하여 Label을 'neutral'과 'negative'를 부여하는 방식
