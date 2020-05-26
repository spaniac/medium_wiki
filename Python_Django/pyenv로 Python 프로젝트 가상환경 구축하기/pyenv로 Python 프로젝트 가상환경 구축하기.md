# pyenv로 Python 프로젝트 가상환경 구축하기

---

최근에 개인 프로젝트나 알고리즘 공부 등등으로 새 파이썬 프로젝트를 여러 개 만들어야 하는 상황이 생겼다. 기존에 프로젝트 버전 및 가상환경 관리를 pyenv로 하고 있었는데, 까먹고 Pycharm Professional IDE로 생성했다가 python console이 정상적으로 실행되지 않아 사용할 수 없었다. 코딩하다가 이것저것 테스트하는 용도로 python console을 자주 사용하는 나로서는 여간 불편한 게 아니었다. 그래서 상기하는 느낌으로 pyenv 사용법을 간단히 재학습하는 시간을 가졌다.

---

## 가상환경??

이전 회사에서 파이썬을 입문했을 때, 가상환경을 만들지 않으면 모든 프로젝트가 패키지를 공유하는 시스템이 자바와는 많이 달라서 어색했다. 더군다나 마이크로서비스 아키텍쳐를 구성하는 서로 다른 서버 애플리케이션들의 파이썬 버전, 패키지 리스트, 패키지 버전 등이 달라서 개발환경에서 레포지토리를 옮겨다니며 코딩하기 위해서는 가상환경이 필수였다. 이런 가상환경의 개념이 처음엔 익숙하지 않았지만, 이제는 프로젝트를 만들면서 가상환경을 먼저 생각하게 되었다.

![https://dojang.io/pluginfile.php/14099/mod_page/content/4/047005.png](https://dojang.io/pluginfile.php/14099/mod_page/content/4/047005.png)

![https://dojang.io/pluginfile.php/14099/mod_page/content/4/047006.png](https://dojang.io/pluginfile.php/14099/mod_page/content/4/047006.png)

> 이미지 출처: 파이썬 코딩도장 [https://dojang.io/mod/page/view.php?id=2470](https://dojang.io/mod/page/view.php?id=2470)

## 왜 pyenv를 사용하는지?

처음에는 virtualenv를 사용했다. 하지만 각각의 프로젝트의 파이썬 버전을 관리할 수는 없었기 때문에 불편을 겪었다. pyenv는 프로젝트 별로 파이썬 버전을 다르게 설정할 수 있기 때문에 virtualenv에서 pyenv로 갈아탔다.

---

## pyenv 설치

```
brew install pyenv
```

나같은 경우는 pyenv가 이미 설치되어 있었기 때문에 버전을 업그레이드 해주었다.

```
brew upgrade pyenv
```

---

## 가상환경 생성 경로 변경

이 상태로 사용해도 되지만, 이렇게 되면 가상환경이 생성되는 위치가 home 디렉토리의 숨겨진 디렉토리 `~/.pyenv` 에 생성이 된다. 프로젝트를 관리하는 디렉토리가 있다면 가상환경이 생성되는 위치를 프로젝트를 관리하는 경로로 변경해주면 편하다.

```
# 나는 iterm, zsh를 사용하기 때문에 해당 설정을 .zshrc 파일에 저장했다.
# Terminal을 사용한다면 .zshrc 대신 .bash_profile에 저장한다.
$ echo 'export PYENV_ROOT="$HOME/[프로젝트 관리 경로]"' >> ~/.zshrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc

# 저장 후 설정을 적용한다.
$ source ~/.zshrc

```

---

## 파이썬 설치

```
# 설치 가능한 파이썬 버전 확인
$ pyenv install --list

# 해당 버전의 파이썬 설치
$ pyenv install [버전]
# ex
$ pyenv install 3.7.2

```

---

## shell에서 실행 가능한 파이썬 버전 지정

shell에서 `python` 명령어로 파이썬을 실행하면 로컬에 다른 버전의 파이썬 설치 여부와 상관없이 항상 2.7 버전의 파이썬이 실행된다. 만약 파이썬3 버전을 설치했다면 `python3` 명령어로 파이썬3 버전을 실행할 수 있지만, 여간 번거로운 것이 아니다. 이 때, 다음 명령을 실행하면 `python` 명령어로도 지정한 버전의 파이썬을 실행할 수 있다.

```
$ pyenv global [설치된 파이썬 버전]

```

---

## 가상환경 생성

작년(2018년)에는 pyenv와 함께 가상환경을 생성하는 pyenv-virtualenv 패키지를 설치했어야 했는데, 이번에 다시 확인해보니 이 패키지가 제공하는 기능들이 pyenv에 합쳐졌다. 그래서 따로 pyenv-virtualenv를 설치할 필요가 없어졌다.

```
$ pyenv virtualenv [설치된 파이썬 버전] [생성할 가상환경명]
# ex
$ pyenv virtualenv 3.7.2 demo

```

---

## shell에서 가상환경 폴더 진입 시 자동으로 가상환경 실행

가상환경을 생성한 후 프로젝트 작업을 위해 독립적인 환경을 구축하려면 가상환경을 실행해야 한다. 하지만 가상환경을 실행/종료해야 하는 상황이 빈번히 일어나는 마당에 이 때마다 명령어를 실행하는 것이 여간 귀찮은 것이 아니다. 이런 귀찮은 문제를 다음 명령어를 통해 한 번에 해결할 수 있으며, 가상환경 경로에 진입 시 가상환경을 자동으로 실행해주기까지 한다!(이 기능을 제공하는 autoenv 패키지를 설치할 필요가 없다)

```
# 이 명령어는 프로젝트 폴더에 진입하여 실행해야 한다.
$ pyenv local [프로젝트를 포함한 가상환경명]

```

---

## 기타 명령어들

```
# 현재 파이썬 버전
$ pyenv version

# 가상환경 리스트
$ pyenv versions
$ pyenv virtualenvs

# 가상환경 삭제 및 버전 삭제
$ pyenv uninstall [파이썬 버전 or 가상환경명]
$ pyenv virtualenv-delete [가상환경명]

```

기타 명령어들을 알아보고 싶다면 `pyenv help` 또는 [https://github.com/pyenv/pyenv/blob/master/COMMANDS.md](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md)를 참고하자.