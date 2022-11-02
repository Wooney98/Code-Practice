# Data Processing
- Overview 길이 분포 및 최솟값, 최댓값 확인
- 텍스트 전처리
  - 이상치에 해당하는 overview의 이미지를 채우기
  - 한글 외 문자 제거
  - 'cat3'을 라벨링하여 target으로 전처리
  
 # 형태소 분석기로는 `kiwi`를 사용
 
 # 사전모델학습 klue/bert-base
 
 # K-Fold사용, n_splits 5로 지정
 # 폴드별로 나온 model_pth들을 argmax로 앙상블
 # public : 0.83405 / private : 0.84037
