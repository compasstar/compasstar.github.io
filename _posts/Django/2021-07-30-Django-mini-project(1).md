---
layout: post
title:  "[Django] 2.Django 미니프로젝트(1)"
subtitle:   "Django 미니프로젝트(1)"
categories: Django
tags: Django
comments: true
date: 2021-07-30 00:12:00
---

<h3>Django 미니프로젝트를 만들어 보겠습니다.</h3>
<br>
<i>기본세팅은 이전 포스팅에서 확인해 주세요</i>
<br><br>
순서는 아래와 같습니다. <br>
1. urls.py <br>
2. views.py <br>  
3. main > templates > main > index.html <br>
4. models.py <br>
<br><br>

<h1> 1. urls.py </h1>
<hr>
간단하게 말하자면, 사이트의 주소에 대한 설정입니다.

```
"""landingpage URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/3.2/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

처음 들어가면, 이렇게 복잡한 코드를 보실 수 있습니다. <br> 주석은 다 제거하고 시작하겠습니다.

```
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

요렇게 입력해주겠습니다.
```
from django.contrib import admin
from django.urls import path
from main.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', index),
]
```
`views` 에서 `index`라는 함수를 가져왔습니다. (`index`함수는 `views.py`에서 만들어 주겠습니다.) <br>`path`를 추가하여 본연의 페이지를 `index`와 연결했습니다. <br> <br>
페이지 주소를 입력하면 `index`가 보이게 되고, 주소 뒤에 `/admin`을 적어주면 관리자 페이지에 접속하게 됩니다. 
<br><br>

<h1>2. views.py</h1>

```
from django.shortcuts import render

def index(request):
    return render(request, 'main/index.html')
```
<hr>

`index.html`을 제공하는 함수입니다.<br> `index`라는 함수는 `urls.py`로 `import` 되어 기본 주소에서 실행하게 되었습니다. <br>
이제 index.html을 만들어 보겠습니다.
<br><br>

<h1> 3. index.html </h1>

main > templates > main > index.html 
순서로 만들어줍니다.<br>
`index.html`만 파일이고, 나머지는 폴더입니다.<br> 전부 직접 만들어주셔야 합니다.
<br>

![index html 디렉토리](https://user-images.githubusercontent.com/55419868/127595163-561afd77-9534-46ea-8678-abb45ba1e9fa.JPG)

```
# index.html

hello world
```

`index.html` 에 `hello world` 라고 적고 서버를 작동시키겠습니다.

![hello world](https://user-images.githubusercontent.com/55419868/127607620-e4a63552-7905-4a94-ad91-eca0c712108a.JPG)

사이트에서 반겨주는 것을 확인 할 수 있습니다.<br><br>

<hr>

기본적인 토대는 여기까지 입니다.<br>
다음 포스팅에서는 템플릿을 가져와서 사이트를  꾸며보겠습니다.