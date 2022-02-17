---
layout: post
title: Neural Networks
subtitle: Coursera Machine Learning Course
categories: machine-learning
tags: [machine learning, coursera, neural network]
---

Cousera의 Ng교수님 수업 수강하며 내용을 요약합니다.


----------------------------------------------------------------

## Neural Networks

Feature가 굉장히 많고, Linear하지 않은 등의 경우에 대한 Classification 문제를 해결하기 위해 Neural Networks를 사용한다.
인체의 신경망의 동작을 흉내내는 알고리즘으로, 하나의 (neuron)이 logistic unit으로 표현되고, 이러한 logistic unit이 여러개 모인 계층을 여러개 묶어 하나의 학습을 진행하는 형태로 이루어진다.

## Model Representation
Logistic Unit은 Sigmoid (logistic) activation function
$a_j^{(i)}$
로 표현된다.(i: layer number, j: layer 내 unit 순번)

$a_j^{(i)} = sigmoid(\vec{\theta_j^{(i-1)}}\vec{a_{k}^{(i-1)}})

Logistic Unit의 조합을 통해 이산 논리 회로를 구성할 수 있다(AND/OR/NOT/XOR 등)

## Multiclass Classification
마지막 Layer의 Unit의 수가 Class 수 만큼 존재하도록 구성한다.

## Cost Function

## Backpropagation

모든 i, j, l에 대해 $/Delta_{i, j}^{(l)}:=0$ 로 초기화한다.

각 training example에 대해,
1. $a^{(1)} := x^{(t)}
2. forward propagation을 수행하며 $a^{(l)}$을 구한다.

$a^{(n)} = sigmoid(\theta^{(n-1)}a^{(n-1)})$
3. $\delta^{(L)} = a^{(L)} - y^{(t)}$를 구한다.
4. back propagation을 수행하며 $\delta^{(l)}$을 구한다.

$\delta^{(l)} = ((\theta^{(l)})^T\delta^{(l+1)}).*a^{(l)}.*(1-a^{(l)})$

>>특정 unit의 cost function을  

(WHY?)
5. $\Delta$를 업데이트한다.

$\Delta^{(l)}:=\Delta^{(l)}+\delta^{(l+1)}(a^{(l)})^T$

$D_{i,j}^{(l)}:=\frac{1}{m}(\Delta_{(i,j)}^{(l)}+\lambda\theta^{(l)}_{i,j})$, if j is not 0

$D_{i,j}^{(l)}:=\frac{1}{m}\Delta_{(i,j)}^{(l)}$, if j = 0

Gradient descent의 Cost Function 편미분항은 $D_{i,j}^{(l)}$이다.

##Unrolling Parameters

fminunc등의 함수를 사용하기 위해 vector를 parameter로 넘겨야 한다.
>thetaVector = [Theta1(:); Theta2(:);]

처럼 nxm 차원의 matrix를 n*m 차원의 vector로 변환한다(unrolling)

fminunc 함수의 결과물을 reshape 함수를 수행하여 matrix로 변환한다.
>reshape(thetaVec(111:120), 10, 11)

##Gradient Checking
back propagation이 오동작 할 수 있다.
이에 대한 검증을 위해 Gradient Checking을 수행한다.

$\frac{\partial}{\partial\Theta}J(\Theta) \approx \frac{J(\Theta + \epsilon) - J(\Theta - \epsilon)}{2\epsilon}$

위 수식으로 특정 $\Theta$에서의 J의 근사된 편미분값을 구할 수 있다.
Backpropagation으로 구한 편미분값과 근사된 편미분값이 근사하다면 Backpropagation이 정상동작한다는 것을 확인할 수 있다.
이후 gradient check없이 Backpropagation을 수행할 수 있다.

>근사된 gradient는 로직은 간단하지만 연산 수행 속도가 느려 Backpropagation을 대체할 수 없다.

##Random Initialization
$\Theta$의 초기값을 설정할 때 Symmetric하게 설정될 경우 Backpropagation을 동일하게 수행하여 학습이 제대로 이루어질 수 없다.
Symmetric하지 않은 초기값 설정을 위해 $-\epsilon$에서 $\epsilon$ 사이의 Random 값으로 초기값을 설정한다.
>Theta1 = rand(10,11)*(2*INIT_EPSILON) - INIT_EPSILON;

##Neural Network Process
1. Neural Network Architecture : 각 Hidden Layer의 Unit의 수를 모두 같도록 하는 것을 default로 한다.
2. Random Initialization
3. Forward Propagation -> get hypothesis function
4. implement cost function
5. implement Backpropagation -> partial derivatives
6. gradient check 을 통해 Backpropagation 동작 검사
7. fminunc, Backpropagation을 통해 학습

>Gradient descent는 경사에 따른 하강을, Backpropagation은 하강의 방향을 정한다.
