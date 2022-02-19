# 02_branch

`head `: 내 현재 위치

```bash
$ git init
$ git add .
$ git commit -m 'first commit'
$ touch .gitignore => '.idea/' 입력
```



## git log

`git log --oneline`

지금까지 커밋한 각 버젼 목록



`git checkout (버젼목록)` : 해당 버젼으로 돌아감



## git branch

`branch` 는 스티커 개념으로 이해

`commit` 은 브랜치별로 뻗어 나간다

`git branch 'name'` : 'name' 브랜치 생성



더블 tap : 해당 명령어 수행 가능한 목록

ex) `git merge` + `tap+tap` => merge 가능한 목록 나열



마스터를 원하는 브랜치로 merge 해서 합치기



## git switch -c

`git switch -c b2` : b2 라는 브랜치를 생성하면서 head 이동

`git switch b1` : head 를 b1 으로 이동



## vim

`vim b2.txt`

`i` -> 입력 -> `esc` -> `:wq`or `:x` 눌러서 나오기

`:q!` 하면 그냥 나오기

`commit -m` 안남기면, `i` -> 입력 -> `:q`
