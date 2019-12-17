# 1_Propositional_Logic

### 논리 / Logic

- 논리는 Symbolic Language이다.

- AI 분야에서 수학적으로 잘 정의한 언어를 사용해야 함, 그러므로 **논리**에 대해 공부해야 하는 것

- [Proposition Logic(명제 논리)](https://ko.wikipedia.org/wiki/명제_논리)

  [Predicate Logic(서술 논리 / 1차 서술 논리 / 1차 논리)](https://ko.wikipedia.org/wiki/술어_논리)

- Propositional Logic ⊃ Predicate Logic

## Syntax / 문법

### Operation

|      Operation      |         Read         |
| :-----------------: | :------------------: |
|          t          |        "true"        |
|          f          |       "false"        |
|   ￢ A (negation)   |       "not A"        |
| A ∧ B (conjunction) |      "A and B"       |
| A ∨ B (disjunction) |       "A or B"       |
| A ⇒ B (implication) |    "A implies B"     |
| A ⇔ B (equivalence) | "A if and only if B" |

- A ⇒ B 은 ￢ A ∨ B로도 쓰인다.
- A ⇔ B 은 (A ⇒ B) ∧ (B ⇒ A)로도 쓰인다.

### Formula(Proposition)

- 논리에서 '문장'이라고 표현되는 것 모두

- `A ∧ B`, `A ∧ A ∧ A`,  `(￢ A ∧ B) ⇒ (￢ C ∨ A)` 등의 표현식 모두 **Formula**라고 한다.

- **atomic formula(또는 proposition variable)** : A, B와 같이 truth 값이 들어가는 formula

  **compound formula** : ￢, ∧, ∨, ⇒, ⇔ 를 이용하여 표현되는 formula



## Semantics / 의미론

- formula가 참(true)인지 거짓(false)인지 정하는 것을 말한다.
- formula의 참과 거짓을 정하는 함수(mapping)을 정의하는 것으로부터 시작

### Mapping

- **Interpretation(assignment)** : 모든 formula의 truth값(true/false)을 지정하는 함수를 의미한다.
- **world** : proposition variable을 가지고 만들 수 있는 interpretation의 집합을 의미한다.
  - proposition variable이 n개면, interpretation은 2^n개



### 명제 논리의 의미론

- **mapping function I**

  - I(A ∨ B)의 값은 I(A)와 I(B)의 값에 의해 결정된다.

    따라서, I(A)가 참이거나 I(B)이 참이면 I(A ∨ B)이 참이 된다.

    `I(A ∨ B)=t iff I(A)=t or I(B)=t` 
    
  - 문법에서 정의한 모든 formula의 정의에 대해 truth value를 정의해야 한다.

    -> 진리표(Truth Table)로 정리

### Truth Table

![truth table](.\image\01_truth_table.JPG)

- empty formula는 모든 interpretations에 대해 true
- `A ≡ B`는 `A ⇔ B`를 설명하기 위한 **Meta Language**라고 할 수 있다.



### Satisfiability

- **Satisfiable** : 어떤 formula가 최소한 하나의 interpretation(world)에서 참일 때

- **Valid(logically valid)** : 어떤 formula가 모든 interpretation에서 참일 때

  - 이 때의 formula를 **tautology**라고 한다.

    ex) `A ∨ ￢A`는 tautology

- **Model** : 어떤 formula가 satisfiable일 때, 그 때의 interpretation을 의미
- **Unsatisfiable** : 어떤 formula가 모든 interpretation에서 거짓일 때



## Proof Systems

## Resolution

## Horn Clauses

## Computability and Complexity

## Applications and Limitations

