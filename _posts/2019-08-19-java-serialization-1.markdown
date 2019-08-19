---
layout: post
title:  "JAVA Serialization - 개념편"
date:   2019-08-19 08:43:59
author: Lee YeJi
categories: Study Java
tags: 
comments: true
---

개발을 하던 중 자바 직렬화로 인한 문제가 발생했고 이에대해 공부한 내용을 정리하기위해 작성하였다. [우아한 형제들의 기술블로그](http://woowabros.github.io/experience/2017/10/17/java-serialize.html)를 참고하였고 먼저 직렬화에 대한 기본적인 개념들을 정리해보았다.

<hr>

# 자바 직렬화란?
자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 변환하는 기술과 바이트로 변환된 데이터를 다시 객체로 변환하는 기술(역직렬화)을 아울러서 이야기 함.

## 자바 직렬화 조건 및 방법
- 조건: java.io.Serializable 인터페이스를 상속받은 객체
<br>
<b>Model</b>
{% highlight java %}
class Message implements Serializable {
    private String user_name;
    private String content;

    public Message(String user_name, String content) {
        this.user_name = user_name;
        this.content = content;
    }
}
{% endhighlight %}
- 방법: java.io.ObjectOutputStream 객체를 이용
<br>
{% highlight java %}
    Message message = new Message("yeji", "hello");
    byte[] serializedMessage;
    try (ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
        try (ObjectOutputStream oos = new ObjectOutputStream(baos)) {
            oos.writeObject(message);
            // serializedMessage => 직렬화된 message 객체
            serializedMessage = baos.toByteArray();
        }
    }
    // 바이트 배열로 생성된 직렬화 데이터를 base64로 변환
    System.out.println(Base64.getEncoder().encodeToString(serializedMessage));
{% endhighlight %}


## 역직렬화 조건 및 방법
- 조건<br>
-직렬화 대상이 된 객체의 클래스가 클래스 패스에 존재해야 하며, import되어 있어야 함.<br>
-자바 직렬화 대상 객체는 동일한 serialVersionUID를 가지고 있어야 함.☆☆☆<br>
 따로 선언하여 관리하지 않아도 내부적으로 생성되지만 자바에서는 공식적으로 선언하여 관리하는 것을 적극 권장하고 있다. 이에 대해서는 다음 포스팅에서 자세히 다룰 것이다.

- 방법: java.io.ObjectInputStream 객체를 이용
<br>
{% highlight java %}
    // 직렬화 예제에서 생성된 base64 데이터 
    // ...생략
    String base64Message = Base64.getEncoder().encodeToString(serializedMessage);
    byte[] serializedMessage = Base64.getDecoder().decode(base64Message);
    try (ByteArrayInputStream bais = new ByteArrayInputStream(serializedMessage)) {
        try (ObjectInputStream ois = new ObjectInputStream(bais)) {
            // 역직렬화된 Message 객체를 읽어온다.
            Object objectMessage = ois.readObject();
            Message message = (Message) objectMessage;
            System.out.println(Message);
        }
    }
{% endhighlight %}

<b> [데이터 형태] </b>
- CSV <br>
-표 형태의 다량의 데이터의 직렬화 시 많이 쓰임<br>
-콤마를 기준으로 데이터를 구분<br>
-Apache Commons, Opencsv 등의 라이브러리를 이용<br>
- XML<br>
-구조적인 데이터를 직렬화 할 때 많이 쓰이나 최근에는 JSON을 더 많이 이용함.<br>
- JSON<br>
-최근 가장 많이 사용하는 포맷으로 구조적인 데이터를 직렬화 할 때 유용함.<br>
-자바스크립트에서 쉽게 사용 가능하고 다른 데이터 포맷 방식에 비해 오버헤드가 적다.<br>
  (왜 오버헤드가 적을까?-? => JSON은 문자열을 사용함으로 다른 포맷에 비해 용량이 작음)<br>
  이부분은 다음편에서 조금 더 자세히 설명할 예정이다.<br>
-Jackson, GSON 등의 라이브러리를 이용

## 자바 직렬화의 장점
- 자바 직렬화는 자바 시스템에서의 개발에 최적화되어 있다.<br>
- 복잡한 데이터 구조의 클래스 객체라도 직렬화 기본 조건만 지키면 쉽게 직렬화가 가능하다.<br>
  => 데이터 타입이 자동으로 맞춰지기 때문에 관련 부분에 신경을 쓰지 않아도 됨.

## 자바 직렬화의 단점
- 변경에 굉장히 취약하다.(이부분도 다음 포스팅에서 자세히 다룬다.)

## 자바 직렬화는 언제 어디서 사용되는가?
- JVM의 메모리에서만 상주되어있는 객체 데이터를 그대로 영속화(Persistence)할 필요가 있을 때 사용됨.<br>
- 시스템이 종료되더라도 사라지지 않는 장점을 가지며 영속화된 데이터이기 때문에 네트워크로 전송도 가능함.<br>
- 필요 할 때 직렬화된 객체 데이터를 가져와서 역직렬화하여 객체를 바로 사용할 수 있음.<br>

<b>[사용되는 부분]</b>
- 서블릿 세션(Servlet Session)<br>
서블릿 기반의 WAS들은 대부분 세션의 자바 직렬화를 지원하고 있다. 파일로 저장하거나 세션 클러스터링, DB를 저장하는 등의 기능을 수행 할 경우 세션 자체가 직렬화되어 저장, 전달 된다.
<br>
- 캐시(Cache)<br>
캐시를 이용하면 DB에 대한 리소스를 절약할 수 있기 때문에 자바 시스템에서는 퍼포먼스(성능!!)를 위해 캐시 라이브러리(Redis, Ehcache)를 많이 이용하게 된다. 이렇게 캐시 할 부분은 자바 직렬화된 데이터를 이용하여 저장하면 가장 간편하기 때문에 많이 사용된다.
<br>
- 자바 RMI(Remote Method Inovation)<br>
최근에는 많이 사용되지 않는 기술로 원격 시스템 간의 메시지 교환을 위해서 사용되는 기술이다. 보통 원격 시스템과의 통신을 위해서는 IP와 포트를 이용해서 소켓통신을 해야 하지만 RMI는 그 부분을 추상화하여 원격에 있는 시스템의 메서드를 로컬 시스템의 메서드인 것처럼 호출할 수 있다. 원격의 시스템의 메서드를 호출 할 시에 전달하는 메시지(보통 객체)를 자동으로 직렬화시켜 사용된다. 그리고 전달받은 원격 시스템에서는 메시지를 역직렬화를 통해 변환하여 사용된다.
<br>