---
layout: post
title:  "[Django] 2.Django 미니프로젝트(2)"
subtitle:   "Django 미니프로젝트(2)"
categories: Django
tags: Django
comments: true
date: 2021-07-30 00:12:00
---

'bootstrap 무료템플릿'을 검색하여 아무 템플릿이나 다운로드 받겠습니다. <br>그 폴더명은 'static'으로 바꾸어 'mysite'폴더에 넣어줍니다.
<br><br>
![static폴더](https://user-images.githubusercontent.com/55419868/127609183-35d7b0c9-cf79-4e1c-8aed-aa14084fb710.JPG)

<br>
받은 템플릿에서 `index.html` / `css` / `js` 이것들이 있는지 확인해주시면 됩니다. 

`static` 폴더 안의 `index.html` 내용을 전부 복사하여 main > templates > main > index.html 에 붙여넣어 주겠습니다.  <br><br>
서버를 열어 확인해보시면 html이 적용된 것을 확인할 수 있습니다.

![html적용](https://user-images.githubusercontent.com/55419868/127609474-ef4baa28-7a72-48eb-bbce-433899dbd5de.JPG)

<br>
그러나 css와 js가 적용되지 않아 글자만 이렇게 나타납니다. 
<br> 

```
{% load static %}
```
`index.html` 파일 맨 위에 위의 코드를 적겠습니다. <br>static 폴더를 가져올 수 있게됩니다. <br><br>

```
<link href="css/styles.css" rel="stylesheet" />
```

```
<link href="{% static 'css/styles.css' %}" rel="stylesheet" />
```

`static` 폴더 안의 파일에 링크가 걸려있는 것들을 수정해줍니다.<br>
 `"{% static '' %}"` 이렇게 수정해주어야 제대로 인식할 수 있습니다.

 ```
 # settings.py 입니다.

STATIC_URL = '/static/'
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```

`static` 을 제대로 읽을 수 있도록 `settings.py` 에서 설정을 해주어야 합니다.<br>
`STATIC_URL`은 원래 있던 것이고, 그 아래 `STATICFILES_DIRS` 코드를 작성해줍니다. <br><br>
이제 서버를 작동시켜보면 제대로 `static` 폴더 안까지 적용시킨 것을 확인할 수 있습니다.

![css 적용 후](https://user-images.githubusercontent.com/55419868/127611279-8eba7aec-fce7-4175-af0b-447c88d981c8.JPG)
<br><br>
그런데 혹시 `'os' NameError`가 나타나신다면 `os`함수가 없는 것입니다.
`settings.py` 파일 맨 위에 

```
import os
```
이 코드를 작성해주세요.

<br><br>

<h1>4. models.py </h1>

```
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=50)
    contents = models.TextField()
    img = models.ImageField()
    dataCreat = models.DateTimeField()
    category = models.CharField(max_length=20)
```
<br>

`models.py` 에 사용하고자 하는 모델들을 변수로 넣어주겠습니다.<br>
무슨무슨 `Field` 하는 것들은 'Django medel field' 사이트에서 확인하시면 됩니다. <br>
당장은 정확히는 몰라도 직관적으로 받아들이겠습니다. <br>
`DateTimeField()` 라면 날짜를 뜻하겠죠?
<br><br>
그런데, 서버를 작동시키면 에러가 발생합니다.

```
ERRORS: main.Post.img: (fields.E210) Cannot use ImageField becuase Pillow is not installed.
```
해석해보면, `Pillow` 를 설치하라는 뜻이군요!<br>
설치해주겠습니다.

```
pip install pillow==2.9.0
```
터미널에 버전까지 명시해서 입력하겠습니다. 
<br>(최신버전은 에러나 나는 경우가 있다고 들어서, 옛버전으로 설치했습니다)

<br>
이제 만든 DB(Data Base)를 적용시켜야 합니다.

터미널에 명령해줍니다.
```
python manage.py makemigrations
```
<br>
migrations 폴더를 확인해 보면 여러 파일들이 생성된 것을 확인하실 수 있습니다.<br><br>

![migration 폴더](https://user-images.githubusercontent.com/55419868/127617890-7fec53af-3b12-4f30-a8d5-8bda570d3b44.JPG)


(원래는 migrations 폴더가 비어있었습니다.)

이제 DB를 적용시켜줍니다.
```
python manage.py migrate
```
이것으로 `models.py`에 만든 DB가 적용되었습니다.
<br><br>
이제 admin(관리자)페이지에 들어가서 제대로 적용이 되었는지 확인해 봅시다.<br><br>
우선 관리하는 슈퍼계정을 만들어줍니다.

```
python manage.py createsuperuser
```
입력하시고, 순서에 따라 name, e-mail, password를 입력하시면 계정이 생성됩니다.<br><br>

admin 페이지에 적용시키기 위해 `admin.py` 파일에 들어갑니다.

```
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```
`models`의 `Post`가 등록되었습니다. <br><br>

서버에 접속하셔서 주소창 뒤에 /admin 을 붙여주면 관리자 페이지에 들어갈 수 있습니다.
```
https://django-mini-project-sdzm.run.goorm.io/admin
```

![admin 로그인](https://user-images.githubusercontent.com/55419868/127618691-d0c01a3f-b1a5-4016-bcf5-e78dc35cf24a.JPG)

로그인을 해주시면

![Post](https://user-images.githubusercontent.com/55419868/127619322-9b39fd15-6a8d-442d-beb5-23a62dcee340.JPG)

Post가 생긴 것을 확인할 수 있습니다.<br>
Add를 눌러주세요.

![add post](https://user-images.githubusercontent.com/55419868/127619485-d12d2698-003c-45b9-acfb-e224b055a50b.JPG)

<br>

저희가 `models.py`에 적은 `Field`들이 있는 것을 확인하실 수 있습니다.<br>
적당히 내용을 입력하고 저장하겠습니다.

![Post object](https://user-images.githubusercontent.com/55419868/127619934-0cbc75d1-0236-46c0-888b-c6c99e26e8ba.JPG)

Post object(1) 이 생성되었습니다.<br>
제가 원하던 title이 아닙니다.

`models.py` 의 `Post` class 안에 함수를 넣어주겠습니다.

```
def __str__(self):
        return self.title
```

![title1](https://user-images.githubusercontent.com/55419868/127621112-50d489c6-67cc-4e33-8bc2-a8c2909501a6.JPG)

제가 원하던 title으로 변경되었습니다.<br><br>

그런데 `1.jpg`가 `mysite` 폴더에 덩그런히 저장됩니다. <br>
저장되는 폴더를 지정해주겠습니다.

```
# settings.py
MEDIA_ROOT = os.path.join(BASE_DIR, 'postImg')
MEDIA_URL = '/postImg/'
```
`settings.py` 에 이미지가 저장되는 폴더(postImg)를 만들어주었습니다.<br><br>

관리자페이지에서도 이미지를 볼 수 있도록 설정하겠습니다.
```
# urls.py 

from django.conf.urls.static import static
from django.conf import settings

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

`urls.py`에 위 코드들을 추가시켜 줍니다.<br>
 이제 이미지가 제대로 된 url을 가지면서 페이지에서 이미지를 확인하실 수 있습니다. <br><br>

 `index.html`에 7개의 POST들을 적용시켜 보겠습니다.

 ```
 <div class="row g=0">
    <div class="col-lg-4 col-sm-6">
    <div class="col-lg-4 col-sm-6">
    <div class="col-lg-4 col-sm-6">
    <div class="col-lg-4 col-sm-6">
    <div class="col-lg-4 col-sm-6">
    <div class="col-lg-4 col-sm-6">
 ```
 전체 코드는 아닙니다! 페이지에서 이미지가 6개 모여있는 부분의 코드를 발췌했습니다.

 ![이미지 깨짐](https://user-images.githubusercontent.com/55419868/127630297-35dd629a-4daf-420c-b914-fd7773dad802.JPG)

코드에서의 이미지의 주소와 실제로 이미지가 들어있는 주소가 달라서 깨져있습니다.<br>
저희가 POST에 입력한 이미지대로 이미지가 나타나도록 해보겠습니다.

```
<div class="col-lg-4 col-sm-6">
    <a class="portfolio-box" href="assets/img/portfolio/fullsize/1.jpg" title="Project Name">
        <img class="img-fluid" src="assets/img/portfolio/thumbnails/1.jpg" alt="..." />
        <div class="portfolio-box-caption">
            <div class="project-category text-white-50">Category</div>
            <div class="project-name">Project Name</div>
        </div>
    </a>
</div>
```

```
{% for post in postAll %}
<div class="col-lg-4 col-sm-6">
    <a class="portfolio-box" href="{{post.img.url}}" title="Project Name">
        <img class="img-fluid" src="{{post.img.url}}" alt="..." />
        <div class="portfolio-box-caption">
            <div class="project-category text-white-50">{{post.category}}</div>
            <div class="project-name">{{post.title}}</div>
        </div>
    </a>
</div>
{% endfor %}
```
`for`문을 이용해 일일이 6개씩 이미지를 입력하던 것을 반복문으로 만들었습니다.
`href` / `src` / `Category` / `Project Name`을 수정했습니다.<br>
`{{}}` 을 찾으시면 됩니다.<br><br>
그 외에도 전체코드에서 `src` 주소가 입력된 부분은
```
<script src="{% static 'js/scripts.js' %}"></script>
```
이런 식으로 `{% static '' %}`을 추가 해주었습니다.<br><br>

이제 서버로 들어가 확인해보겠습니다.
![이미지 7개](https://user-images.githubusercontent.com/55419868/127632377-3638e162-7666-4fb8-be47-b1ea3c6129dd.JPG)
7개의 POST가 정상적으로 들어간 것을 확인할 수 있습니다.

