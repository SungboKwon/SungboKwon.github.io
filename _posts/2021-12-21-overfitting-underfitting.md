---
layout: post
title: Overfitting and Regularization
subtitle: Coursera Machine Learning Course
categories: machine-learning
tags: [machine learning, coursera, regularization]
---

Cousera의 Ng교수님 수업 수강하며 내용을 요약합니다.


----------------------------------------------------------------

## Underfitting And Overfitting

Underfitting은 학습을 통한 결과 hypothesis function이 충분히 맞춰지지(fit) 않은 것으로,
feature의 수가 적으면 발생하며, training example조차도 예측률이 떨어진다.
Overfitting은 학습을 통한 결과 hypothesis function이 지나치게 맞춰진(fit) 것으로,
feature의 수가 많을 때 고차항의 계수등 일부 계수(
$\theta$
)가 Cost Function에 과한 영향을 미쳐 발생한다. training example set에 대해 높은 예측률을 보이지만 새로운 data에 대한 예측에 실패하게 된다.

underfitting은 고차항과 feature의 곱으로 이루어진 항 등을 추가하여 해소할 수 있다.
overfitting은 feature를 줄이거나(고차항을 없애는 등) Regularization을 통해 해소할 수 있다.


## Regularization
특정 항이 Cost Function에 과한 영향을 미치는 것을 방지하기 위해 각 항의 Cost Function에 대한 영향을 평준화하는 방법이다.
Cost Function에 일정 계수를 가진
$\theta$
의 제곱항을 더해준다.
이로 인해
$\theta$
의 값이 전체 Cost에 주는 영향이 상대적으로 감소한다.

$J(\theta) = \frac{1}{2m}[\sum_{i=1}^{m}(h_\theta(x_i)-y_i)^2 + \lambda\sum_{j=1}^{n}\theta_j^2]$

이 때 lambda의 값이 지나치게 커지면
$\theta$
의 값이 0으로 수렴하면서 Underfitting이 발생하게 된다.

## Regularized Linear Regression
Cost Funtion은 상기한
$J(\theta)$
와 같다.

Gradient Descent에서는 기존의 각
$\theta$
에 대한 편미분 식에 Regularazation항의 편미분 항이 추가된다.

$-\alpha\frac{\lambda}{m}\theta$

Normal Equation에서는
$(n+1)*(n+1)$
의 Identity Matrix에서 (1,1)의 값이 0인 행렬을 A라고 할 때,

$XX^T\vec{\theta} - X^TY + \lambdaA\vec{\theta} = 0$

$\vec{\theta} = (XX^T+\lambdaA)^-1X^TY$
와 같이 구할 수 있다.

## Regularized Logistic Regression

Cost Funtion 마찬가지로 Logistic Regression의 Cost Function에 lambda를 계수로 한
$\theta^2$
항을 더해준다.

$J(\theta) = \frac{1}{m}\sum_{i=1}^{m}[y_i\log(h_\theta(x_i))+(1-y_i)\log(1-h_\theta(x_i))] + \frac{\lambda}{2m}\sum_{j=1}^{n}\theta_j^2$

Gradient Descent에서도 Linear Regression과 동일하게 기존의 각
$\theta$
에 대한 편미분 식에 Regularazation항의 편미분 항이 추가된다.

$-\alpha\frac{\lambda}{m}\theta$


## Issues
* 적정한 lambda의 값을 정하는 방법은?
* Regularization 외에 Overfitting 해소를 위한 방법은 없는가?
