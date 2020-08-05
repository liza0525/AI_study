[TOC]


# Lec 09 - 1 - XOR 문제 딥러닝으로 풀기

> 딥러닝으로 XOR 문제를 풀어본다

## XOR Model

- 하나의 Logistic Regression으로는 XOR를 풀 수 없음이 증명되었음
- 따라서 다수의 Logistic Regression로 Neural Network를 구성하면 될 것이라 생각함
  - 하지만 이런 경우 W, b는 어떻게 학습 시키는가?

### XOR using NN

![2-9-1_XOR_using_nn](../MDImage/2-9-1_XOR_using_nn.PNG)

#### 증명

- 각 Logistic Regression의 weight와 bias가 위와 같다고 가정
- 첫 번째 Logistic Regression의 Y1 값은 0이 된다
  - 0 * 5 + 0 * 5 - 8 = -8 --->[Sigmoid] ---> 0
- 두 번째 Logistic Regression의 Y2 값은 1이 된다
  - 0 * (-7) + 0 * (-7) + 3 = -3 --->[Sigmoid] ---> 1
- 세 번째 Logistic Regression의 Y_hat 값은 1이 된다
  - 0 * (-11) + 1 * (-11) - 5 = 6 --->[Sigmoid] ---> 0
- 따라서 X1 = 0, X2 = 0일 때, XOR 연산한 Y_hat은 0이 되므로, 예상한 값과 같다.
- 모든 X1, X2 쌍에 대해서 모두 계산해보면 XOR 연산에 대한 NN을 만들 수 있다는 것을 증명할 수 있다.



----

# Lab 09-1 - Neural Net for XOR

> 신경망 네트워크를 코드로 구현하여 XOR 문제를 해결한다.
## Logistic Regression
- [Recap](./Lec 05 - Logistic Regression_Classification.md)

### Logistic Regression for XOR

> X1과 X2가 같으면 0, 다르면 1 출력

| X1   | X2   | XOR  |
| ---- | ---- | ---- |
| 0    | 0    | 0    |
| 0    | 1    | 1    |
| 1    | 0    | 1    |
| 1    | 1    | 0    |

![2-9-1_XOR_graph](../MDImage/2-9-1_XOR_graph.PNG)

- 위의 그래프를 기존에 배운 Logistic Regression으로**만** 표현하는 것은 한계가 있다.

### Forward Propagation

- 다수의 Linear Regression을 통해 XOR를 구현할 수 있다.

  ![2-9-1_XOR_forward_propagation](../MDImage/2-9-1_XOR_forward_propagation.PNG)

### Neural Net

- **Logistic Regression 한 개** : Linear Function + Logistic Function + Decision Boundary

- 위의 그림은 Layer가 2개인 경우 --> 2 Layer

```python
# Tensorflow Code
def neural_net(features):
    layer1 = tf.sigmoid(tf.matmul(features, W1) + b1)
    layer2 = tf.sigmoid(tf.matmul(features, W1) + b2)
    hypothesis = tf.sigmoid(tf.matmul(tf.concat([layer1, layer2], -1), W3) + b3)
    return hypothesis
```

#### Vector

- Layer에 있는 다수의 Linear Regression도 벡터를 이용해 하나의 Component로 합칠 수 있다.

  ![2-9-1_XOR_nn_vector](../MDImage/2-9-1_XOR_nn_vector.PNG)

```python
# Tensorflow Code
def neural_net(features):
    layer = tf.sigmoid(tf.matmul(features, W1) + b1)
    hypothesis = tf.sigmoid(tf.matmul(layer, W2) + b2)
    return hypothesis
```

### Chart

- 위와 같이 다양한 컴포넌트 조합을 통해

  - RNN
  - LSTM
  - AE

  등을 만들어 낼 수 있다.

## 실습

- [lec9-1_nn_for_xor](./practice/lec9-1_nn_for_xor.ipynb)