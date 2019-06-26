---
layout: post
title:  "Mobx decorator 사용 시 오류"
date:   2019-06-25 08:43:59
author: Lee YeJi
categories: ResolvedError React
tags: React MobX
comments: true
---

[velopert님의 블로그 포스팅](https://velog.io/@velopert/MobX-2-%EB%A6%AC%EC%95%A1%ED%8A%B8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90%EC%84%9C-MobX-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-oejltas52z)을 참고하여 React의 상태관리 라이브러리인 MobX를 공부하던중 decorator를 추가하는 순간부터 오류가 쏟아져내렸는데 몇몇 문제들은 인터넷을 찾아봐도 명확히 나와있는게 없었고 MobX를 사용 할 때마다 같은 상황이 벌어져서 내가 보기위한 포스팅으로 쓰게 되었다. 

하나씩 해결해 가면서 생기는 문제들을 차례대로 정리했으니 본인이 안되는 부분부터 참고하면 될것 같다. 

<hr>
[목차]
<br>
<a href="#first" text-decoration:none >1. decorator 추가 후 bulid 오류</a>
<br>
<a href="#second" text-decoration:none >2. decorator 사용 시 코드에 빨간줄</a>
<br>
<a href="#third" text-decoration:none >3. Cannot find module @babel~</a>
<br>

<h1 id="first">1. decorator 추가 후 bulid 오류</h1>
decorator를 사용하려면 babel을 수정해주어야 하는데 velopert님 블로그를 따라하다보면 "babel 설정을 커스터마이징 하려면 yarn eject 를 해야합니다."라는 말이 있고 다음과 같은 설치 명령어를 알려주고 package.json파일을 수정하는 법이 나와있다.
{% highlight PowerShell %}
yarn add @babel/plugin-proposal-class-properties @babel/plugin-proposal-decorators
{% endhighlight %}

이 과정을 모두 따라했다고 생각했는데 build 오류가 났다면 eject를 안했을 가능성이 매우 높다.

이 블로그 포스팅은 벨로퍼트님이 지필하신 책 내용의 일부인데 yarn eject를 하는 부분은 mobx보다 앞쪽 챕터에서 설명해서 이부분에서는 언급만 하고 넘어가신것 같다.

<b>yarn eject도 명령어라는 점을 명심하자!</b> 

## yarn eject
다음과 같이 command창에 yarn eject를 입력하고 실행하면 정말 eject할것인지 물어보는 부분이 나온다. 거기서 Y를 입력하면 eject가 실행되는데 이 때 아래와 같은 에러가 발생할 수 있다.

<img src = "/image/Error/react_mobx_decorator_error/eject_error.png">

이는 git commit을 하고 다시 eject하면 해결된다.

git commit을 하는 방법은 여러가지인데 벨로퍼트님이 책에 써놓으신 방법으로 해보려면 [https://liante0904.tistory.com/176](https://liante0904.tistory.com/176)를 참고하면 된다.

그런데 나는 위 포스팅대로 했을때 react-scripts 를 삭제하면서 생기는것 같은 문제들이 있어서 그냥 평소에 사용하던 GitKraken으로 로컬에 commit해주었다.

<h1 id="second">2. decorator 사용 시 코드에 빨간줄</h1>
1번의 과정을 하고 서버를 start 시키면 제대로 작동하는데 decorator를 사용한 부분에 빨간줄이 뜰 수 있다. 이는 오류는 아니고 warning의 일종인데 VSCode의 설정때문에 나타나는 문제이다. 

<img src = "/image/Error/react_mobx_decorator_error/vscode_setting_error.png" >

빨간줄이 뜨는 부분에 커서를 가져가면 다음과 같이 experimentaldecorators설정을 바꾸면 해결된다고 뜨는데 시키는 대로 하면 된다.

왼쪽 상단의 `파일>기본설정>설정`에서 experimentaldecorators를 검색하면 체크박스가 비어있는것을 볼 수 있는데 이부분을 체크하면 바뀐 설정이 적용되며 빨간줄이 사라지는 것을 볼 수 있다.

<img src = "/image/Error/react_mobx_decorator_error/vscode_setting_error2.png">


<h1 id="third">3. Cannot find module @babel~</h1>
2번까지 수행해서 프로젝트가 원활히 돌아간다! 하시는 분들은.... 정말 부럽네요.....(;^;)

무얼 해도 남들처럼 되주는 법이 없는 저는 블로그에서 시키는 대로 다 따라했음에도 갑자기 건드리지도 않은 babel안의 파일들이 문제를 일으켰습니다ㅎㅎ..

`Module build failed: Error: Cannot find module '@babel/core'` 

`Module build failed: Error: Cannot find module '@babel/plugin-transform-react-jsx-source'`

<img src = "/image/Error/react_mobx_decorator_error/babel_error.png">

위와 같이 @babel~등의 모듈을 못찾는다는 오류가 날 수 있는데 이 오류는 해당 프로젝트의 src아래의 node_modules 디렉터리를 삭제하고 <b>yarn install</b>로 다시 설치 하면 해결됩니다.


저는 여기까지 했을때 정상적으로 실행됐는데 혹시 다른 오류가 나신 분들은... 힘내세요 ^^!

제가 편하게 보기위해 정리한거지만 저와 같은 오류를 겪으신 분들께도 조금이나마 도움이 되었길바랍니다 :D
