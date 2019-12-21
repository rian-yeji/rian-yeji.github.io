---
layout: post
title:  "Java String Method"
date:   2019-12-21 06:43:59
author: Lee YeJi
categories: Study Java
tags: 
comments: true
---
자바에서 문자열을 사용할 때 가장 자주 쓰이는 String에 대해 정리하고 자주 사용하는 함수를 정리한다.
<hr>

- Java의 String은 int나 char같은 원시타입처럼 쓰이지만 참조형 클래스객체이다. 
- String 클래스는 일단 생성되면 그 값은 길어지거나 줄어들수 없으며 문자가 변경될수도 없다. 그래서 String객체는 불변(immutable)객체라고 한다.
- String의 + 연산을 수행 할 때 객체의 내용이 바뀌는 것이 아니라 두개의 문자열을 기반으로 새로운 객체가 생성되는 것이다.
- String 타입의 비교는 ==가 아닌 .equals()를 사용한다.

<br><br><br>

<h3 style="text-align:center">String Class Method</h3>

|            funtion           |                                            내용                                           |  반환값  |
|:----------------------------:|:-----------------------------------------------------------------------------------------:|:--------:|
|           startWith          |                           문자열이 지정한 문자로 시작하는지 판단                          |  boolean |
|            endWith           |                        문자열 마지막에 지정한 문자가 있는지를 판단                        |  boolean |
|            equals            |                             두개의 String의 문자열 값만을 비교                            |  boolean |
|            indexOf           |         지정한 문자가 문자열의 몇번째에 있는지 판단 없을 경우 -1을 반환(왼쪽기준)         |    int   |
|          lastindexOf         |        지정한 문자가 문자열의 몇번째에 있는지 판단 없을 경우 -1을 반환(오른쪽 기준)       |    int   |
|            length            |                                    문자열의 길이를 반환                                   |    int   |
| replace(target, replacement) |         문자열에 지정한 문자가(target) 있으면 새로 지정한 문자로(replacement) 변경        |  String  |
|          replaceAll          |                           정규표현식을 지정한 문자로 바꿔서 출력                          |  String  |
|             split            |                                지정한 문자로 문자열을 나눔                                | String[] |
|           substring          | 문자열에 지정한 범위에 속하는 문자열을 반환(시작 위치의 값은 포함, 끝 위치의 값은 미포함) |  String  |
|          toLowerCase         |                              문자열의 대문자를 소문자로 변환                              |  String  |
|          toUpperCase         |                              문자열의 소문자를 대문자로 변환                              |  String  |
|           toString           |                                    문자열을 그대로 반환                                   |  String  |
|             trim             |                                    문자열의 공백을 제거                                   |  String  |
|            valueOf           |                                지정한 개체의 원시 값을 반환                               |  String  |
|           compareTo          |         문자열의 사전순 값을 비교하여  같으면 0, 좌측값이 크면 1, 작으면 -1을 반환        |    int   |
|           contains           |                  두개의 String을 비교해서 비교대상 String 포함여부를 판단                 |  boolean |
|            charAt            |                               지정한 index번째에 문자를 반환                              |    int   |
|            concat            |                                     문자와 문자를 결합                                    |  String  |
|            format            |                        서식문자열을 이용해서 서식화된 문자열을 반환                       |  String  |
|            matches           |                             지정한 정규 표현과 일치하는지 판단                            |  boolean |
|         replaceFirst         | 문자열내에 있는 정규식과 매치되는 첫번째 문자열을 replacement 문자열로 바꾼 문자열을 반환 |  String  |