---
layout: post
title: "pyenv 설치 및 환경 설정"
categories: "Tech"
---

Python의 version manager는 virtualenv 등이 있지만 여러모로 pyenv가 편하여 pyenv를 사용하기로 했다.
<!--excerpt-->
pyenv github을 참고하면 다음과 같은 방법으로 설치하도록 되어 있다.

```bash
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

이후 pyenv 관련 환경 변수 설정을 위해

```bash
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
```

수정 이후엔 쉘 재가동을 위해

```bash
$ exec "$SHELL"
```

모든 과정을 마쳤다면 빌드를 위한 Prerequisites 설치를 진행.

Ubuntu / Debian distro 기준

```bash
$ apt install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl
```

Python2 설치시 Openssl Library를 찾지 못하는 경우가 생기는데 다음 라이브러리를 설치해주면 된다.

```bash
$ apt install -y libssl1.0-dev
```

실행 결과 예제

```text
rita@RiTA-Xubuntu:~$ pyenv install 3.7.2
Downloading Python-3.7.2.tar.xz...
-> https://www.python.org/ftp/python/3.7.2/Python-3.7.2.tar.xz
Installing Python-3.7.2...
Installed Python-3.7.2 to /home/rita/.pyenv/versions/3.7.2
```
