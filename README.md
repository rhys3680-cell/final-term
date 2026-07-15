# 딥러닝 수업 정리 (새싹 영등포)

수업 중 작성한 노트북(`assets/Day2~4.ipynb`, 코드만 있고 설명이 없는 라이브 코딩 로그)을
**주제별로 재구성하고 설명을 붙인** 복습용 자료입니다.

각 노트북은 Colab에서 실행한 **출력(학습 로그·그래프)을 그대로 보존**하고 있어서,
GitHub에서 클릭만 하면 코드와 결과를 함께 볼 수 있습니다.

## 노트북

| # | 노트북 | 내용 |
|---|---|---|
| 01 | [01_dnn_basics](notebooks/01_dnn_basics.ipynb) | Fashion-MNIST로 **과적합을 관찰**하고, LFW 얼굴 인식에서 `EarlyStopping`·`stratify`·혼동 행렬로 해결 |
| 02 | [02_dnn_pitfalls](notebooks/02_dnn_pitfalls.ipynb) | 직접 그린 이미지를 넣었더니 **확률 0.99997로 확신하며 오답**, 12장으로 1050만 파라미터 학습하기 |
| 03 | [03_cnn](notebooks/03_cnn.ipynb) | Conv/Pooling으로 **위치 정보를 살리기**, DNN의 1/4 파라미터·1/10 에폭으로 같은 정확도 |
| 04 | [04_cnn_callbacks](notebooks/04_cnn_callbacks.ipynb) | 개 vs 고양이, `EarlyStopping` + `ModelCheckpoint`로 최적 모델 저장 — 그리고 **202장으론 CNN도 못 배운다** |
| 05 | [05_autoencoder](notebooks/05_autoencoder.ipynb) | 정답 없이 배우기, Dense vs Conv 디코더(1/67 파라미터), **2차원 잠재공간 시각화**와 숫자 생성 |
| 06 | [06_rnn](notebooks/06_rnn.ipynb) | 순서를 기억하기 — 문자 예측·감성 분석·MNIST 시퀀스, 그리고 **깊다고 좋은 게 아니다** |
| 07 | [07_cnn_rnn_scratch](notebooks/07_cnn_rnn_scratch.ipynb) | 밑바닥부터 — CNN·RNN·역전파를 NumPy로 손계산해 Keras와 대조 |
| 08 | [08_seq2seq](notebooks/08_seq2seq.ipynb) | Seq2Seq 번역(영↔한), `Tokenizer`·`pad_sequences`, Bidirectional·LSTM |

*07은 01~06의 원리를 파헤치는 심화편, 08부터는 Day5 NLP 시리즈입니다.*

## 시리즈를 관통하는 세 가지 메시지

1. **데이터를 먼저 보라.** 스케일·극성·균형·양 — 모델보다 데이터가 먼저다. (01, 02, 04)
2. **정확도 하나를 믿지 마라.** 손실, 혼동 행렬, 검증 곡선을 함께 보라. (01, 02)
3. **크게 ≠ 좋게.** 구조에 맞는 모델이 이긴다 — CNN의 필터 재사용, Conv 디코더,
   1층 RNN이 모두 "적은 파라미터로 더 나은 결과"를 보여줬다. (03, 05, 06)

각 노트북 끝에 그 노트북에서 배운 것을 표로 정리해두었습니다.

## 작업 방식

1. 정리본 코드·마크다운을 설계
2. Colab에서 실행 (GPU T4)
3. Google Drive에 저장 → 다운로드 → `notebooks/`에 커밋 (출력 보존)

원본 노트북(`assets/`)은 실행 출력이 포함된 1.3MB 파일이라 git에서 제외합니다.

## 환경

- Python 3.13 / TensorFlow (Keras 3)
- 학습은 Colab GPU 런타임에서 수행