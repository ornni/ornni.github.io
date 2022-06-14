---
layout: single
title:  "SVM multiclass OvR, OvO 특징"
---


Suppor vector machine(SVM)은 대표적인 이진분류(binary classification)모델이다.<br>

SVM으로 다중분류를 하기 위해서는 OvR이나 OvO의 방법을 이용해야 한다.<br>

각각의 특징은 아래와 같다.<br/>


**OvR(One-vs-Rest), OvA(One-vs-All)**<br>

- 숫자 대 나머지를 비교하는 전략

- 숫자별로 숫자 하나만 구별하는 이진분류기를 만들어서 점수를 매김

- 대부분 OvR 방법을 선호:)<br>

ex) MNIST dataset을 이용하는 경우 10개의 점수 중 가장 높은 점수를 선택<br/>


**OvO(One-vs-One)**<br>

- 1대1로 이진분류기를 만드는 방법

- 작게 나눠서 훈련시키는 것이 유리한 알고리즘에 사용<br>

ex) MNIST datset에서 10개 중 2개를 고르는 방법, 즉 45개의 분류기를 만들어서 양성이 가장 많은 클래스로 분류
