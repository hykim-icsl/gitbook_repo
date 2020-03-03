## Neural Net
- 가장 최소단위인 perceptron의 조합을 통해 이루어진다.
- **로지스틱 회귀가 퍼셉트론의 개념과 동일하다.**
  - y=wx+b (w weight, b bias) => activation function
- 퍼셉트론은 결과적으로 2개중 1개의 결과를 낼수 있도록 구분하는 선, 면, hyperplan을 구하는 작업이다.

## 인간의 신경망과 인공 신경망의 관계 예상
- 뉴런 -> 신경망 -> 지능
- 퍼셉트론 -> 인공신경망 -> 인공지능
- 하지만 perceptron만 가지고 인공신경망을 구현할 수 없었고(XOR문제), 이를 해결하기 위해 Hidden Layer를 포함한 Multilayer perceptron을 통해 인공신경망을 구축하게 되었다.

## Multilayer perceptron
- Multilayer perceptron : **입력층과 출력층 사이에 hidden layer가 존재하는 perceptron**
- 2차원 평면에 나타난 XOR값을 구분할 수 있는 직선은 존재하지 않는다
- 이를 해결하기 위해 입력층과 출력층 사이에 Hidden layer를 두고 좌표평면에 변화를 주는 역할을 하도록한다.
- 쉽게 생각해서 Hidden layer는 **입력값 x1, x2, … , xn이 존재하는 domain을 직선 하나로 구분이 가능한 다른 domain으로 transform시키는 것**으로 볼 수 있다.



## Neural Net (인공신경망, 신경망)
- 퍼셉트론 하나로 해결되지 않는 문제를 입력층 출력층 사이에 hidden layer를 추가함으로써 복잡한 문제를 해결 가능하도록 했다.
- 여러 뉴런들이 복잡한 과정을 통해 사고하는 것이 이와 비슷해 인공 신경망이라 부르기 시작함

## Backpropagation (오차 역전파 이론)

### 신경망 구현과정
- 환경변수 지정 : 데이터셋 (입력 값 ,결과 값), Learning rate, 활성함수, 가중치
- 신경망 실행 : 초기값 입력 후 실행
- 결과를 실제 값과 비교 : 오차측정
- 역전파 실행 : Weight 수정
- 결과 출력

### 딥러닝
- 인간의 신경망이 여러층이 되어 지능이 되듯, 인공 신경망을 쌓아 올리면(hidden layer를 여러층으로 하여) 인공지능이 될거라 생각했으나, 결과가 좋지 않았다고 한다.

- 문제점? 기울기 소실문제

기울기 소실 문제 (Gradient vanishing problem)
학습하면서 weight를 수정하기 위해 오차역전파 과정을 거치는데, hidden layer가 많을 수록 역전파를 통해 전달되는 기울기 값이 점점 작아져 맨 처음 층까지 전달되지 않는 기울기 소실 문제가 발생
- 활성화 함수로 사용된 시그모이드 함수의 특성 (시그모이드 함수는 미분시 최대값이 0.3으로 계속 곱하다보면 0에 가까워짐)
- 이를 해결하기 위해 tanh, Relu 등이 사용됨



다중분류(multi classification)
- 활성함수로 softmax가 사용됨
- Softmax : n개의 결과값을 도출하는 경우 총합이 1이 되면서 가장 그럴듯한 값에 높은 가중치를 주어 결과를 출력한다.

![multi classification](/DL_study/images/multiclass.png)

> 그림인용 : 모두의 딥러닝 개정2판



Overfitting
- 학습 데이터 셋을 가지고는 높은 정확도를 보이지만, 새로운 데이터를 가지고 적용할 경우 정확도가 낮은 것을 말한다.
- 네트워크의 weight 값들이 학습 데이터에 너무 과하게 맞춰져 있다는 의미
- Layer가 너무 많거나, 변수가 복잡하거나, 테스트셋과 학습셋이 중복되는 경우 
- 주어진 데이터를 학습데이터와 테스트 데이터로 구분하여 학습 후 테스트를 진행

K-fold cross validation
- 테스트를 정확하게 한다면(test data 수가 많은 경우) Model의 검증이 충분히 이루어질 수 있다.
- 하지만 테스트 데이터가 충분하지 않다면?