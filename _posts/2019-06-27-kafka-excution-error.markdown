---
layout: post
title:  "Kafka server 실행 오류"
date:   2019-07-08 08:43:59
author: Lee YeJi
categories: ResolvedError Kafka
tags: Kafka
comments: true
---
카프카를 사용한 프로젝트를 진행하며 서버를 자주 껐다 켰다 할일이 있었는데 어느순간 갑자기 카프카 서버 실행오류가 나서 인터넷을 찾아보고 해결했다. 그런데 그 문제가 반복해서 나타나서 매번 찾아야하는 번거로움에 간단하게 정리해보았다.

zookeeper는 문제없이 실행되고 kafka-server를 실행할 때 나는 오류인데 다음과 같이 kafka-logs 파일에 문제가 있다고 나온다.
<img src="/image/Error/kafka_logs_error/kafka_logs_error.png">

카프카 서버 실행 때마다 매번 나는것은 아닌데 로그파일이 많이 쌓이면 나는것 같다. 
이럴땐 C:\tmp 아래의 kafka-logs 디렉토리 자체를 삭제한 후 다시 실행하면 정상적으로 실행된다. 
<img src="/image/Error/kafka_logs_error/kafka_logs_directory.png">