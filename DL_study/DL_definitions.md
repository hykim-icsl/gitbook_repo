## Regression
- 독립변수와 종속변수 간의 관계를 가장 잘 나타내는 예측선을 긋는 것
- regression은 관계를 잘 나타내는 Coefficient를 찾는 것을 말하나?

## Linear Regression 
- 독립변수와 종속변수 간의 관계를 가장 잘 보이는 직선 혹은 Hyperplane으로 나타낸다.
- Simple linear Regression :  독립변수가 하나인 경우 : x
- Multiple linear Regression :  독립변수가 2개 이상인 경우 : x1, x2, … , xn

## Logistic Regression
- 독립변수에 따른 종속 변수의 값이 0 혹은 1로 구분되는 값을 가질 때 이러한 관계를 잘 보이는 곡선을 activation function과 weight값을 찾아서 나타내는 것
- 주로 sigmoid 함수를 사용한다.

## Perceptron
- N개의 입력에 대해 0 또는 1로 출력을 내주는 박스 단위로 볼 수 있다.
- N개의 입력(x1, x2, … , xn)이 들어갔을 때 각각의 입력에 대해 Weight가 곱해지고 bias값이 더해진 결과가 Activation 함수 등을 통해서 0 or 1로 결과를 내어놓는다.

![perceptron](/DL_study/images/perceptron.png)

> 그림인용 : 모두의 딥러닝 개정2판

## Epoch
- 학습 프로세스가 모든 샘플에 대해 한번 실행되는 것을 1 epoch
 
## Batch Size
- 한번에 몇 개의 샘플을 끊어서 처리할 것인지
- Batch size가 너무 크면 학습속도가 느려지고, 너무 작으면 각 실행 값의 편차가 생겨 결과값이 불안정해질 수 있다. Batchsize는 컴퓨터 메모리를 고려해야할 필요가 있다.

## Softmax

## 경사하강법
- '어떤 loss function이 정의되었을 때 손실함수의 값이 최소가 되는 지점을 찾아가는 방법
- Loss function을 Weight에 대해 편미분 진행 => 