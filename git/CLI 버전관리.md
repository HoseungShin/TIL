# CLI 버전관리



## 3. 버전관리의 시작

- git 버전관리를 맡길 폴더를 생성



### 등장 명령어 정리

- `mkdir[파일명]`
- `pwd`
- `ls -al`
- `cd`



### git init

​	```Initialized empty Git repository in C:/Users/shs94/git_basic/.git/```

- 대상 폴더에서 `git int` 입력하면 그 폴더가 깃 폴더가 되는 것.

- 버전 정보들이 git 이라는 디렉토리 안에 파일에 적당히 저장된다.

- 절대 `.git` 을 지우면 안됨. 프로젝트의 역사가 사라지는 것.





## 4. 버전의 생성

| Working tree       | Staging area                | Repository    |
| ------------------ | --------------------------- | ------------- |
| 파일을 수정하는 곳 | 버전을 만들려고 하는 파일들 | 만들어진 버전 |



### 등장 명령어 정리

- `nano [파일명]` : `[파일명]` 의 관리 툴(?) 같은 곳으로 들어가서 뭘 작성하고 그럼
- 위에서 기본 에디터는 vim -> 강의자가 nano로 바꾼 것
- `cat [파일명]` : `[파일명]` 의 내용을 출력 



### git status

- Read

​	앞으로 깃에서 가장 많이 사용하게 될 명령어. 지금 상태가 어때? 하고 물어보는 것.



### git add [파일명]

- Working tree의 파일을 Staging area로 보내는 명령어.

- 이후 git status를 하면

  warning: LF will be replaced by CRLF in hello1.txt.
  The file will have its original line endings in your working directory

  

### git commit -m "들어갈 내용"

- git commit 까지만 입력하면  기본 editor가 떠서 직접 수정이 가능함.  :q로 탈출 가능.

- Staging area 에 있던 파일이  Repository로 이동

- 이후 git status를 하면

  ```[master (root-commit) 088cf35] Message 1 
  [master (root-commit) 088cf35] Message 1
   1 file changed, 1 insertion(+)
   create mode 100644 hello1.txt
  ```

  

### git log

- Read

- 역사를 보고싶다라고 명령
- commit 이후에 git status 를 확인하면 

	commit 088cf35ec55e39548e40a58b5330ba935b6a27c1 (HEAD -> master)
	Author: Hoseung Shin <shincharito@naver.com>
	Date:   Thu Apr 8 16:37:02 2021 +0900




## 5. 버전간의 차이점 비교

### git diff

- 마지막 버전과 Working tree 사이의 차이점을 파악하도록 도움.
- 버전을 만들기 전에 반성을 하고 검토를 할 기회를 줌.



### git reset --had

- Working tree에서 작업했던 내용 전부 사라지고 마지막 버전 불러옴
- 과거를 불러올 수 있다는 것이 매우 큰 효용

```HEAD is now at 432276b Message 2```



### git log -p

- 버전 기록들을 모두 살피며 각 commit 에서 무엇이 추가되었는지를 보여줌
- 문서 상에서 문제가 생겼을 때 어디에서 문제가 생겼는지를 파악하는 데 용이



비교를 할 수 있고, 의사결정을 하는 데 많은 도움을 얻을 수 있다의 이점을 기억할 것.



### CRUD

Create : 버전을 만들고

Read : 버전을 보고 - `git status`, `git log`

Update : 버전을 수정하고

Delete : 버전을 삭제하는 것





## 6. Checkout 과 시간 여행

### git checkout [commit 로그]

- (HEAD)를 과거의 특정 시점으로 옮기는 것

- 마우스 이용해서 로그를 copy 하고 마우스 이용해서 git checkout 뒤에 붙여 넣으면

```Note: switching to '088cf35ec55e39548e40a58b5330ba935b6a27c1'.
Note: switching to '088cf35ec55e39548e40a58b5330ba935b6a27c1'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 088cf35 Message 1


```

- 그리고 그 시점으로 회귀하게 됨



### git checkout master

- 다시 최신 상태로 복귀됨

  ```Previous HEAD position was 088cf35 Message 1
  Previous HEAD position was 088cf35 Message 1
  Switched to branch 'master'
  ```





## 7. 보충수업

### git add .

- `git add [파일명]` 말고 `git add .` 을 적으면 그 디렉토리 안의 모든 새로운, 변경된 파일을 Staging area로 보냄



### git commit -am "commit의 이름"

- 한 번에 add 와 commit 이 진행됨
- 하지만 주의할 점이 있음. 최초 한 번은 add가 되어서 tracked 상태가 돼야지만 그 파일을 자동으로 추가함
  - 추적하고 싶지 않은 파일이 실수로 추적되는 사고를 방지할 수 있게 됨





## 8. 버전 삭제 - git reset

- `git reset --hard [버전 로그]` : 가장 강력하게 지우는 것
- 만약 버전만 지우고 작업하는 것은 살리고 싶다 하면 --뒤에 soft 같은걸로 바꿔서 사용 가능
- git reset help 로 입력해서 여러가지 명령을 확인할 수 있음
- 해당 버전 로그를 리셋하겠다가 아니라, 그 로그로 가겠다의 의미





## 9. 버전 되돌리기 - git revert

- 모든 시스템이 CRUD를 지원하는 것은 아님
- revert를 이용하면 삭제의 목적과 보존의 목적 두 가지를 모두 다 만족시킬 수 있음

- reset의 매커니즘과 다르게, 내가 남기고 싶은 것보다 한 단계 뒤의 버전에서 revert를 해야 원하는 것이 남음

- 기존의 commit은 두고, 그 commit 에서의 변화를 취소한 것이다. 그래서 오히려 git log 했을 때 한 개가 늘어나 있음.