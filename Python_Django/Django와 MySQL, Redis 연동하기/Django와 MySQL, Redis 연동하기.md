# Django와 MySQL, Redis 연동하기

# 개요

Django와 MySQL, Redis를 연동하는 방법을 설명한다.

# 준비

Django와 MySQL, Redis를 연동하기 위해서는 당연히 MySQL server, Redis server를 구동해야 한다. 바이너리 파일을 받아 구동할 수도 있지만, docker를 통해 두 서버를 구동하도록 하겠다.

## Docker 준비

[Get Started with Docker | Docker](https://www.docker.com/get-started)

Windows라면 위의 주소에서 Docker Desktop을 받아서 사용할 수 있다.

MacOS에서는 터미널에서 `brew install docker` 명령을 통해 쉽게 받을 수 있다.

## Docker Image 받기

설치가 완료되었다면 `docker pull mysql redis` 명령을 통해 MySQL, Redis 이미지를 받을 수 있다.

## MySQL, Redis container 구동

MySQL 이미지를 구동하기 위해서 서비스 디스커버리와 root 계정의 패스워드를 설정하기 위한 환경변수를 적용해야 한다. 그리고 MySQL의 데이터 영속성을 보장하기 위해 `-v` 옵션으로 호스트 파일 시스템을 컨테이너에 마운트해야 한다.

Redis는 별도의 계정 설정을 할 필요가 없으므로 서비스 디스커버리만 설정해주면 된다.

```bash
docker run --name mysql -p 3306:3306 --env MYSQL_ROOT_PASSWORD="password" -v ./mysql_data:/var/lib/mysql -d mysql
docker run --name redis -p 6379:6379 -d redis
```

구동한 뒤 별다른 에러가 발생하지 않았다면 `docker ps -a` 명령을 통해 잘 구동되었는지 확인할 수 있다.

![Django%20MySQL%20Redis%208d5e5998c2994550a11fb2db5631c361/Untitled.png](Django%20MySQL%20Redis%208d5e5998c2994550a11fb2db5631c361/Untitled.png)

status 탭을 통해 정상 구동 중인 것을 확인할 수 있다.

# Django 프로젝트에서 [settings.py](http://settings.py) 설정하기

`[settings.py](http://settings.py)` 에서 Django 프로젝트의 다양한 설정을 할 수 있으며, DB와 Cache 설정도 있다. 이 부분을 설정해주어야 한다.

그 전에 Django가 MySQL server와 Redis server에 접근할 수 있도록 인터페이스 라이브러리를 설치해야 한다.

```powershell
pip install mysqlclient django-redis
```

그 후 `settings.py`에서 `DATABASES`, `CACHES` 변수를 설정해주면 된다(없다면 만들면 된다).

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': '127.0.0.1',
        'PORT': 3306,
        'USER': 'root',
        'PASSWORD': 'password',
        'NAME': 'personal_blog',
    }
}

CACHES = {
    'default': {
        'BACKEND': 'django_redis.cache.RedisCache',
        'LOCATION': 'redis://127.0.0.1:6379/0',
        'OPTIONS': {
            'CLIENT_CLASS': 'django_redis.client.DefaultClient'
        }
    }
}
```

# 출처 및 참조

[docker 에 mysql 5.7버전 설치](https://www.rdf.or.kr/entry/docker-%EC%97%90-mysql-57%EB%B2%84%EC%A0%84-%EC%84%A4%EC%B9%98)

[Redis를 활용한 데이터 캐싱하기](https://nachwon.github.io/redis/)

[Django에서 Redis를 이용해 Caching하기](https://jupiny.com/2018/02/27/caching-using-redis-on-django/)