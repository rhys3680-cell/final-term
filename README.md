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
| 06 | `06_rnn` *(예정)* | 문자 예측, 감성 분석, MNIST를 시퀀스로 |

## 01에서 배운 것

| 주제 | 핵심 |
|---|---|
| **스케일링** | 255로 나눌지는 **데이터를 확인하고** 정한다. Fashion-MNIST는 0\~255(나눔), LFW는 이미 0\~1(안 나눔) |
| **flatten** | DNN은 이미지를 1차원으로 펴야 한다 → **위치 정보가 사라진다** (CNN이 해결할 문제) |
| **과적합** | 학습 손실↓ 인데 검증 손실↑ 이면 외우기 시작한 것. **정확도가 아니라 손실을 보라** |
| **EarlyStopping** | `monitor='val_loss'`, `patience`, 그리고 **`restore_best_weights=True`** |
| **stratify** | 불균형 데이터를 나눌 때 클래스 비율 유지 |
| **혼동 행렬** | 정확도 하나로는 안 보이는 "어떤 클래스에서 틀리는지"를 드러낸다 |

실행 결과가 보여준 두 장면:

- **Fashion-MNIST (콜백 없음)** — 12에폭이 최적이었는데 50에폭을 다 돌려서
  검증 손실이 `0.3282 → 0.5838`로 나빠졌다. **과적합을 방치한 경우.**
- **LFW (EarlyStopping)** — 22에폭이 최적, 32에폭에서 자동 종료 후 22에폭 가중치 복원.
  이 옵션이 없었다면 검증 정확도 `0.8351` 대신 `0.7684`짜리 모델을 손에 쥐었을 것이다.
  **과적합을 막은 경우.**

## 작업 방식

1. 정리본 코드·마크다운을 설계
2. Colab에서 실행 (GPU T4)
3. Google Drive에 저장 → 다운로드 → `notebooks/`에 커밋 (출력 보존)

원본 노트북(`assets/`)은 실행 출력이 포함된 1.3MB 파일이라 git에서 제외합니다.

## 환경

- Python 3.13 / TensorFlow (Keras 3)
- 학습은 Colab GPU 런타임에서 수행