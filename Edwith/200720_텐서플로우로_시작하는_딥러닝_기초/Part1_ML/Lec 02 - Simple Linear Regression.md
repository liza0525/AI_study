# Lec 02 - Simple Linear Regression

> 단순 선형 회귀 : ML의 핵심 개념

## Regression이란?

- 사전적으로는 후퇴, 퇴보의 의미

- **Francis Galton(통계학자/인류학자)** 

  *"Regression toward the mean(평균)"*

  즉, 어떤 Data들의 크기와 상관 없이 이 Data들은 **전체 평균**으로 회귀하려는 특징을 갖고 있다는 의미

## Linear Regression

- 선형회귀 : 데이터를 가장 잘 대변하는 직선을 방정식으로 나타낸 것
- **y = ax + b**
  - 우리가 구해야 하는 것: a, b
- 어떤 Data들의 입력과 출력의 관계(증감)를 표현

## Hypothesis

- 어떤 데이터들이 있을 때 이에 대해 가장 잘 대변하는 직선의 식을 **H(x) = Wx+b** 라고 가정해보자
  - W : Weight
  - b : Bias
  - 이 때의 가설 함수는 궁극적으로는 우리가 만들 '**모델(Model)**' 이라고 볼 수 있다.
- 이 때 W와 b의 값을 어떻게 구할 수 있을까?

## Cost

> 동의어 : loss, error

- **H(x) - y**

  - x값에 의한 H(x) 값과 실제 Data의 y값 사이의 차이

  - 각 Cost의 값들의 평균이 작을수록 해당 직선이 Data를 잘 대변한다는 것을 의미

    - 이 때 Cost는 음수가 나올 수 있기 때문에, Cost를 제곱을 한 값을 합하여 평균을 구하도록 한다.

      ![fomula_for_minimize_cost](../MDImage/1-2_fomula_for_minimize_cost.PNG)

- **How fit the line to our (training) data**
- **Goal : *minimize cost(W, b)***

---

## 실습

### 아나콘다 가상환경 설정

```conda
conda create -n [가상환경 이름]
activate [가상환경 이름]
conda install tensorflow
conda install jupyter
jupyter notebook
```

- 가상환경의 pip가 jupyter notebook에서 적용이 안될 때는 `conda install jupyter`를 해주면 해결

### Tensorflow 문법

#### tf.reduce_mean(*list*)

- 값의 평균을 나타냄

- 차원(rank)이 하나 줄어들게 된다.

  ```python
  v = [1., 2., 3., 4.,] # rank 1
  tf.reduce_mean(v) # 2.5 # rank 0
  ```

#### tf.square(*variable*)

- 값의 제곱 수를 나타냄

  ```python
  tf.square(3) # 9
  ```

#### A.assign_sub(B)

- -= 연산과 동일

- tensorflow 코드에서는 -= 연산은 사용할 수 없기 때문에 assign_sub 메소드를 이용

  ```python
  W.assign_sub(learning_rate * W_grad)
  # W -= learning_rate * W_grad
  ```

#### tf.exnable_eager_execution()

- 즉시 실행하는 코드

### Gradient Descent(경사 하강법)

- cost를 최소화 시키며 W, b를 찾는 방법 중 하나

  (*minimization algorithm/ minimization function*)

  ```python
  import tensorflow as tf
  
  x_data = [1, 2, 3, 4, 5]
  y_data = [1, 2, 3, 4, 5]
  
  # 임의로 값을 정해주면 된다
  W = tf.Variable(2.9)
  b = tf.Variable(0.5)
  
  hypothesis = W * x_data + b
  
  cost = tf.reduce_mean(tf.square(hypothesis - y_data))
  
  # learning_rate initialize
  learning_rate = 0.01
  
  for i in range(100):
      # Gradient descent
      # GradientTape()은 with 구문과 같이 쓰는 편
      with tf.GradientTape() as tape:
          # 변수(W, b) 변환의 정보를 tape에 기록/저장한다는 것
          hypothesis = W * x_data + b
          cost = tf.reduce_mean(tf.square(hypothesis - y_data))
  
      # tape 내 변수들의 경사도 값, 즉 미분값을 구함
      # cost 함수에 대하여 [W, b] 변수들의 개별 미분 값을 튜플로 반환한다는 것
      W_grad, b_grad = tape.gradient(cost, [W, b])
  
      # W와 b값을 업데이트 한다
      # learning_rate : 해당 gradient 값을 얼마만큼 반영할 것인지 결정 / 보통은 0.01 또는 0.0001 같은 작은 값을 선택
      W.assign_sub(learning_rate * W_grad)
      b.assign_sub(learning_rate * b_grad)
  ```

  - 위의 구문을 여러 번 반영하여 W와 b의 값을 찾아가는 것이므로 for문으로 반복한다.

  - 값의 변화를 확인하기 위해 위 예제에 다음 코드를 붙여 확인해봐도 된다.

    ```python
    if i % 10 == 0:
        print("{:5}|{:10.4}|{:10.4}|{:10.6f}".format(i, W.numpy(), b.numpy(), cost))
    ```

  - Epoch : 학습 횟수

    - 위의 예제에서는 Epoch는 100까지(if i==99)



#### 결과

W는 1로, b는 0, cost는 0으로 수렴하게 된다.

- cost가 0으로 수렴한다는 것은 해당 모델이 실제 값을 잘 예측한다는 의미

#### Predict

```python
print(W * 5 + b)  # tf.Tensor(5.0066934, shape=(), dtype=float32)
print(W * 2.5 + b) # tf.Tensor(2.4946523, shape=(), dtype=float32)
```

- 이 모델을 사용하게 된다면 (오차 범위 내에서) 실제 값과 동일한 값을 출력하는 것을 알 수 있다. 