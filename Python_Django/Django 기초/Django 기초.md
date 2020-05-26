# Django 기초

# Django의 기본 작동 방식

![Django%20f9cbdf4927f14c0bb7a1333410bc7228/Untitled.png](Django%20f9cbdf4927f14c0bb7a1333410bc7228/Untitled.png)

Django는 기본적으로 MVT 패턴을 바탕으로 작동한다. 사용자가 Django 서버로 요청을 보내면 다음과 같은 과정으로 응답을 받는다.

1. View: 사용자가 요청한 URL에 해당하는 View로 요청을 전송
2. Model: 대상 객체에 대한 요청을 처리(읽기, 수정, 삭제 등)
3. Template: Model의 변경사항을 적용하여 사용자에게 html로 응답

# Django 구성요소

![Django%20f9cbdf4927f14c0bb7a1333410bc7228/Untitled%201.png](Django%20f9cbdf4927f14c0bb7a1333410bc7228/Untitled%201.png)

`django-admin startproject config`를 실행하면 Django 프로젝트가 생성된다. 그리고 `find .` 명령을 입력하면 위와 같은 구성 요소를 확인할 수 있다.

- `[urls.py](http://urls.py)`

    : 사용자가 URL로 Django에 접근을 하면 Django는 URL 규칙을 보고 내부에서 일치하는 view를 찾아 연결해준다.

- `wsgi.py`

    : Web Server Gateway Interface의 약자이며, 예전에 cgi, php의 fpm과 비슷한 Gateway Interface 중 하나다. python의 표준 Gateway Interface이다.

- `[asgi.py](http://asgi.py)`

    asgi는 django-channels와 관련된 파일이다. ASGI는 Asynchronous Server Gateway Interface의 약자이며, django-channels가 사용하고 있는 Daphne와 django-channels가 작동하는 기반이다. ASGI는 WSGI와 비슷한 구조를 가지고 있으며, 반드시 비동기 통신만을 지원하지는 않는다.

- `manage.py`

    Django의 다양한 명령어를 실행하기 위한 파일이다.

- `settings.py`

    `settings.py`는 프로젝트에 관련된 다양한 설정을 포함한 파일이다. 숨겨져 있는 기본값들을 포함한 여러 가지 설정을 할 수 있다. 기본값들은 `django/conf/global_settings.py` 파일을 참조한다.

[Python Django 기초 제 2강](https://velog.io/@vlvksbdof12/Python-Django-%EA%B8%B0%EC%B4%88-%EC%A0%9C-2%EA%B0%95)