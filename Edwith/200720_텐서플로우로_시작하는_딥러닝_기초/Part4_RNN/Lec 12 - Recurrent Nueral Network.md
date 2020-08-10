[TOC]

# Lec 12 - NN의 꽃 RNN 이야기

> 순환 신경망(Recurrent Neural Network)에 대해 알아본다.

## Sequence Data

- 어떤 데이터가 시계열 특징이 있을 때
- 이전 데이터가 다음 데이터에 영향을 미칠 때
- (ex) 음성인식, 자연어 데이터 등
  - 하나의 단어로만 전체 맥락을 알 수 있지 않음
- NN / CNN으로는 이를 판단 불가

## RNN

![12_RNN_architecture](../MDImage/12_RNN_architecture.PNG)

- X0를 A라는 수식에 넣으면 h0(또는 Y0)라는 결과 값이 나오는데, 이는 다음 h1을 도출할 때, 새로운 input과 함께 영향을 준다는 의미

### State

- RNN 연산 중 어느 한 시점에서의 결과 값

![12_RNN_formula](../MDImage/12_RNN_formula.PNG)

- Vanilla RNN을 통해 h_t 연산 후, 최종 y_t 도출

  `h_t = tanh(W_hh * h_(t-1) + W_xh * x_t)`

  `y_t = W_hy * h_t`

  - 여기서는 f_w로 tanh를 사용

## Character-level language model example

### word training of  'hello' 

- x0, x1, x2, x3, x4 = 'h', 'e', 'l', 'l', 'o' 입력
- 이 때, 'h', 'e', 'l', 'o' 각 글자에 대한 one-hot encoding이 선행되어야 함
- 첫 state 학습 후 나온 결과 값(hidden layer)을 다음 state의 input값으로 함께 이용
- output layer는 state 값을 이용하여 도출

![12_RNN_hello_example](../MDImage/12_RNN_hello_example.PNG)

- 두 번째 output layer의 경우, 원하는 답과 실제 답이 다름 -> softmax로 해결



## RNN 활용 예시

- Language Modeling
- Speech Recognition
- Machine Translation
- Conversation Modeling/Question Answering
- Image/Video Captioning
- Image/Music/Dance Generation

### Multi-Layer RNN

### LSTM

### GRU