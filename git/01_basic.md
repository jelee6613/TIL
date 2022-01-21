# Git_01_Basic

## What?

분산 버젼 관리 시스템

## Why?

수많은 수정 과정을 효율적이고, 간결하게 버젼 관리 가능하므로 사용

## How?

### Git config

Git을 설치하면 가장 먼저 사용자이름과 주소를 설정

``` bash
$ git config --global user.name "jelee6613"
$ git config --global user.email "jelee6613@gamail.com"
```

프로젝트마다 다른 이름과 이메일을 사용하고 싶으면 `--global` 을 빼고 입력



### Git init

관리하고자 하는 디렉토리에 git init 입력하면 .git이 생성되고, 디렉토리는 repository 로 변경 (git 앞에 붙은 . 은 hidden 숨김을 의미, ls -a로 확인 가능)

repository 디렉토리의 하위 디렉토리도 전부 git 관리

#### 금기사항

* Home 디렉토리 git init
* git init 입력한 디렉토리의 하위 디렉토리에 중복 git init

#### 취소방법

취소하려는 repository 디렉토리에서 rm -rf .git 입력



### Git add

` $ git add blah.md `  : 'blah.md' 란 파일을 스테이징

` $ git add . ` : 현재 디렉토리의 전체 변경사항을 스테이징

#### Git status

` git add ` 하고 `git status `로 스테이징 됐는 지 확인 가능



### Git commit

git add 를 하고나서 git status 를 하면 초록불로 바뀜 (스테이징 상태를 의미)

` $ git commit -m 'blah'` : 스테이징에 올라온 것들을 'blah' 라는 메시지를 남기고 기록 (버젼으로 남김)

#### Git log

커밋 기록 조회

최근 내역이 가장 위



### Git push

local 에서 remote로 commit 이력을 업로드

`$ git push origin master ` : 내 컴퓨터(로컬 저장소)에서 origin(원격 저장소)으로 push

실수로 push 하지 않도록 주의

*최초에 github sign in 창이 나와서 로그인 해주면 동기화 완료

#### Git remote add origin URL

`$ git remote add origin 원격 저장소URL` : 원격 저장소를 연결, origin 은 암묵적 명칭이므로 임의 설정 가능

---

### .gitignore

해당 파일에 적은 파일은 버젼 관리로부터 무시



### READ.md

프로젝트 소개글

관리되는 디렉토리에 대문자 READ.md 로 파일 생성하면 원격 저장소에 소개글 기능



### Fork

상대방의 원격저장소를 그대로 복제하여 내 원격저장소에 등록

이후, fork 받은 저장소를 clone하여 로컬에서 작업하고 push하면 fork받은 ‘나의 원격저장소’에 올라감

 

