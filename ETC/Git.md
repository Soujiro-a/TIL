## Git

### 기본적인 명령어

##### 새로운 저장소 생성

- `git init` : git 하위 디렉토리 생성(git 저장소로 쓸 폴더 안에서 명령 실행)

##### 저장소 복제/다운로드

- `git clone <URL>` : 기존 소스 코드 다운로드/복제
- `git clone /로컬저장소/경로` : 로컬 저장소 복제
- `git clone 사용자명@호스트:/원격저장소/경로` : 원격 서버 저장소 복제

##### staging area/commit

- `git status` : 파일 상태 확인
- `git add <파일명>` : staging area에 단일 파일을 변경 사항을 포함
- `git add --all` : staging area에 파일에 변경 사항을 한번에 모두 포함
- `git reset HEAD <파일명>` : 해당 파일의 git add를 취소하고 Unstage상태로 변경
- `git commit -m "commit 메시지"` : commit 생성
- `git reset HEAD~N` : 마지막 N개의 commit을 취소 (1개일때는 보통 `HEAD^`와 같은 표기를 씀)

##### push

- `git push origin main` : commit까지 한 항목들을 origin 레포지토리의 main Branch에 업로드

##### pull

- `git pull remote main` : remote 레포지토리의 main Branch를 가져와 병합

##### 그 외

- `git log` : commit log 확인

### Branch

**독립적으로 어떤 작업을 진행하기 위한 개념**

- 한 소스 코드에서 동시에 다양한 작업을 가능하게 해줌
- 소스코드의 한 시점과 동일한 상태를 만들고, 브랜치를 넘나들며 작업할 수 있음.
- 각 브랜치에서 생긴 변화가 다른 브랜치에 영향을 주지 않고 독립적으로 코딩을 진행할 수 있음.

#### 종류

- Integration Branch

  - 배포될 소스 코드가 기록되는 Branch
  - Github Repo를 생성하면 기본적으로 main Branch가 생성됨
  - 해당 프로젝트의 모든 기능이 정상적으로 작동하는 상태의 소스코드가 담겨있음

- Feature Branch(Topic Branch)
  - 기능 추가, 버그 수정과 같이 단위 작업을 위한 Branch
  - Integration Branch로 부터 만들어내며, 하나의 작업이 완료되면 다시 병합하는 방식으로 진행.

#### 명령어

##### 새 Branch 생성

- `git branch 새 Branch 이름`

##### 새로운 Branch 생성 후 해당 Branch로 전환

- `git switch -c 새 Branch 이름`
- `git checkout -b 새 Branch 이름`

##### Branch 목록 확인

- `git branch`

##### Branch 목록과 각 Branch 최근 커밋 확인

- `git branch -v`

##### Branch 삭제

- `git branch -d 삭제할 branch 이름`
- `git branch -D` => 병합하지 않은 브랜치를 강제 삭제하는 방법

##### Branch 전환

- `git switch branch 이름`
- `git checkout branch 이름`

##### Branch 병합

- main Branch로 dev Branch를 병합할 때 (dev -> main)
  1. `git checkout main` => main Branch로 이동
  2. `git marge dev` => 병합

##### 로그에 모든 Branch를 Graph로 표현

- `git log --branches --graph --decorate`

##### 아직 commit 하지 않은 작업을 스택에 임시로 저장

- `git stash`

#### merge VS rebase

- main Branch로 dev Branch를 병합할 때 (dev -> main)
- merge
  - 변경 내용의 이력이 모두 남아있기 때문에 이력이 복잡해짐
  - main Branch에 dev Branch를 병합하는 commit log가 main에 새로 추가됨.
- rebase
  - Branch Base를 이동시킨다는 의미로, merge와 비슷하게 Branch 통합을 목적으로 하지만, 특정 시점으로 Branch가 가리키는 곳을 변경하는 기능을 함.
  - dev Branch를 베이스로 commit을 재정렬 함.
  - main에서 rebase를 하는건 피하는게 좋다.
