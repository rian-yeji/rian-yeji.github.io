---
layout: post
title:  "Jekyll 로컬에서 실행하기"
date:   2019-05-09 20:45:45
author: Lee YeJi
categories: Jekyll
tags: Jekyll
comments: true
---
요즘 개발자들 사이에서 git블로그가 유행함에 따라 보다 간편하게 블로그 작성을 할 수 있도록 로컬에서 작업하는 방법을 설명한다. 

지킬 기반의 블로그를 수정할 때 커밋하지 않고도 수정사항을 로컬상에서 작업하며 확인할 수 있는데 이를 수행하기 위해서는 몇가지 설치과정을 거쳐야한다.

해당 포스팅은 Window10기반으로 작성되었다.
<hr>

<h3>1.루비(Ruby) 설치</h3>
<p>Jekyll은 Ruby 기반으로 만들어졌기 때문에 로컬에서 Jekyll을 실행하려면 선행적으로 루비가 설치되어있어야 한다.

루비 인스톨러의 다운로드 페이지에서 자신의 운영체제에 맞는 루비+개발자킷(DevKit)설치 프로그램을 다운로드 후 설치한다.</p>
<img src = "/image/Jekyll_post/ruby_install.PNG" width="200px" height="450px">
<p>별도의 설정없이 모두 기본으로 설치하였다.</p>
<br>

<h3>2.지킬(Jekyll) 설치</h3>
<p>루비 설치가 완료되면 윈도우 검색창에서 'Ruby'를 검색하여 Start Command Prompt with Ruby를 실행한다.
루비 콘솔창에서 `gem`명령어를 통해 지킬과 관련 패키지들을 설치한다.</p>
{% highlight ruby %}
> gem install jekyll
> gem install minima
> gem install bundler
> gem install jekyll-feed
> gem install tzinfo-data
{% endhighlight %}
<br>

<h3>3.로컬에서 블로그 실행</h3>
<p>루비 콘솔창에서 블로그의 깃허브 저장소와 연동된 폴더로 이동하고 지킬을 실행하면 된다.</p>
{% highlight ruby %}
> jekyll serve
{% endhighlight %}
<p>그런데 이 때 윈도우상에서는 아래와 같은 인코딩에러가 발생 할 수 있다.</p>
<img src = "/image/Jekyll_post/jekyll_error.PNG" whidth="500px" height="150px">
<p>이럴때는 다음과 같은 코드를 먼저 실행한 뒤 지킬을 실행하면된다.</p>
{% highlight ruby %}
> chcp 65001
{% endhighlight %}
<img src = "/image/Jekyll_post/jekyll_serve.PNG" whidth="500px" height="250px">
<br>
이제 브라우저에서 [http://127.0.0.1:4000/][locall-jekyll]로 접속하면 로컬상에서 블로그 구현 결과를 확인 할 수 있다.
<br>

<h3>4.수정사항 업로드(Git Kraken사용)</h3>
<p>위의 과정은 로컬에서 블로그가 어떻게 구현되었나를 확인하기 위한 방법일 뿐이므로 실질적으로 구현한 내용을 블로그에 적용시키려면 꼭 내용을 commit하고 깃허브 저장소에 push해주어야한다.</p>
<img src = "/image/Jekyll_post/jekyll_upload.PNG" whidth="800px" height="500px">
<br><br>

<hr>
참고 사이트 : [https://shryu8902.github.io/jekyll/jekyll-on-windows/][site-url]

[site-url]: https://shryu8902.github.io/jekyll/jekyll-on-windows/
[locall-jekyll]: http://127.0.0.1:4000/
