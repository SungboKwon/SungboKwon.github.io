---
layout: post
title: Linear Regression Basic
subtitle: Coursera Machine Learning Course
categories: machine-learning
tags: [machine learning, coursera, linear regression]
---

Cousera의 Ng교수님 수업 수강하며 내용을 요약합니다.


----------------------------------------------------------------

## What is Linear Regression
>티코 브라헤는 덴마크 왕가(프레데릭 2세)의 전폭적인 지원과 자신의 재능을 바탕으로 장기간 천문을 관측하여 방대한 데이터를 수집합니다.
>프레데릭 2세의 죽음과 함께 신성 로마제국의 프라하로 옮긴 브라헤는 독일의 수학자이자 천문학자인 요하네스 케플러를 채용합니다.
>브라헤의 죽음으로 브라헤의 방대한 데이터를 얻은 케플러는 이 데이터를 정리하기 시작한다.
>당시 케플러는 행성의 공전 궤도가 원 궤도일 것이라고 믿고 원 궤도에 데이터를 맞추어보았으나 약간의 오차가 발생한다.
>브라헤의 관측에 대한 오차보다 더 믄 오차가 발생한다고 생각한 케플러는 '화성의 전투'라고 불리는 방대한 계산을 통해 행성 궤도에 대한 식을 찾아낸다.
>이것이 케플러의 제 1, 제 2 법칙이며, 케플러의 법칙은 뉴턴 역학의 정립에 큰 영향을 미치게 된다.

과학의 발전은 연역과 귀납의 두 엔진을 통해 이루어졌다.
그 중 특히 귀납적 방법론은, 다양하게 수집된 데이터를 해석하여 일정한 수식을 도출해내고, 이에 대한 설명을 붙이는 방향으로 이루어진다.
데이터로부터 일정한 수식을 도출해내는 방법 중 하나가 Linear Regression이라고 할 수 있다.
통계는 과학의 수단에서 인문학으로 그 사용 범위가 확장되었고, 그와 함께 사회 또한 과학적으로 접근하는 사회과학의 한 틀이 되었다.
이제 우리는 보다 방대하고 다양한 데이터를 수집할 수 있고, 이를 컴퓨터를 통해 빠르게 해석할 수 있는 시대를 살고 있다.

Linear Regression은 설정한 다항식에 대한 계수를 찾는 방향으로 이루어진다.
'어떤 상황'에서 '어떤 결과'가 나타났는지에 대한 데이터는 각각 '어떤 상황'이라는 입력값과 '어떤 결과'라는 출력으로 이루어진다.
각 입력값에 대한 다양한 차수의 항으로 다항식을 구성했을 때, 계수를 조정하여 데이터의 패턴과 가장 유사한 계수의 집합을 찾아내는 과정이다.

## Model Representation
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
linear regression을 통해 함수
$h : X -> Y$
를 찾으며,
$h(x)$
를 hypothesis function이라 한다.
hypothesis function속에 각 항의 정해지지 않은 계수는
$\theta_n$
으로 설정한다.

## Cost Function
$y_i$
와 학습을 통해 정해질
$h(x_i)$
의 값의 차이는 예측에 대한 오차이다.
이 오차는 linear regression에 대한 cost가 된다.
training example들에 대한 error들을 최소화하는 방안으로  Minimum Mean Square Error(MMSE)라는 통계적 기법을 사용한다.
>MMSE

>Error의 제곱의 평균을 최소화하여 찾고자 하는 값에 가장 근사한 값을 찾는다.


$MSE = j(\theta) = \frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x_i)-y_i)^2$
가 된다.
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
Linear하지 않은 경우 Local Minimum으로 빠질 수 있다.
Learning Rate(
$\alpha$
)가 크면 diverge(발산)할 수 있고, 너무 작으면 converge(수렴)까지 오래걸린다.

$\theta_n := \theta_n - \alpha\frac{1}{m}\sum_{i=1}^{m}(h_\theta(x_i) - y_i)x_i; x_0 = 1$

$\vec{\theta_n} := \vec{\theta_n} - \alpha\frac{1}{m}XX^T\vec{\theta} - X^TY$

한편 feature의 range가 크게 차이날 경우 점근 중 swing이 많이 발생한다.
안정적 점근을 위해 feature scaling을 해준다.(각 feature의 range를 조정 : 빼고 나눈다!)

## Normal Equation
미분 값이 0이 될 때 함수는 극값을 갖는다.
각 $\theta_n$에 대해 편미분하여 극값을 갖는 $\theta_n$을 찾는다.

$XX^T\vec{\theta} - X^TY = 0$

$\vec{\theta} = (XX^T)^-1X^TY$


각 편미분식의 해를 찾을 수 있는지 혹은
$XX^T$
의 역행렬을 찾을 수 있는지가 문제가 된다.
redundant feature(선형적 의존)를 없애고,
training set보다 feature가 더 많은 경우는 feature를 줄이거나 regularization을 수행한다.

## Issues
* Feature를 어떻게 정하는가
* Data는 어떻게 수집할 수 있는가
* Mean Square Error에 대한 이해
* Gradient Descent, Normal Equation외의 알고리즘은 없을까
* 유사한 다른 통계적 기법은 어떤게 있을까
(추세선과 계절성을 분리하여 각각의 Regression을 수행하는 등)
