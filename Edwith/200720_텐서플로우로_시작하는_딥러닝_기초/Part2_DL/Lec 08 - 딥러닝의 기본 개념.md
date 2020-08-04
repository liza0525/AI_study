[TOC]
# Lec 08-1 - 딥러닝의 기본 개념 : 시작과 XOR 문제
> 딥러닝의 기본 개념과 XOR 문제에 대해 알아본다.

## Deep Learning의 등장
### Ultimate Dream: thinking machine
- 인류의 궁극적인 꿈 : 난제를 기계가 대신 해결
- 뇌과학에 대한 관심
    - 뉴런은 수학적인 해석을 할 수 있음 => Deep Learning의 시초가 됨
    - 위의 예시는 Logistic regression으로 표현할 수 있음
- Input ---- (Implement) ----> Output
- Dr. Frank Rosnblatt : Hardware적인 딥러닝을 시도
    - *'언제가는 기계가 걷고, 말하고, 자가 생산 등을 할 수 있을 것이다.'*

### AND / OR Logic
> 50년대 당시에는 AND / OR 연산이 가능하면 어느정도 AI에 대한 희망이 있다고 생각
#### OR 연산
|X1|X2|Y|
|--|--|-|
|0 |0 |0|
|1 |0 |1|
|0 |1 |1|
|1 |1 |1|
#### AND 연산
|X1|X2|Y|
|--|--|-|
|0 |0 |0|
|1 |0 |0|
|0 |1 |0|
|1 |1 |1|
#### XOR 연산
- 당시에는 이에 대한 기계 연산이 불가능했다.
- 아래의 표를 정확히 나타내는 Linear Function을 구할 수 없었음
- 아무리 높여도 50%의 정확도만 해결

|X1|X2|Y|
|--|--|-|
|0 |0 |0|
|1 |0 |1|
|0 |1 |1|
|1 |1 |0|
- 이에 대한 연구가 시작됨

### Perceptron(1969)
> by Marvin Minsky
- 결론적으론 XOR는 당시의 기술로는 풀 수 없다고 생각함
    - Multilayer Layer Perceptrons(MLP)로 해결할 수 있음을 주장
        - *'여러 개의 레이어를 합치면 XOR를 해결할 수 있을 것이다.'*
        - *'대신 weight나 bias를 학습 시킬 수 없다.'*

### Backpropagation(역전파)
> 1974, 1982 by Paul Werbos, 1986 by **Hinton**
- error가 났을 경우에는 거꾸로 돌아가며 각 Layer의 weight와 bias를 조절하는 알고리즘(1974 논문)
    - 당시에는 사람들로부터 별 반응이 없었음(Minsky마저도)
- Hinton이 1986년에 Rediscovery(재발견) --> 사람들의 주목을 갖게 됨
- XOR은 물론이고 좀 더 복잡한 문제도 풀 수 있게 됨

### Convolution Neural Networks
- 고양이가 그림을 보는 도중의 뉴런을 연구(by Lecun)
    - 보는 그림에 따라 활성화되는 뉴런이 다르다는 것을 발견
    - 일부를 보는 신경망들이 있고 후에 조합이 되는 것이라고 생각
    - 이것이 CNN 이론의 기반이 됨
- AlphaGo도 CNN 형식

### Neural Network의 계속적인 발전(~1990 초반)
- ALVINN : 무인 자동차
- Terminator2 (1991)

### A Big Problem : Neural Network의 위기와 침체(1990 중반)
- Backpropagation의 한계 : Layer가 많아질수록 Error가 점점 전달이 되지 않아 의미가 희미해짐
- 다른 DL 알고리즘의 등장 : SVM, RandomForest 등

---

# Lec 08-2 - 딥러닝의 기본 개념 2: Back-propagation과 2006/2007 '딥'의 출현
> 딥러닝의 발전 역사를 이어 알아본다.
## CIFAR
- Canadian Institute for Advanced Research
- 딥러닝에 대한 관심을 극대화 시킨 캐나다의 연구 단체
### Breakthrough in 2006 and 2007(by Hinton & Bengio)
- 2006 논문 : 초기값만 잘 준다면 NN를 잘 학습할 수 있다.
- 2007 논문 : 신경망을 보다 깊게 구축하면 다양한 문제 해결 가능
## ImageNet
- 이미지를 인식하는 모델망 구축 챌린지
- 오답률이 30% 가까이었으나 2012년 AlexNet을 통해 약 15%까지 급격히 떨어짐
- 2015년에 3%까지 떨어졌고, 이는 인간의 오답률보다도 낮아짐

## 딥러닝의 계속적인 발전
- 노이즈 환경 음성 인식
- 알파고
- 게임 플레이 자동화 등