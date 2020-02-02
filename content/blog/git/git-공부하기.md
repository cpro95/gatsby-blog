---
title: git 공부하기
date: 2020-02-02 21:02:02
category: git
draft: false
---

![git](./git_image.png)

wiki 참조했으며, 필요한 부분 추가했습니다.

# DVCS(분산 버전 관리 시스템)

git = 분산 버전 관리 시스템(Distributed Version Control System)

## 파일의 상태

### TRACKED 파일의 세 가지 상태

- modified: 파일을 수정했지만 아직 커밋하지 않은 상태

- staged: 파일을 수정해서 곧 커밋할 것이라고 표시한 상태

- committed: 데이터가 로컬 데이터베이스에 안전하게 저장된 상태

## 파일의 라이프사이클

### 작업 디렉토리(Working Directory)의 파일

- Untracked = 버전 관리 대상이 아닌 파일
- Tracked = 버전 관리 대상 파일
- Unmodified = 수정 안 한 파일
- Modified = 수정한 파일
- Staged = 커밋 직전의 파일 = Changes to be committed

Untracked, Modified 파일을 추가(add)한다는 것은 다음에 커밋할(Staged) 파일 목록에 추가한다고 생각해야 한다. 프로젝트에 파일을 추가한다는 뜻이 아니다. 그리고 Untracked 파일은 Staged 파일이 되기 때문에 자연스럽게 Tracked 파일이 된다.

## 설정

### 설정 파일

```
/etc/gitconfig
~/.gitconfig
.git/config
```

설정의 우선순위는 역순이다.

### 사용자 정보

```
$ git config --global user.name "John Doe" $ git config --global user.email "johondoe@example.com"
git config --global 옵션으로 명령했기 때문에 우분투의 경우 사용자 설정 파일 ~/.gitconfig 에 다음 내용으로 저장된다.
﻿
cat .gitconfig \[user] name = John Doe email = johondoe@example.com
```

## 저장소 만들기

### 로컬 현재 디렉토리를 GIT 저장소로 만들기

```
git init
```

### 원격 저장소를 로컬로 복제(CLONE)하기

```
git clone https://github.com/libgit2/libgit2
// 원격 저장소를 원격 저장소의 이름으로 복제한다.
﻿
git clone https://github.com/libgit2/libgit2 mylibgit
// 원격 저장소를 mylibgit 새로운 이름으로 복제한다.
```

#### 참고 사항

원격 저장소의 이름은 기본값이 origin이다. 권한이 없는 원격 저장소를 clone할 수 있고 오픈소스를 fork한 원격 저장소를 clone할 수도 있다.

## 여러 가지 예시

새 파일 저장소에 저장하기 (UNTRACKED -> STAGED -> COMMITTED)
\*.c와 LICENSE 새로운 파일을 만들어서 저장소에 저장하는 것은 2단계로 나눌 수 있다.

- 1단계 (Untracked -> Staged)

```
$ git add *.c
$ git add LICENSE
```

- 2단계 (Staged -> Committed)

```
$ git commit -m 'initial project version'
```

파일을 수정하고 저장소에 저장하기 (UNMODIFIED -> MODIFIED -> STAGED -> COMMITTED)
처음 저장소를 Clone하면 모든 파일은 Tracked이면서 Unmodified 상태이다.

- 1단계: 파일 수정 (Unmodified -> Modified)

에디터로 hello.c 파일을 편집한다.

- 2단계: 파일 추가 (Modified -> Staged)

```
$ git add hello.c
```

- 3단계: 파일 커밋 (Staged -> Committed)

```
$ git commit -m 'greeting message changed'
```

git add 명령어는 Untracked 파일을 Staged 파일로 만들 때도 쓰고 Modified 파일을 Staged 파일로 만들 때도 사용한다.

git add의 의미는 프로젝트에 파일을 추가한다기보다 다음에 커밋할 파일의 목록에 추가하는 것으로 이해한다.

작업 디렉토리의 파일의 상태 확인

```
$ git status
```

파일 무시하기

```
.gitignore
```

// 위 파일을 만들어 버전 관리하지 않고 무시할 파일 목록을 만든다.

파일 비교

```
$ git diff
```

// Modified 파일을 Committed 파일과 비교하여 보여준다.

```
$ git diff --staged
```

// Staged 파일을 Committed 파일과 비교하여 보여준다.

변경사항 커밋하기

```
$ git commit
```

// 커밋 메시지를 에디터로 입력 후 커밋한다.

```
$ git commit -m "Story 182: Fix benchmarks for speed"
```

// 커밋 메시지를 옵션으로 지정하고 커밋한다.

```
$ git commit -am "added new benchmarks"
```

// Staging Area 생략 후 바로 커밋할 수도 있다.

파일을 삭제하기

```
$ git rm 파일이름
```

파일 이름 바꾸기

```
$ git mv 옛파일이름 새로운파일이름
```

되돌리기

마지막 커밋 내용을 되돌리기

이미 커밋을 했지만 파일을 깜빡하고 추가하지 않은 파일이 있거나 커밋 메시지를 수정하고 싶을 때 git commit —amend 명령어를 이용한다.

