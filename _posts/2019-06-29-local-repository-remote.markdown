---
layout: post
title:  "local에서 작업한 저장소 Github에 올리기"
date:   2019-06-29 08:43:59
author: Lee YeJi
categories: Git
tags: Git GitKraken
comments: true
---
항상 Github에서 먼저 Repository를 생성하고 GitKraken으로 Clone한 폴더안에서 작업을 시작했는데 리엑트에서 MobX예제들을 따라하면서 git에 올리기 전에 로컬에 commit한 프로젝트들이 많았다.

이 프로젝트들을 깃허브에 올리려고 원래했던 방식으로 클론해서 로컬에 깃허브와 연결된 폴더를 만들고 그 안에 복붙하는 굉장히 무식한(...)방법을 사용했다.

쉽게 하고 싶어서 인터넷에 찾아봐도 시작부터 셋팅을 마치고 프로젝트를 시작하는 예제들만 설명이 되어있었다. 그래서 이것저것 그럴듯한 메뉴들을 눌러가며 방법을 찾게되었다.

막상 해보니 너무 쉽고 간단해서 이걸 포스팅해놓은 사람이 없었구나 싶다...ㅋㅋㅋ

<hr/>

### 1. Repository 생성
처음 프로젝트를 시작할 때처럼 새 저장소를 만들고 해당 저장소의 clone 주소를 복사한다.
<img src="/image/git_post/create_repository.png">

<img src="/image/git_post/copy_clone_url.png">


### 2. Remote
로컬에만 저장하고 작업한 파일을 GitKraken으로 열어보면 Remote부분이 0으로 되어있는데 이부분에 깃주소를 연결해주면 된다.
<img src="/image/git_post/gitkraken_remote.png">

<img src="/image/git_post/gitkraken_remote2.png">
Project name은 readme에 적히게 되니 적당히 본인에게 맞춰서 쓰면되고 아까 복사했던 주소를 url에 넣어주고 Add remote를 누르면 된다.


아마 처음 Pull이나 Push를 하려면 branch를 master로 할것인지 정하는게 뜨고 설정한 후 Pull/Push를 하면 처음에는 오류가 나는데 그냥 Force Pull/Push하면 아무 문제없이 연결된것을 확인할 수 있다.
