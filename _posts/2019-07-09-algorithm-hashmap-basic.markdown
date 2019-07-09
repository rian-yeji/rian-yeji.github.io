---
layout: post
title:  "HashMap 사용하기 + 유용한 함수"
date:   2019-07-08 08:43:59
author: Lee YeJi
categories: Algorithm
tags: Algorithm HashMap
comments: true
---

# 1. HashMap
- Map 인터페이스의 한 종류로 <key, value>로 이루어져있다.
- key값은 중복이 불가능하고 value는 중복이 가능하다.
- 동일 키값으로 추가 시 덮어쓰기 된다.
- value값엔 null값도 넣을 수 있다.
- 해싱 검색을 사용하기 때문에 대용향 데이터 관리 시에 좋은 성능을 보인다.

<br>
<hr>
<br>

# 2. HashMap 생성자/메소드

|                                       생성자/메소드                                       |                                                   설명                                                  |
|:-----------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------:|
| HashMap()                                                                                 | 기본 생성자 HashMap<K, V> hashmap = new HashMap<>();                                                    |
| HashMap(int initlalCapacity)                                                              | 주어진 값을 초기 용량으로 하는 HashMap을 생성                                                           |
| HashMap(Map m)                                                                            | 주어진 Map에 저장된 모든 요소를 포함하는 HashMap을 생성                                                 |
| void clear()                                                                              | HashMap에 저장된 모든 객체를 제거                                                                       |
| Object clone()                                                                            | 현재 HashMap을 복제하여 반환 newMap = (HashMap)map.clone();                                             |
| boolean containsKey(K Key)                                                                | HashMap에 지정된 키(Key)가 포함되어 있는지 알려준다.                                                    |
| boolean containsValue(V Value)                                                            | HashMap에 지정된 값(Value)가 포함되어 있는지 알려준다.                                                  |
| Set entrySet()                                                                            | HashMap에 저장된 Key - Value값을 엔트리(키와 값을 결합) 형태로 Set에 저장하여 반환                      |
| V get(K Key)                                                                              | 지정된 Key의 값을 반환                                                                                  |
| bloolean isEmpty                                                                          | HashMap이 비어있는지 확인한다.                                                                          |
| Set keySet()                                                                              | HashMap에 저장된 모든 키가 저장된 Set을 반환                                                            |
| V put(K Key, V Value)                                                                     | HashMap에 키와 값을 저장                                                                                |
| void putAll(Map m)                                                                        | 주어진 Map의 모든 요소를 HashMap에 저장                                                                 |
| V remove(Object Key)                                                                      | HashMap에서 주어진 key에 해당하는 값을 제거                                                             |
| int size()                                                                                | HashMap에 저장된 요소의 개수를 반환                                                                     |
| Collection values()                                                                       | HashMap에 저장된 모든 값을 컬렉션 형태로 반환                                                           |
| V getOrDefault(Object Key, Object defaultValue)                                           | 지정된 Key의 값을 반환하고 없을 시에는 defalultValue를 반환                                             |
| V putIfAbsent(Object Key, Object Value)                                                   | 지정된 Key의 값이 HashMap에 없을 경우 추가, Value를 반환                                                |
| V compute(K key,BiFunction<? super K, ? super V, ? extends V> remappingFunction)          | 지정된 Key의 값에 따라 Value를 어떻게 연산할지 정의, Value(리턴 값)을 반환                              |
| V computeIfAbsent(K key, Function<? super K, ? extends V> mappingFunction)                | 지정된 Key의 값이 HashMap에 없을 경우 Function의 리턴 값을 Value로 설정하고 추가, Value(리턴 값)을 반환 |
| V computeIfPresent(K key, BiFunction<? super K, ? super V, ? extends V> remappingFunction | 지정된 Key의 값이 HashMap에 있을 경우 Function의 리턴 값을 Value로 변경, Value(리턴 값)을 반환          |

<br>

### 2.1 Java8에서 추가된 Collection API
다음은 Java8에서 새롭게 추가된 함수들 중 일부이다. [참고한사이트](https://sticky32.tistory.com/entry/Java8-%EC%83%88%EB%A1%9C%EC%9A%B4-collection-api%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)

- V getOrDefault(Object Key, Object defaultValue)

key의 값을 가져오고 만약 값이 없거나 null이면 default값을 가져온다.
{% highlight java %}
Map<String, Integer> map = new HashMap<>();
map.put("A", 5); 
map.put("B", 6);

map.getOrDefault("A", 77); //result 5
map.getOrDefault("C", 77); //result 77
{% endhighlight %}

- V putIfAbsent(Object Key, Object Value)

key의 값이 없거나 null면 값을 추가한다. 위와 비슷해 보이지만 key="C"의 경우 위의 예제는 단순히 결과값만 나올뿐 Map에 추가되지 않고 아래의 예제는 새롭게 추가된다는 점이 다르다.
{% highlight java %}
Map<String, Integer> map = new HashMap<>();
map.put("A", 5); 
map.put("B", 6);

map.putIfAbsent("A", 77); //result 5
map.putIfAbsent("C", 77); //result 77
{% endhighlight %}

- V compute(K key,BiFunction<? super K, ? super V, ? extends V> remappingFunction)

Key의 값에 대해서 어떻게 연산할지 정의한다. 기존의 키에 대한 값이 없는 경우 V는 null로 생성된다.
{% highlight java %}
Map<String, Integer> map = new HashMap<>();
map.put("A", 1); 
System.out.println(map.compute("A", (s, integer) -> integer+1)); // result : 2 
System.out.println(map); // {A=2}
{% endhighlight %}


- V computeIfAbsent(K key, Function<? super K, ? extends V> mappingFunction)

기본적으로 compute와 동일하다. 다만 key의 값이 없을 경우에만 Function이 실행된다. 이 때 Function은 람다식을 사용한다.
{% highlight java %}
Map<String, Integer> map = new HashMap<>();
map.put("A", 5); 
map.computeIfAbsent("A", key -> 10);
map.computeIfAbsent("B", key -> 10);

System.out.println(map.get("A")); // result : 5
System.out.println(map.get("B")); // result : 10
{% endhighlight %}

- V computeIfPresent(K key, BiFunction<? super K, ? super V, ? extends V> remappingFunction)

`computeIfAbsent`와 반대로 key의 값이 존재할 경우에만 람다식이 실행된다.
{% highlight java %}
Map<String, Integer> map = new HashMap<>();
map.put("A", 5); 
System.out.println(map.computeIfPresent("A", (s, number) -> number*number)); // result : 25 
System.out.println(map.computeIfPresent("B", (s, number) -> 10)); // result : null
{% endhighlight %}

<br>
<hr>
<br>

# 3. HashMap 정렬
#### 3.1 Sort by key
key에 대한 정렬은 TreeMap객체를 사용하면 된다. 따로 정렬을 하지 않아도 되어있을 수 있으나 항상 보장할 수 있는것은 아니기때문에 필요한 경우라면 정렬해서 쓰는것이 안전하다.
{% highlight java %}
HashMap<Integer, String> map = new HashMap<>();
map.put(5, "abc");
map.put(3, "def");
map.put(10, "ghi");
		
TreeMap sortedMap = new TreeMap(map);
System.out.println(sortedMap); //{3=def, 5=abc, 10=ghi}
{% endhighlight %}

#### 3.2 Sort by value
key에 대한 정렬과 달리 값에 대한 정렬은 만들어져 있는것이 없어서 필요한 경우 Comparator 인터페이스를 이용하여 직접 구현해야 한다. 

이미 잘 설명된 글이 많으므로 링크만 달아두겠습니다
<br>
[참고사이트](https://cornswrold.tistory.com/114)
<br>
[참고사이트2](https://ithub.tistory.com/34)