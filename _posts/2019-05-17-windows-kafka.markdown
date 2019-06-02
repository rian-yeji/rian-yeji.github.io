---
layout: post
title:  "Apache Kafka 다운로드 및 실행"
date:   2019-05-16 19:30:00
author: Lee YeJi
categories: Kafka
tags: Kafka
---
이번년도 3월부터 한이음멘토링을 진행하며 화상회의 프로그램 개발을 주제로 잡았는데 그 중 채팅기능을 구현할때 보다 높은 성능을 위해 Apache Kafka를 적용해보기로 했고 이에따라 처음 카프카 시작하기위한 설치과정과 cmd로 실행하여 consumer와 producer가 메시지를 주고받는 기능까지 실습해보았다.
<hr>
[목차]
<br>
<a href="#first" text-decoration:none >1. Kafka란?</a>
<br>
<a href="#second" text-decoration:none >2. Kafka 다운로드 및 실행</a>
<br>

<h1 id="first">1. Kafka란?</h1>
<p>
Apache Kafka는 아파치 소프트웨어 재단이 스칼라로 개발한 오픈 소스 메시지 브로커 프로젝트이다. 이 프로젝트는 실시간 데이터 피드를 관리하기 위해 통일된, 높은 스루풋의 낮은 레이턴시를 지닌 플랫폼을 제공하는 것이 목표이다.
</p>

<h5>#카프카는 일반적으로 두 가지의 광범위한 종류의 응용 프로그램에 사용된다.</h5>
<ol>
<li>1. 시스템 또는 응용 프로그램간에 데이터를 안정적으로 얻는 실시간 스트리밍 데이터 파이프 라인 구축</li>
<li>2. 데이터 스트림을 변환하거나 이에 반응하는 실시간 스트리밍 애플리케이션 구축</li>
</ol>

<h5>#카프카의 기본 개념</h5>
<ol>
<li>1. Kafka는 여러 데이터 센터로 확장 될 수있는 하나 이상의 서버에서 클러스터로 실행된다.</li>
<li>2. 카프카 클러스터는 주제(topic)라는 카테고리에 레코드 스트림을 저장한다.</li>
<li>3. 각 레코드는 키, 값 및 타임 스탬프로 구성된다.</li>
</ol>

<h5>#카프카가 제공하는 핵심 API</h5>
<img src="/image/kafka_post/kafka-apis.png" width="600px" height="500px">
<br>
출처: [https://kafka.apache.org/intro][kafka_apis_url]
<br><br>
<li>Producer API<br>
한 개 이상의 topic에 스트림을 게시 할 수있는 응용 프로그램을 제작</li>
<li>Consumer API<br>
한 개 이상의 topic을 구독하고 생성된 레코드 스트림을 처리</li>
<li>Streams API<br>
한 개 이상의 topic에서 입력 스트림을 소비하고 출력 스트림을 생성<br>
효과적으로 입력 스트림을 출력 스트림으로 변환 할 수 있음</li>
<li>Connector API<br>
kafka에 기록된 데이터를 기존 응용 프로그램 또는 DB에 연결하는 재사용 가능한 Producer 또는 Consumer를 구축 및 실행할 수 있음</li>


<h1 id="second">2. Kafka 다운로드 및 실행</h1>
<h5>#아파치 카프카 설치</h5>
아파치 카프카는 아파치 공식 홈페이지([https://kafka.apache.org/downloads][kafka_download_url])에서 원하는 버전을 다운로드하거나, 다음 링크에서 2.2.0파일을 바로 받아서 압축만 풀면 되므로 굉장히 간단하다.
[http://mirror.navercorp.com/apache/kafka/2.2.0/kafka_2.12-2.2.0.tgz][kafka_file_url]
<br>
해당 포스팅은 Window10기반으로 작성되었다.

<h5>#아파치 카프카 실행</h5>
<p>설치가 간편했던 것에 비해 실행은 과정이 조금 많은데, Apache Kafka는 zookeeper라고 하는 오픈소스 분산형 구성 서비스 위에서 돌아 가기 때문에 zookeeper를 먼저 실행 해 주어야 한다.</p>

<h6>#Zookeeper 실행</h6>
{% highlight PowerShell %}
cd kafka압축해제경로\bin\windows
zookeeper-server-start.bat ../../config/zookeeper.properties
{% endhighlight %}
<img src="/image/kafka_post/zookeeper_execute.PNG" width="700px" height="200px">
<br><br>

그리고 새로운 cmd창을 열어서 kafka server를 실행한다.

<h6>#Kafka server 실행</h6>
{% highlight PowerShell %}
cd kafka압축해제경로\bin\windows
kafka-server-start.bat ../../config/server.properties
{% endhighlight %}
<img src="/image/kafka_post/kafka_server.PNG" width="700px" height="200px">
<br>

<h6>#Topic 생성</h6>
{% highlight PowerShell %}
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic [토픽명]
{% endhighlight %}

<h6>#Topic list 확인</h6>
{% highlight PowerShell %}
kafka-topics.bat --list --zookeeper localhost:2181
{% endhighlight %}

<h6>#Consumer</h6>
{% highlight PowerShell %}
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic [토픽명]
{% endhighlight %}

<h6>#Producer</h6>
{% highlight PowerShell %}
bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic [토픽명]
{% endhighlight %}


[kafka_apis_url]: https://kafka.apache.org/intro
[kafka_download_url]: https://kafka.apache.org/downloads
[kafka_file_url]: http://mirror.navercorp.com/apache/kafka/2.2.0/kafka_2.12-2.2.0.tgz