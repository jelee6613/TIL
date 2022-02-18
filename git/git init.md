# 02_branch

<정리중>

git init

git add .

git commit -m 'first commit'

touch .gitignore

ㄴ 깃이그노어에 '.idea/' 입력

git add .

git commit -m '2'



git log -- oneline

git checkout



head master

git branch b1 브랜치 생성

git switch b1 < - 브랜치



tap tap 할 수 있는 목록

ex) git merge (더블탭)

마스터를 해당 브랜치로 머지



git switch -c b2

만들면서 이동



vim b2.txt

i -> 입력 -> esc -> :wq or :x 눌러서 나오기

:q! 하면 그냥 나오기

commit -m 안남기면

그냥 누르고 인서트 입력 후 :q



브랜치는 스티커

헤드는 내 현재 위치

커밋은 브랜치별로 뻗어나간다

머지 하기 위해 브랜치

