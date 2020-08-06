[TOC]

# Lab 10-1 - Sigmoid 보다 ReLU가 더 좋아

> ReLU 활성화 함수에 대해 알아본다.

## Problem of Sigmoid

- Input --> Network --> Output
  - 이 때의 ground-truth와 output의 차이를 loss(또는 cost)라고 한다.
  - Loss를 미분한 것을 Backpropagation 하면서 weight와 bias를 학습
    - d(loss) - gradient (loss를 미분)
    - 여러 Layer 사이에 있는 Activation Function으로 Sigmoid로 쓰다보면, Backpropagation하면서 loss값이 점차 상실된다. (**Vanishing Gradient**)
      - Sigmoid는 x가 -∞나 ∞로 갈수록 미분값이 0에 수렴(거의 0)하기 때문
      - 다수의 Sigmoid 미분값을 곱하면 이런 0으로 수렴하는 값때문에 loss가 상실된다는 것

## ReLU

- f(x) = max(0, x)

  - x가 0보다 작은 경우에는 0, 0보다 큰 경우에는 x를 취한다.

    ![2-10_Graph_of_ReLU](../MDImage/2-10_Graph_of_ReLU.PNG)

  - 장점 : x가 0보다 클 때의 미분값은 항상 1이기 때문에, loss가 상실되는 경우가 없다.

  - 단점 : x가 0보다 작을 때의 미분값은 항상 0이기 때문에, loss가 전달되지 않는다.

- ***왜 쓸까?*** : 단점이 존재하더라도, Backpropagation이 잘 되기 때문에 많이 쓴다.

- 그 외에 쓰는 Activation Function

  `tf.keras.activations` 안에 Activation Function이 있으므로, 바꿔가면서 성능차이 확인 및 Model 학습을 해볼 것

  - tanh
  - elu
  - selu
  - leaky relu : `tf.keras.layers` 안에 있음
    - x가 음수일 때, 어떤 α 값을 x에 곱한 값으로 되어 있다.(보통 α는 0.1이나 0.01)
    - x가 양수일 때는 ReLU와 같음

---

# Lab 10-2 - Weight 초기화 잘해보자

> 가중치 초기화(Weight Initialization)에 대해 알아본다

## Weight Initialization 종류

- Xavier(자비어) Initialization (= Glorot Initialization)
- He Initialization

### Xavier Initialization

- Network의 목표는 어느 한 지점으로부터 (Global) Loss Minimum을 찾아내기 위한 학습을 하는 것
  - 그러나 Loss Minimum이 다수인 경우(Local Loss Minimum이 존재하는 경우) 어느 지점에서 시작하냐에 따라 Global Loss Minimum에 도달하지 못할 수 있다.
  - Saddle Point(안장점)에 도달하는 경우도 있다.
    - Saddle Point : 어느 방향에서 보면 극대값이지만, 다른 방향에서 보면 극소값이 되는 점
- Global Loss Minimum을 찾기 위해 좋은 출발점을 찾아야 하는데, Xavier는 그것을 찾아준다.
- 지금까지 했던 예제에서는 weight 정할 때, random normal(평균 0, 분산 1인 random 함수)를 이용하여 initailization을 했다.
  - **Xavier**의 경우, 평균은 0, 분산은 2/(Channel_in + Channel_out)인 random 분포로 weight를 설정
    - **Channel_in** : Input으로 들어가는 Channel의 갯수
    - **Channel_out** : Output으로 나오는 Channel의 갯수

### He Initialization

- ReLU 함수에 특화되어 있는 weight initialization 기법
- 평균은 0, 분산은 Xavier의 2배(4/(Channel_in + Channel_out))인 경우다.

---

# Lab 10-3 - Dropout

> Dropout에 대해 알아본다.

## Why do we use Dropout?

- Training Data sample으로 학습한 Network의 종류가 있을 때, 다음과 같이 분류가 가능하다.

  - Under-fitting : Training Data sample를 너무 못 맞추는 경우
  - Good : Training Data sample를 적절히 맞추는 경우
  - Over-fitting : Training Data sample를 너무 잘 맞추는 경우

  Under-fitting 경우는 train 데이터도 잘 못 맞추기 때문에 test 데이터도 못 맞추기 마련이지만,

  Over-fiiting 경우는 train 데이터는 아주 잘 맞추면서도 test 데이터를 맞추는 정확도가 떨어진다.

  - **Why?** Train 데이터 샘플만 잘 맞추기 때문에, 모델이 알지 못하는 전혀 다른, 새로운 데이터에 대한 정확도가 보장이 되지 않기 때문

- 우리는 Over-fitting과 Under-fitting을 피하는 방법으로 **Dropout**(Regularization 중 하나)이라는 기법을 사용할 수 있다.

## What is Dropout?

- 어떤 모델을 학습 시킬 때, 몇 개의 뉴런(노드)을 제외하고 학습하는 방법을 의미
  - 끄는 노드는 Randomly 정해진다.
- (ex) 고양이 분류 모델이 있다고 가정할 때, Dropout을 하지 않으면 고양이의 모든 부분을 가지고 학습을 하지만, Dropout을 하면 고양이의 일부분(귀, 눈, 발, 꼬리 등)만 가지고도 학습을 할 수 있다.
  - 갈색 고양이로 학습 시켜도, 검은 고양이, 회색 고양이로 테스트 해도 분류를 해낼 수 있게 된다.