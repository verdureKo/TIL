# .gitignore

`.gitignore`란 Git 버전 관리에서 제외할 파일 목록을 지정하는 파일이다. git으로 프로젝트를 관리할 때, 그 프로젝트 안의 특정파일들은 Git으로 관리할 필요가 없는 경우가 있다.

이번 미니프로젝트를 진행하면서 인텔리제이로 작업시 .iml파일과.idea폴더는 이클립스의 워크스페이스와 같은 파일로 컴퓨터 환경에따라 변경되기때문에 올리면 안된다는 것을 알게되었다.
지금까지는 싹다 올렸는데.. 🙄

python으로 개발할 때는 venv, NodeJS로 개발할 때는 npm module가 있고,
out 폴더엔 Java코드가 컴파일된(.class) 파일, AWS 비밀 키, JWT 비밀 키 등등이 있다.

python 가상환경과 npm 모듈은 용량이 크기도 하고, 프로젝트를 clone 받은 다음에 직접 npm install 해주는 것이 더 효율적이기 때문에 올리지 않는다. 그리고 AWS 키, JWT 비밀 키 같은 것은 Github에 public으로 노출이 되면 악용될 사레가 있기 때문에 올리지 않아야 한다.

.gitignore에 Git의 추적을 받기를 원하지 않는 이름을 적어주면 된다.

```txt
*.iml
*.idea
```

[.gitignore 파일생성 사이트](https://www.toptal.com/developers/gitignore)
기본적으로 세팅되어 있는 .gitignore에 대한 파일을 만들어주는 사이트이다.
본인이 프로젝트를 하고 있는 환경을 입력한 후에 사용하면 편리하다.
