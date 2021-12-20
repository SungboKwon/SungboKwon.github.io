---
layout: post
title: Logistic Regression Basic
subtitle: Coursera Machine Learning Course
categories: machine-learning
tags: [machine learning, coursera, logistic regression]
---

Cousera의 Ng교수님 수업 수강하며 내용을 요약합니다.


----------------------------------------------------------------

## What is Logistic Regression

Linear Regression이 연속한 차원의 결과값을 구하는 식의 계수를 찾는 과정이었다면, Logistic Regression은 이산 차원의 결과(0 or 1)를 구하는 식의 계수를 찾는 과정이다. 이를 위해 Logistic Regression의 Model은 Sigmoid Function을 통해 정의되며, 이로 인한 편미분 식의 차이는 있으나 전반적인 방법론은 Linear Regression과 동일하다.

## Hypothesis Representation
input을
$x_i$
, output을
$y_i$
라고 했을 때 pair
$(x_i, y_i)$
를 training example이라고 하고,
training example의 집합
$(x_i, y_i);i=1,...,m$
을 training set이라 한다.
logistic regression을 통해 함수
$h : X -> Y$
를 찾으며,
$h(x)$
를 hypothesis function이라 한다.
hypothesis function속에 각 항의 정해지지 않은 계수는
$\theta_n$
으로 설정한다.
( => Linear Regression과 동일)

Y는 0 혹은 1로 이루어져 있기 때문에 sigmoid function
$g(z) = \frac{1}{1+e^{-z}}$
를 이용하여
$h(x) = g(\theta^Tx) = \frac{1}{1+e^{-\theta^Tx}}$
가 된다.



## Cost Function
MMSE는
$h(x)$
와
$y_i$
간의 차(오차)를 제곱하여 cost를 구한다.
하지만 sigmoid function을 사용한 logistic regression의 hypothesis function에 이를 적용할 경우 local minimum이 많아져 gradient descent가 좋은 결과를 내기 어려워진다.
따라서 cost function은
$h(x_i)$
와
$y_i$
의 차에 따라 그 값이 0에서
$\infty$
까지 변화하는 log 함수를 통해 표현한다.
$J(\theta) = \frac{1}{2m}\sum_{i=1}^{m}[y_i\log(h_\theta(x_i))+(1-y_i)\log(1-h_\theta(x_i))]$

$J(\theta)$
를 최소화하는
$\theta$
를 찾으면 hypothesis function을 찾을 수 있다.
J를 찾는 과정에서, Gradient Descent와 Normal Equation을 사용할 수 있다.
알고리즘 복잡도는 Gradient Descent가
$O(n^2)$
, Normal Equation이
$O(n^3)$
으로,
training set의 규모가 적을 때 Normal Equation이, 클 때 Gradient Descent가 유리하다.

## Gradient Descent
Initial
$\theta$
로부터 시작하여 각 차원에 대한 편미분 값을 빼며 극소값으로 점근하는 방법이다.
마찬가지로 sigmoid function을 그대로 편미분하면 local minimum으로 빠질 수 있기 때문에
$h(x)$가 linear한 경우의 편미분 식(linear regression에서 구한 편미분 식)
$\theta_n := \theta_n - \alpha\frac{1}{m}\sum_{i=1}^{m}(h_\theta(x_i) - y_i)x_i; x_0 = 1$
에
$h_\theta(x_i)$
에만 sigmoid function을 포함하는 hypothesis function을 적용하는 방식으로 식을 구한다.

$\vec{\theta_n} := \vec{\theta_n} - \alpha\frac{1}{m}Xsigmoid(X^T\vec{\theta}) - X^TY$

## Multiclass Classification
y의 값이 0,1 두가지가 아니라 여러가지인 경우의 문제이다.
y의 결과값을 A, B, C, ...라고 했을 때,
결과가 A인 경우를 1, 나머지를 0으로 하여 Single Class문제로 해결한다.
결과가 B인 경우 또한 1, 나머지를 0으로 하여 해결한다.
이와 같이 각 결과 값에 대해 1인지의 여부를 찾는 hypothesis function을 찾아 문제를 해결할 수 있다.

## Issues
* Gradient Descent, Normal Equation외의 알고리즘을 Logistic Regression에 적용한다면?
* Cost Function과 Gradient Descent의 편미분 식의 수학적 근거를 더욱 깊이 확인해보자.
