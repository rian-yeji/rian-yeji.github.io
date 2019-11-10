---
layout: post
title:  "JAVA 배열, list 중복제거"
date:   2019-11-10 06:43:59
author: Lee YeJi
categories: Study Java
tags: 
comments: true
---
Java에서 중복을 제거하는데는 기본 코드로 반복문을 돌거나 라이브러리 함수를 이용하는 등 여러 방법이 있다. 중복제거는 빈번하게 등장하는 개념이라 각 방법에 대해 정리해보았다.
<hr>

## 1. 배열의 요소를 직접 확인하며 중복을 제거
{% highlight java %}
String[] dataList = {"apple", "banana", "orange", "apple", "grape", "banana"};
ArrayList<String> arrayList = new ArrayList<>();

for(String data : dataList){
    if(!arrayList.contains(data))
        arrayList.add(data);
}

System.out.println(arrayList); //result = [banana, orange, apple, grape]
{% endhighlight %}
Logic을 직접 구현하는 방식으로 중복제거의 경우에 한해서는 Set자료구조의 사용보다 속도가 빠르다는 장점이 있다.

## 2. Set을 이용하여 중복제거 (HashSet, LinkedHashSet, TreeSet)
dataList는 위와 동일
{% highlight java %}
HashSet<String> hashSet = new HashSet<>();
LinkedHashSet<String> linkedHashSet = new LinkedHashSet<>();
TreeSet<String> treeSet = new TreeSet<>();
for(String data : dataList){
    hashSet.add(data);
    linkedHashSet.add(data);
    treeSet.add(data);
}
System.out.println(hashSet); //result = [banana, orange, apple, grape]
System.out.println(linkedHashSet); //result = [apple, banana, orange, grape]
System.out.println(hashSet); //result = [banana, orange, apple, grape]
{% endhighlight %}

<b>Set은 요소의 중복을 허용하지 않는 데이터의 집합이다.</b> 단순히 데이터들을 add하는 것으로 중복을 제거할 수 있어서 효율적이다. 

Set의 하위 클래스로는 HashSet, LinkedHashSet, TreeSet등이 있는데 <b>HashSet은 데이터의 순서를 전혀 보장하지 않고 LinkedHashSet은 추가된 순서에 따라 저장되며 TreeSet은 자동으로 정렬(default는 오름차순)해서 저장된다는 차이점이 있다.</b> 

위의 결과만 보면 HashSet도 순서가 보장된 것 처럼 보이나 데이터의 갯수가 작아서 생긴 우연의 일치일뿐 순서가 보장되어야 하는 경우에는 LinkedHashSet, 정렬이 필요한경우 TreeSet을 사용해야한다.

- <b>List에서 Set의 사용</b>

주어진 데이터가 배열이 아니라 List라면 위의 방법처럼 방법문을 돌며 add하지 않고 생성시에 바로 대입해서 사용가능하다. 
{% highlight java %}
ArrayList<String> dataList = new ArrayList<>();
dataList.add("apple");
dataList.add("banana");
dataList.add("orange");
dataList.add("apple");
dataList.add("grape");
dataList.add("banana");

HashSet<String> hashSet = new HashSet<>(dataList);
LinkedHashSet<String> linkedHashSet = new LinkedHashSet<>(dataList);
TreeSet<String> treeSet = new TreeSet<>(dataList);
{% endhighlight %}

- <b>한줄로 끝내기!</b>
{% highlight java %}
String[] dataList = {"apple", "banana", "orange", "apple", "grape", "banana"};
dataList = new HashSet<String>
(Arrays.asList(dataList)).toArray(new String[0]);
{% endhighlight %}

## 3. Array / List / Set 형변환
데이터 자료구조를 변환해야 할 때 주의점은 자료구조를 바꾸는 것이지 자료형을 바꾸는것은 아니라는 것이다. 

즉 String형은 변환이 가능하지만 Integer로 선언된 List나 Set을 int형 배열로 바꾸는것은 아래의 방법으로는 불가능하다. 

반복문을 돌며 하나하나 추가해서 바꾸는 방법과 각 자료구조에서 제공하는 메서드를 사용하는 방법이 있는데 해당 포스팅에서는 메서드를 사용하는 방법만 소개한다.

### 3-1. List to Array
{% highlight java %}
ArrayList<String> arrayList = new ArrayList<>();
//Add datas
String[] array = arrayList.toArray(new String[0]);
{% endhighlight %}
- 이전 버전에서는 적절한 크기의 배열을 만들기위한 java reflection의 호출이 느리게 수행돼서 new String[arrayList.size()]로 사전에 크기를 지정하여 사용하는 방식을 많이 사용했는데 OpenJDK 6의 업데이트 이후 해당 호출이 내재되어 있고 사전에 지정된 크기의 배열인 경우 null값이 들어갈 우려가 있어서 new String[0]으로 빈 배열을 생성하여 사용하는 방식을 선호하고 있다.

### 3-2. Array to List
{% highlight java %}
String[] array = new String[10];
//Add datas
ArrayList<String> arrayList = new ArrayList<>(Arrays.asList(array));
{% endhighlight %}

### 3-3. List to Set / Set to List
List와 Set은 모두 Java Collection을 상속받기 때문에 생성시 매개변수로 넣어주면 변환이 가능하다.
{% highlight java %}
ArrayList<String> arrayList = new ArrayList<>();
//Add datas
Set<String> set = new Set<>(arrayList);
{% endhighlight %}

{% highlight java %}
Set<String> set = new Set<>();
//Add datas
ArrayList<String> arrayList = new ArrayList<>(set);
{% endhighlight %}

이외에 addAll()을 이용할 수도 있다.
{% highlight java %}
ArrayList<String> arrayList = new ArrayList<>();
//Add datas
Set<String> set = new Set<>();
set.addAll(arrayList);
{% endhighlight %}

{% highlight java %}
Set<String> set = new Set<>();
//Add datas
ArrayList<String> arrayList = new ArrayList<>();
arrayList.addAll(set);
{% endhighlight %}