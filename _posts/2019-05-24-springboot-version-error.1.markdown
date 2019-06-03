---
layout: post
title: "java.lang.NoSuchMethodError:
javax.servlet.http.HttpServletRequest.
getHttpServletMapping()Ljavax/servlet/http/HttpServletMapping;"
date:   2019-05-28 08:43:59
author: Lee YeJi
categories: ResolvedError
tags: Spring
comments: true
---

<a href="#solution" text-decoration:none >☆해결방법 바로가기☆</a>
<br>

### 1. 문제발생
IntelliJ를 설치하고나서부터 계속 겪고있던 오류가 있는데, 제목과 같이
<b>java.lang.NoSuchMethodError: javax.servlet.http.HttpServletRequest.getHttpServletMapping()Ljavax/servlet/http/HttpServletMapping;</b>
servlet관련 함수를 찾지 못해서 발생한 오류였다. 하지만 내가 만든건 Spring Boot프로젝트였고 의존성의 버전관리는 자동으로 되어야했기때문에 굉장히 당황스러웠다. 
<img src="/image/Error/springboot_version_error/nosuchmethod.PNG">

### 2. 해결을 위한 노력
일단 서버를 실행시키는데까지는 문제가 없는데 localhost:8080으로 접속하는 순간 오류가 발생했다.
처음에는 내가 spring에 익숙하지 않아서 뭔가 잘못하고있는건가 했는데 인터넷에 나와있는 예제를 똑같이 배껴도 안돌아가는걸 보고 문제가 있다는것을 알게되었다.

이 문제를 해결하기위해 처음 해본일은 예전에 돌아갔었던 프로젝트들이 제대로 작동하는지 확인하는 것이었다. 기존의 프로젝트들마저 안돌아간다면 컴퓨터 자체의 문제거나 툴이나 java같은 좀 더 근원적인 부분이 문제일것 같아서 굉장히 긴장했었다. 
하지만 기존에 돌아갔던 프로젝트들은 정상적으로 작동했으므로 이것은 내가 새로 만들고 있는 프로젝트들에 한정된 문제라는것을 파악했다.

다음으로는 혹시 내가 작성한 코드에 문제가 있을까해서 아무것도 작성하지 않은 빈프로젝트를 만들어서 실행시켜보았다. 여기서부터 문제가 보이기 시작했는데 정말 아무것도 없는 빈프로젝트에서도 같은 오류가 발생하였다.

사실 여기까지 파악하는것도 굉장히 오랜시간이 걸렸고 최대한 해결하기위해 노력하려고 구글링도 많이 해보았다.

대부분의 답변에서 '버전이 맞지 않는다'는 키워드를 발견했다. 톰캣버전에 관한 이야기가 많아서 톰캣도 제일 최신버전으로 다시 깔아보았으나..... 이 과정중 다시 알게된 사실은 spring boot는 톰캣이 내장되어있어서 내 컴퓨터에 설치된 톰캣과는 관련이 없다는것....^^(이제 이걸 까먹을 일은 절대 없을것 같다ㅎㅎㅎ)

또한 톰캣과 함께 많이 언급된건 Spring Boot버전이라서 버전을 낮추어보았는데 놀랍게도 아주 정상적으로 잘 작동했다. 하지만 매번 버전을 낮추는건 일시적인 해결일뿐이고 협업개발을 할 때 굉장히 불편하기때문에 다른 방법을 계속 찾아보았다.

<h3 id="solution">3. 문제 발생 원인 및 해결방법</h3>
결론적으로 문제는 오류내용에 나온대로 servlet문제가 맞았다. 그리고 구글링결과 많이 언급된 버전문제인것도 맞았다. spring boot가 2.0.x버전까지는 Servlet3을 사용하다가 2.1.x버전부터 Servlet4를 사용한다고 하는데 내컴퓨터의 경우 이 Servlet4를 사용하지 못한것이었다.
<br>
<b>해결법은 Java버전을 업데이트 하는것이었다.</b>
<br>
기존에 사용하던것은 `1.8.144`였는데 `1.8.211`을 받고 환경변수 설정에서 새로 받은 버전으로 설정했더니 문제없이 돌아갔다.<br>

<br><br>


#### 후기
<p style="text-color: gray">
노트북을 처음샀을때 설치한 Java로 계속 쓰고있었는데 그러한 자바에비해 IntelliJ가 너무 최신버전이라 발생한 문제였다. 항상 새로운 툴이나 기술을 사용할때는 이런문제가 가장 힘든것같다. 이 문제 하나로 거의 2주는 웹프로젝트에 손대지못했고 스트레스도 굉장히 많이 받았다. Sevlet문제가 Java와 관련이 있다는것도 이번에 처음 알게 되었다. 분명 예전에 배웠을테지만 대충만 듣고 지나가니 문제가 생겨도 관련 해결방법이 떠오르지도, 어떻게 인터넷에 찾아야하는지도 모르겠어서 기초가 중요하다는것을 다시 한번 깨닫는 계기였다.
</p>
<br>
+오류 해결해준 [용서크](https://dydtjr1128.github.io/) 넘나 고마워용;ㅁ;
 