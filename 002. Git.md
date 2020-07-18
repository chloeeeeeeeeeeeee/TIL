# Git

> Git은 분산버전관리시스템(DVCS)이다. `Distributed Version Control System` 
>
> 소스코드의 버전 및 이력을 관리할 수 있다.





## 준비하기

윈도우에서 git을 활용하기 위해서 git bash(CLI)를 설치한다.
	:bulb:`MAC은 기본적으로 git을 가지고 있다.`



git을 활용하기 위해서 GUI 툴인 `source tree`, `github desktop` 등을 활용할수도 있다. 
	:bulb:`자신의 데스크탑에는 GUI를 최적화하여 사용할 수도 있지만, 어떤 컴퓨터 환경을 사용하게 될 지 모르므로, CLI로 작업하는 훈련을 해두는 것이 좋다.`



초기 설치를 완료한 이후에 컴퓨터에 author 정보를 입력한다. 

```bash
$ git config --global user.name {user name}
$ git config --global user.email {user email}
```





## 로컬 저장소(repository) 활용하기

### 1. 저장소 초기화

```bash
$ git init 
Initialized empty Git repository in C:/Users/{사용자 이름}/{폴더 이름}/.git/
```

* `.git` 폴더가 형성되며, 여기에 git과 관련된 모든 정보가 저장된다.
* git bash에 `(master)` 라고 표시되는데, 이는 현재 폴더가 git으로 관리되고 있다는 뜻이며, `master` branch에 있다는 뜻이다.
  :bulb:`branch : 소스코드에 새로운 기능을 덧붙일 때, 원본은 남겨두고 가지치기를 하며 새로운 버전을 시도할 수 있다.`



### 2. `add`
`working directory`, 즉 작업공간에서 변경된 사항을 이력으로 저장하기 위해서는 반드시 `staging area`를 거쳐야 한다. 

```bash
$ git add {파일/폴더}
$ git add markdown.md 	# 파일
$ git add images/		# 폴더 (이름 뒤에 /가 붙는다)
$ git add .				# 현재 디렉토리
```

​	:bulb: `$ git add . 을 실행할 시 현재 디렉토리에 있는 모든 파일과 폴더를 staging area로 올린다`



* markdown.md 파일이 폴더에 새롭게 작성되었으나, 아직 git으로 관리되지 않고`add` 되기 전 상태 

  ```bash
  $ git status
  On branch master
  No commits yet
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
          markdown.md
  nothing added to commit but untracked files present (use "git add" to track)
  ```

* markdown.md 파일이 add 후에 `staging area`로 올라간 상태

  ```bash
  $ git status
  On branch master
  No commits yet
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   markdown.md
  ```



### 3. `commit`

commit은 **이력을 확정짓는 명령어**로, 해당 시점의 스냅샷을 기록한다.
커밋시에는 반드시 메시지를 작성해야 하며, <u>메시지는 변경사항을 알 수 있도록 명확하게 작성한다.</u>

```bash
$ git commit -m "마크다운 정리"
[master (root-commit) 6c84015] 마크다운 정리
 1 file changed, 170 insertions(+)
 create mode 100644 markdown.md
```

커밋 이후에는 아래의 명령어를 통해 지금까지 작성된 커밋 이력을 확인한다.

```bash
$ git log 
commit 6c840158f44a51f40c02f08d226289d899a6c904 (HEAD -> master)
Author: user.name <user.email>
Date:   Fri Jul 17 14:17:22 2020 +0900

    마크다운 정리
    
$ git log --oneline
6c84015 (HEAD -> master) 마크다운 정리
````

​	:bulb:`online 옵션은 복잡한 로그를 간결하게 볼 수 있다. 많은 사람이 개입하며 여러 번 커밋된 이력을 확인하기 유용하다.`



커밋은 해시값을 바탕으로 구분된다.

​	:bulb:`hash : 특정 데이터를 더 짧은, 고정된 길이의 데이터로 변환한 값`





## 원격저장소(remote repository) 활용하기

원격 저장소 기능을 제공하는 다양한 서비스 중에 github을 기준으로 설명한다.

​	:bulb:`github 외에도 다양한 서비스가 있지만, 현재로서는 github가 가장 풍부한 생태계를 가지고 있다.`

### 0. 준비사항

* ~~Github 가입~~
* Github에 repository 생성



### 1. 원격 저장소 등록

```bash
$ git remote add origin {github url}
```
* 원격저장소(remote)로 `origin`이라는 이름으로 github url을 등록(add)한다.

* 등록된 원격 저장소를 보기 위해서는 아래의 명령어를 활용한다.

  ```bash
  $ git remote -v
  origin  https://github.com/danonieee/TIL.git (fetch)
  origin  https://github.com/danonieee/TIL.git (push)
  ```



### 2. `push` - 원격 저장소로 업로드

```bash
$ git push origin master
```

`origin`이라는 이름의 원격 저장소로 commit 기록들을 업로드한다.

이후 변경사항이 생길 때마다, `add` -  `commit` - `push` 를 반복한다.



### 3. `pull` - 원격저장소로부터 불러오기

```bash
$ git pull origin master
```

`origin` 이라는 이름의 원격 저장소로부터 새로운 commit 기록들을 불러온다.