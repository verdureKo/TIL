# GitHub . Fork Repository

먼저 Pull Request를 보내기 전 Fork한 Repository를 업데이트 싱크 해주어 최신버전으로 만들어주는게 충돌예방에 좋다

```bash
git remote add upstream https://"원본주소"
$ git remote -v
$ git fetch upstream
```

* `upstream`으로 오리지날 Remote와 연동시킨다.
* 연결이 잘됬나 확인
* 오리지날 Remote에있는 최신버전을 내려받는다.

나의 튜터님은 포크보다는 브랜치를 생성하는 것을 추천하였다.
이유는 포크레파지토리의 경우 깃 깃허브가 익숙하지 않은 경우 해결하기 힘든 충돌이 발생할 수 있기 때문이라고 한다.
