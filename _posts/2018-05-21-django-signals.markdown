---
layout: post
title:  django에서 signals.py 생성 시 설정
date:   2018-05-21 12:01:01 +0300
description: # Add post description (optional)
img:  post-6.jpg # Add image post (optional)
tags: [Python, Django, Signals]
author:  # Add name author (optional)
---

Django 1.7 이상에서는 아래와 같이 적용
-------------

- Django에서 signals.py를 생성할 때 아래와 `apps.py` 파일에 `ready()` function을 생성해야한다.

```
# apps.py
from django.apps import AppConfig

class MyAppConfig(AppConfig):
    name = 'my_app'

    def ready(self):
        import my_app.signals
```
그리고, `__init__.py` 파일에 아래와 같이 작성한다.
```
# __init__.py
default_app_config = 'my_app.apps.MyAppConfig'
```
&nbsp;
&nbsp;
&nbsp;

Django 1.6 이하에서는 아래와 같이 적용
-------------

`__init__.py` 파일에 아래와 같이 작성한다.
```
import signals
```
