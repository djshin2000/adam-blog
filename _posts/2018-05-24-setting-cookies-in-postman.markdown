---
layout: post
title:  Postman에서 Cookie 설정하기 (with Session-Id)
date:   2018-05-24 01:00:00 +0300
description: # Add post description (optional)
img:  2018-05-24-postman-bg-01.png # Add image post (optional)
tags: [postman, cookies, sessionid, bug, error]
author:  # Add name author (optional)
---
```
[환경정보]
OS: ubuntu 16.04 LTS / 64-bit
Postman: linux-x64-6.1.2
```
<br>
<br>
# Intro
**Postman** 을 이용하여 request를 보낼 때 **FastCampus WPS 수업** 에서는 token을 이용하여 사용자를 인증하는 방법을 배웠는데,
우리 회사에서는 `token`이 아닌 `session id`를 이용하여 사용자를 인증한다. (아놔! ㅡㅡ;)

그래서 **Postman** 에서 **session id** 를 설정하는 것을 포스팅하고자 한다.

사실 [Postman 공식문서][postman-cookie]에 설명이 되어 있기는 한데 `쿠키(cookie)`가 무엇인지 잘 모르는 상태에서는 이해가 쉽지 않고, 미래의 나를 위해 이 글을 작성하는 한다.
그리고 cookie 설정 시 **버그** 로 인해 고생하여 버그 내용도 함께 작성한다.
<br>
<br>
<br>
<br>

# Cookie 설정
## 'Manage Cookies' 모달창 열기
**send** 버튼 아래 **Cookies** 링크를 클릭한다.

![open 'manage cookies' modal][img1]
<br>
<br>
## Domain 입력하기
상단의 text 입력창에 Domain을 입력하고 **Add** 버튼을 클릭하면 하단의 도메인 리스트에 추가된다.
> (주의)도메인 입력시 **port** 나 **http://** 를 입력하면 안된다.



![add domain][img2]
<br>
<br>
## Cookie 생성하기
생성한 도메인에 Cookie를 추가하려면 **Add Cookie** 버튼을 클릭한다. 하단 입력창에 **HTTP State Management** 표준에 따라 쿠키 문자열이 생성된다.
> [Bug] 여기서 UI가 매우 불친절한(?) 버그가 있다. 다음과 같이 도메인에 **port** 를 같이 입력하면 **Add Cookie** 버튼이 동작하지 않는다. `예시) localhost:8000`

> [postman issue report 바로가기][bug-report]

![create cookie][img3]
<br>
<br>
## Session Id 입력하기
쿠키 문자열 편집창에 아래와 같이 수정한 후 **save** 버튼을 클릭하여 변경된 내용을 저장한다.
```
sessionid={세션아이디 문자열}; path=/; domain=localhost;
```
<br>
<br>
<br>
<br>
> reference

> Postman 공식문서 : https://www.getpostman.com/docs/v6/postman/sending_api_requests/cookies
> Postman GitHub : https://github.com/postmanlabs/postman-app-support/issues/3518

[postman-cookie]: https://www.getpostman.com/docs/v6/postman/sending_api_requests/cookies
[img1]: https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/58524551.png
[img2]: https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/WS-manage-cookies-3.png
[img3]: https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/WS-manage-cookies-2.png
[bug-report]: https://github.com/postmanlabs/postman-app-support/issues/3518
