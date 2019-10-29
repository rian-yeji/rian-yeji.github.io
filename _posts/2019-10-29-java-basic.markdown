---
layout: post
title:  "[면접대비 기본개념] JAVA편"
date:   2019-10-29 06:43:59
author: Lee YeJi
categories: Study Java
tags: 
comments: true
---
<b>[목차]</b><br>
<a href="#chapter1" text-decoration:none >- OOP란? </a>
<br>
<a href="#chapter2" text-decoration:none >- Java / C++ / C 차이점 </a>
<br>
<a href="#chapter3" text-decoration:none >- Java의 특징</a>
<br>
<a href="#chapter4" text-decoration:none >- SOLID 원칙</a>
<br>
<a href="#chapter5" text-decoration:none >- 

<hr>
<h1 id="chapter1">- OOP란?</h1>
Object-Oriented Programing의 약자로 프로그램 설계방법론이자 개념의 일종이다.
프로그램을 단순히 데이터와 처리 방법으로 나누는 것이 아니라 프로그램을 수많은 '겍체'라는 기본단위로 나누고 이 객체들의 상호작용을 서술하는 방식이다.

### 객체 / 클래스 / 인스턴스 차이점

<h1 id="chapter2">- Java / C++ / C 차이점</h1>

<h1 id="chapter3">- OOP의 특징</h1>

1. 추상화 <br>
구체적인 사물들의 공통적인 특징을 파악해서 이를 하나의 개념으로 다루는 것
<br>
각 개체의 구체적인 개념에 의존하지말고 추상적 개념에 의존하여 설계해야 한다.

2. 캡슐화 <br>
연관있는 변수와 함수를 클래스로 묶는 작업<br>
높은 응집도와 낮은 결합도를 유지할 수 있도록 설계해야 한다.
- 응집도(Cohension): 클래스나 모듈 안의 요소들이 얼마나 밀접하게 관련되어 있는가
- 결합도(Coupling): 어떤 기능을 실행하는 데 다른 클래스나 모듈에 얼마나 의존적인가

3. 일반화(상속) <br>
여러 개체들이 가진 공통된 특성을 부각시켜 하나의 개념이나 법칙으로 성립시키는 과정<br>
일반화관계는 객체지향 프로그래밍 관점에서는 상속관계라 한다. 그래서 속성이나 기능의 재사용만 강조해서 사용하는 경우가 많다.<br>
부모자식 클래스간에는 'is a kind of'관계가 성립되어야 한다.

4. 다형성 <br>
서로 다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 능력<br>
다형성을 사용하면 코드를 간결하게 할 수 있고 구체적으로 현재 어떤 클래스 객체가 참조되는지와 무관하게 프로그래밍을 할 수 있어서 변화에 유연하게 대처할 수 있다.

<h1 id="chapter4">- SOLID 원칙</h1>
SRP(단일 책임 원칙), OCP(개방-폐쇄 원칙), LSP(리스코프 치환 원칙), DIP(의존 역전 원칙), ISP(인터페이스 분리 원칙)을 말하며, 앞자를 따서 SOILD 원칙이라고 부른다. 프로그래머가 시간이 지나도 유지 보수와 확장이 쉬운 소프트웨어를 만드는데 이 원칙들을 적용할 수 있다. 

1.	Single Responsibility Principle: 소프트웨어의 설계 부품은 단 하나의 책임만을 가져야 한다.

2.	Open-Closed Principle (개방-패쇄 원칙): 기존의 코드를 변경하지 않고(Closed) 기능을 수정하거나 추가할 수 있도록(Open) 설계해야 한다.

3.	Liskov Substitution Principle (리스코프 치환 원칙): 자식 클래스는 부모클래스에서 가능한 행위를 수행할 수 있어야 한다.

4.	Dependency Inversion Principle (의존 역전 원칙): 의존 관계를 맺을 때, 변화하기 쉬운 것 보단 변화하기 어려운 것에 의존해야 한다는 원칙이다. 

5.	Interface Segregation Principle (인터페이스 분리 원칙: 한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다. 하나의 일반적인 인터페이스보다는, 여러 개의 구체적인 인터페이스가 낫다.



