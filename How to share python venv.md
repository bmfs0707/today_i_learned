python 파일을 공유하다 보면 해당 파일을 실행하기 위한 가상환경까지 같이 공유해주어야 하는 경우가 있다. 

가상환경은 대규모 프로젝트일수록 엄청난 용량을 자랑하기 때문에 가상환경을 통으로 공유하는 것은 매우 비효율적이다. git 저장소에 올리는 것 또한 엄청난 낭비다

그럼 어떻게 해야 할까? 답은 간단하다. 공유하려는 가상환경에 설치된 패키지 명과 버전만 공유해주면 된다. pip에는 현재 가상환경에 설치된 패키지 명과 버전을 출력하는 명령어와 입력받은 패키지 명과 버전을 토대로 패키지를 설치하는 명령어가 존재한다

아래 내용에 하는 방법을 기재해두었으니 한 번 사용해보자

# How to do

- A = python venv를 공유**하는** 사람
- B = python venv를 공유**받는** 사람

A가 공유하려는 python 파일의 가상환경을 실행하고 가상환경에 설치된 모든 패키지와 버전을 txt 파일로 저장하여 txt 파일을 B에게 공유한다
```bash
source {myvenv}/script/active
pip freeze > requirements.txt
```

B는 가상환경을 새로 만들고 공유 받은 txt 파일을 `pip install`의 인자로 실행하면 A의 가상환경과 같은 가상환경이 B에게도 생긴다
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

# Comment
- 만약 공유 받은 txt 파일을 설치했는데도 module not found error가 확인될 경우
    - 공유자가 처음부터 가상환경 위에서 python 파일을 작업하지 않았을 가능성이 있다
    - 찾지 못한 module을 pip으로 수동설치하면 된다 ?? 만약 git으로 공유 받았다면 update해주자

- python은 가상환경 위에서 만드는 것이 공유하기 편하다. 패키지를 `global`로 설치하는 습관은 공유자가 생기는 순간 매우 피곤해진다.