```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

STAGED -> UNSTAGED

git reset HEAD \[파일 이름] 명령어로 특정 파일을 Staged 상태에서 Unstaged 상태로 변경한다.

```
$ git reset HEAD CONTRIBUTION.md
```

MODIFIED -> UNMODIFIED

git checkout — \[파일 이름] 명령으로 애초에 저장소에 저장된 버전을 다시 꺼내온다.

```
$ git checkout -- CONTRIBUTION.md
```

원격 저장소(REMOTE REPOSITORY)

원격 저장소 = 인터넷이나 네트워크 어딘가에 존재하는 저장소

원격 저장소 확인

원격 저장소를 clone하면 origin 이름으로 원격 저장소가 자동으로 등록된다.

```
$ git remote
```

// 원격 저장소의 이름을 확인한다.

```
$ git remote -v
```

// 원격 저장소의 이름과 URL을 함께 확인한다.

원격 저장소 추가\$ git remote add \[원격 저장소 이름]\[url] 명령으로 아래는 예시이다.

```
$ git remote add pb https://github.com/paulboone/ticgit
```

위와 같이 등록하고 실제로 로컬 저장소에는 없지만 pb 원격 저장소에 있는 것을 가져오려면 아래와 같이 명령한다.

```
$ git fetch pb
```

git fetch 명령은 원격 저장소의 데이터를 모두 로컬로 가져오지만 자동으로 Merge하지는 않는다.

원격 저장소에 PUSH하기git push \[원격 저장소 이름]\[브랜치 이름] 명령으로 Push할 수 있다.

```
$ git push origin master
// origin 원격 저장소의 master 브랜치에 Push한다.
﻿
$ git push origin HEAD
// 원격 저장소에 현재 로컬 브랜치와 동일한 이름의 브랜치에 Push한다.
// 원격 저장소의 다른 브랜치에 잘못 커밋하는 실수를 줄여줄 수 있다.
```

원격 저장소 이름을 바꾸거나 삭제하기

```
$ git remote rename pb paul
// 원격 저장소의 이름을 변경할 수 있다.
﻿
$ git remote rm paul
//원격 저장소를 삭제할 수 있다.
```

원격 저장소 이름 규칙

전형적인 원격 저장소의 이름이다.origin: Github 내 저장소의 이름(Fork한 경우 포함)upstream: Fork한 경우 원본 프로젝트의 저장소의 이름(디폴트 이름은 아니지만 통상적인 이름) 참고로 master는 브랜치 이름이다.master: git init으로 저장소 생성 시 디폴트 브랜치 이름

브랜치

브랜치 만들기

```
$ git branch testing
```

// git branch \[브랜치 이름] 명령으로 아래와 같이 testing 브랜치를 만든다.

브랜치 변경

```
$ git checkout testing
```

// git checkout 명령어로 작업하려는 testing 브랜치로 이동할 수 있다.

브랜치를 이동(변경)하면 작업 디렉토리의 파일 내용도 변경된다.

```
$ git checkout -b testing
```

// git checkout -b 명령어로 두 번 입력하지 않고

// 한 번에 브랜치를 만들고 바로 이동할 수도 있다.

로컬 브랜치를 원격 저장소에 PUSH하기

```
$ git push -u origin testing
```

// git push -u origin \[브랜치 이름] 명령으로

// 로컬 브랜치를 원격 저장소에도 반영할 수 있다.

MERGE

이슈 처리를 위해 브랜치 적용 시나리오

```
$ git checkout -b issue53
// 어떤 이슈 처리를 위한 issue53 토픽 브랜치를 만든다.
﻿
$ vim index.html
// 소스파일을 수정한다.
﻿
$ git commit -am 'fixed the broken email address'
// 수정한 파일을 로컬 저장소로 커밋한다.
﻿
$ git checkout master
// master 브랜치로 다시 이동한다.
﻿
$ git merge issue53
// issue53 브랜치의 내용을 master 브랜치에 반영하여 합친다.
﻿
$ git branch -d issue53
// 브랜치가 불필요해지면 삭제한다.
```

REMOTE CLONE & BRANCH PULL

리모트 CLONE 후 BRANCH 도 CLONE 하는 방법

```
$ git clone http://github.com/username/project.git
// 원하는 repository를 clone 하고
﻿
$ git branch -a
// 모든 branch 확인
﻿
$ git checkout -b branch-name origin/branch-name
// 원하는 BRANCH로 -b 옵션으로 checkout 하면 로컬에서 해당 branch 가능
```

기타 유용한 명령어

1. git stash

커밋 후 깨끗한 상태에서 나름 작업했던 것을 커밋하지 않고 임시로 stash(안전한 곳에 넣어두다)할 수 있다. 나중에 stash한 상태의 코드를 다시 불러 올 수 있다.

```
$ git stash save "mystash"
﻿
// 현재 작업을 저장해두고 branch를 head로 돌린다. (git reset -hard)
$ git stash list
﻿
// 저장되어 있는 stash들 보기
$ git stash pop
﻿
// stash들은 스택에 저장된다. 따라서 pop 명령은 가장 최근에 stash 한 상태를 현재 branch에 적용하고,
// stash가 저장되어 있는 stack 에서 삭제된다.
﻿
$ git stash apply
// pop 과 비슷한 명령이지만 stash list에서 삭제하기 않고 그냥 적용만 시킨다.
﻿
$ git stash drop
// 필요없는 stash를 삭제
﻿
$ git stash clear
// 전체 stash list를 삭제
```
