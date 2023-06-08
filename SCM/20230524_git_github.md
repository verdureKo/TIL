# SCM (Software Configuration Management)

- SCM (Software Configuration Management) ?
 `형상관리`, `버전관리` 라고 한다.

- 버전관리 소프트웨어 ?
 `Git`, `Subversion`, `CVS` 등이 있다.

- 원격 협업 및 파일 저장 서비스 ?
  `Github`, `Gitlab`, `Bitbucket` 등이 있다.

- Github ?  
 대표적인 무료 클라우드 Git 저장소. 2008년부터 서비스가 시작되었고 Git 호스팅 기능 덕분에 `GitHub` 는 자유 소프트웨어와 오픈소스의 성지로 떠올랐다.

## Git

- 다운로드
  - [Git 윈도우](https://git-scm.com/download/win) 또는 [Git For Windows](https://gitforwindows.org/)
  - [Git Tutorial](https://git-scm.com/book/ko/v2)
  
- 설치
  - Git 편집기 선택 → 기본 선택 VIM (`VisualStudioCode`가 편리하다)
  - PATH 환경설정
    - Use Git from Git Bash only : Git Bash에서 Git command line tools만 사용 가능
    - Git from the command line and also from 3rd-party software : Git Bash와 cmd에서 Git 사용 가능
- 기타옵션 설정
  - Enable file system caching : 성능 향상을 위해 파일 시스템 데이터를 메모리에 캐시
  - Enable Git Credential Manager : Windows용 Git 보안 자격증명 저장소를 사용하기 위해 Git Credential Manager 활성화
  - Enable symbolic links : Symbolic links 사용

## Command Prompt

```bash
  $ 커맨드라인 명령어
  # git은 #이후 문자로 시작하는 줄을 주석줄로 처리
```

- git 버전확인

```bash
  git --version
```

- git 설정확인

```bash
  git config --list
 ```

- git 초기화(.git 폴더 생성, 버전관리 시작)

```bash
  $ git init
  # Initialized empty Git repository in ...
```

- `.git` 폴더 확인 (.git 폴더가 숨겨져 있을 경우, 보기탭 - "숨긴 항목" 크하면, 숨겨져 있는 .git 폴더가 보여짐)
- Git 처음 설치시 이름과 메일 설정함. `global 옵션`으로 초기 한번 설정
- 해당 시스템에서 해당 사용자가 사용할 때 이 정보를 사용
- 만약 프로젝트가 다시 시작될 경우, 다른 이름과 이메일 주소를 사용하고 싶으면

- 만약 name, email 을 바꾸고 싶다면 바꿀 내용만 다르게하여

```bash
  git config --global user.name "name"
  $ git config --global user.email "gmail@gmail.com"
```

- git config 설정 확인

```bash
  git config --list 
```

- git 사용 안내, 명령어 잊어버렸을때 알 수 있음

```bash
  git help  
```

- 저장소 폴더 내 전체 파일을 워킹디렉토리에서 스테이징으로 올려보냄

```bash
git add -A 
```

- 신규, 변경된 파일 모두를 add 처리함

```bash
git add . 
```

- index.html 파일만 워킹디렉토리에서 staging area로 보냄

```bash
git add index.html
```

- index.html 파일이 Repository로 보내지며, -m 식별 메시지 "first commit"로 구분

```bash
git commit index.html -m "first commit"
```

- 저장소 폴더 내부 변화 상태(status) 확인

```bash
git status 
```

- git log 기록 확인(일련 번호 등)

```bash
git log 
```

## **reset** vs **revert**

작업을 진행하다가 실수로 중요한 파일을 삭제했거나 제대로 병합이 안됐을 경우, 잘 작동이 되던 이전 버전으로 돌아가야 한다. 이것이 바로 버전 관리를 하는 이유이며, 이 때 사용하는 명령어가 `git reset`과 `git revert` 명령어이다.

- [`reset --mixed`] : commit / index 재설정. 아무것도 지정하지 않으면 --mixed 된다(default)

```bash
git reset (돌아갈 커밋의 log 일련번호 앞 6자리 or log 다써도됨) --mixed 
```

- [`reset --soft`]옵션 : 커밋을 제외하고 reset 되는 상태이며 내용은 유지된다.

```bash
git reset (돌아갈 커밋의 log 일련번호 앞 6자리 or log 다써도됨) --soft 
```

- [`reset --hard`] : commit / index / 작업 트리 모두 재설정 --hard 옵션은 내코드 뿐만아니라 타인의 코드 모두 reset 되기 때문인데 복구하는 방법을 알고있고 깃에 능숙해지기 전까지 사용하지 말아야한다. reset 대신 revert(이력을 그대로 두고 되돌리기)를 사용할 수 있다.

```bash
git reset (돌아갈 커밋의 log 일련번호 앞 6자리 or log 다써도됨) --hard 
```

> 깃노예 실습창

```bash
  C:\gitTest>git log
  commit 0eb1e9ea65860e434e90fb698b5f993fcfe6819a (HEAD -> master)
  Author: verdureKo <verdure.ko@gmail.com>
  Date:   Mon Mar 22 19:21:03 2023 +0900
  second commit
```

```bash
  C:\gitTest>git revert 0eb1e9
  # 현재 기록 연계 앞전 상태로 돌아가기, commit 이력들은 그대로 유지 됩니다.
  commit bc6cce643a391d70ca4d46c0f6324d6c84b5472f   
  Author: verdureKo <verdure.ko@gmail.com>    
  Date:   Mon Mar 22 19:20:11 2023 +0900    
  first commit
```

실행 창 닫고, git log 명령어 실행 확인

```bash
  C:\git_test>git log   
  commit 0eb1e9ea65860e434e90fb698b5f993fcfe6819a (HEAD -> master)    
  Author: verdureKo <verdure.ko@gmail.com>    
  Date:   Mon Mar 22 19:21:03 2023 +0900    
  second commit
```

```bash
  C:\git_test>git reset 0eb1e9e --hard 
  commit bc6cce643a391d70ca4d46c0f6324d6c84b5472f   
  Author: verdureKo <verdure.ko@gmail.com>
  Date:   Mon Mar 22 19:20:11 2023 +0900
  first commit
```

reset 복구 = reflog 실행 기록 확인 후 reset 복구

```bash
  C:\git_test>git reflog
  572917c (HEAD -> master) HEAD@{0}: reset: moving to 572917c526f004fbbc8dba87f3be27405eb8ddeb    
  da2a2c5 HEAD@{1}: commit: third commit    
  2a82323 HEAD@{2}: commit: second commit   
  572917c (HEAD -> master) HEAD@{3}: commit (initial): first commit
```

reset --soft/mixed/hard 후에 복구는 reflog를 사용

```bash
  C:\git_test>git reset --hard head@{2}
  # second commit 으로 reset 가능함
  HEAD is now at 2a82323 second commit
```

github.com 원격(remote) 리포지토리 연결하려고 하면, `Verification` 자격 증명하라는 팝업이 뜨는데 등록한 메일에서 Verification Code를 입력하면 된다.
그러면 Windows에 "자격 증명 관리"에 Windows 자격 증명 들어가면 자격 증명들이 생성되기 시작함.
처음 만들면 안뜨는데, 이미 만든 사람은 처음 인증 PC와 다른 PC에서 사용하기 때문에 Verification Code 입력을 해줘야 한다.
(일반 자격 증명 - Github 등록하면 자격 증명이 하나 등록됨)
(개인 PC가 아니면 github 자격 증명 모두 제거 후 나와야 한다.)

- git branch (새 브랜치명) # 현재 master branch 와는 별도로 새로운 branch 생성

- git branch # 로컬 PC branch 리스트 확인

- git checkout (브랜치명) # 특정 브랜치로 이동

- git branch -D (삭제할 브랜치명)  # 브랜치 삭제

- git branch # branch 현황 확인

- Git 참고 웹 사이트

  - [Git 공식 홈페이지](https://git-scm.com/)
  - [Git ignore 파일](https://www.gitignore.io/)
  - [Git ignore 템플릿](https://github.com/github/gitignore)

## Git 을 VSCode에서 사용 시

  "용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증 후 다시 시도하십시오." 메시지가 나타날 경우 해결 방법 : "powershell" 모드로 되어서 나타나는 에러

- 문제 해결 방법

  - 이 기본 터미널의 종류를 `cmd` 또는 `Git Bash` 로 변경하면 오류없이 실행이 가능

  - 먼저 `Ctrl + Shift + P` 를 누르면 `Command Palette` 가 열림

  - 입력란에  `Terminal: Select Default Shell` 을 입력 후 항목들 중에서 `Command Prompt` 또는 Git `Bash`를 선택
  - 변경 후 Terminal을 닫았다가 새로 Terminal을 열거나 다시 실행하면 조금 전 내가 선택한 터미널의 종류로 열리게 되고 이상없이 가상환경이 실행되어 오류가 나지 않는다.

## Git을 eclipse에서 사용 시 환경 설정

- Eclipse에서 Git을 선택, 우측 상단에 돋보기를 클릭하거나, Ctrl + 3 을 실행해서 git을 선택

- 프로젝트 선택 후 마우스 우클릭 [Team] → [Share Project] 클릭해서 저장소(Repository)를 생성(Configure Git Repository 창에서 Create 버튼 클릭 - Project 선택 체크 - Finish 버튼 클릭 : .git 폴더가 생성됨)

  - git 키워드 입력 후 Git Repositories 선택하면, 다음의 Git Repositories Select 명령문들이 나타납니다.
  Add an existing local Git repository: PC(Local)에 저장되어 있는 소스를 추가함
  Clone a Git repository: 이미 존재하는 Git repository를 복제함
  Create a new local Git repository: 새로운 Repository 생성함

  - Github에 대한 정보를 입력합니다. URL, User ID, User Password 를 알고 있어야 합니다.

  - branch를 선택합니다. branch가 아직 master만 있다면 master로 설정합니다.

  - 선택을 완료하면 입력 정보를 확인 한 후 Finish를 합니다. Git repository 에 저장된 파일이 정상적으로 복제 되었는지 확인합니다.

  - 커밋을 적용할 경우, 프로젝트 선택 후 마우스 우클릭 - Team - Commit 을 선택합니다.

  - Commit Message 항목에 알맞은 메시지 작성한 후 "Unstaged Changes"에 있는 파일들을 "Staged Changes"로 옮겨줍니다. commit 버튼을 클릭 실행합니다.

  - 우측 상단 JAVA EE 아이콘을 클릭하면 JAVA EE 프로젝트 화면이 나타나고, GIT 아이콘을 클릭하면 .git 폴더가 있는 프로젝트 GIT 상태 화면이 나타납니다.

## Local repository - Github repository 연동 시

- Local repository origin master branch - Github repository master branch
  Local master 브랜치와 Github master 브랜치 Sync 여부 체크

- 예를들어, Local repository origin a branch - Github repository a branch 라고 했을때
  Local a 브랜치와 Github a 브랜치 Sync 여부 체크

## 협업시 순서 : Fetch  →  Pull  →  Push  →  Merge Requesting

먼저 Fetch(가져오기)로 문제 없는지 검사하고, 그 다음에 Pull(가져와 병합하기)로 데이터를 가져온 후, 마지막에 Push(밀어넣기)
