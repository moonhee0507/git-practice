# git-practice
## what I learned
- ***2022-06-01 강의: 원격 저장소 사용하기***
    - 원격목록 확인하는 방법
    ```bash
    git remote
    ```
    - 자세히 확인하려면 `git remote -v`
    - 협업을 하는 상황에서는 zip을 다운받을게 아니라(.git이 없어서 관리내역을 확인할 수 없기 때문), 다운받기를 원하는 폴더에서 git bash를 열어서 처리한다.
    ```bash
    git clone HTTPS복사붙이기
    ```
    - 원격의 저장소(깃허브)에서 커밋했다면? `git pull`로 커밋을 당겨올 수 있다.
    - 협업 시 push하기 전에 pull 해줘야 적용이 원활하다.(각각 merge방식과 rebase방식)
    ```bash
    git pull --no-rebase (원격과 로컬의 분기된 시간선을 마지막에 한군데로 모아준다)
    ```
    ```bash
    git pull --rebase (원격에 우선 맞춘 다음에 내가 한걸 잘라서 붙인다)
    ```
    - 로컬내역 강제 push `git push --force`(충돌 전으로 reset)

<br>

- ***2022-06-20 강의: 원격의 브랜치 다루기***
    - 로컬에서 브랜치 만들고 원격에 push
    ```bash
    git push <!--이렇게 입력하면 대상을 명시하라는 메시지 나옴-->
    git push -u origin from-local
    ```
    - 브랜치 목록 확인하기
    ```bash
    git branch --all
    ```
    - 원격에서 만든 브랜치 로컬에 받아오기(git branch -a해도 현재는 보이지 않음)
        - 원격 변경사항 확인
        ```bash
        git fetch
        (git branch -a로 확인)
        ```
        - 아래 명령어로 로컬에 같은 이름의 브랜치 생성하여 연결하고 switch
        ```bash
        git switch -t origin/from-remote
        ```
    - 원격에 있는 브랜치 삭제하기
    ```bash
    git push (원격 이름) --delete (원격의 브랜치명)
    원격 이름은 origin
    ```
<br>

- ***2022-06-21 강의: SourceTree로 진행해보기***
    - 이미 레포(원격저장소)가 있어도 또 레포(원격저장소)를 만들 수 있다.
        - 소스트리 -> 상단 메뉴 '저장소' -> 원격 저장소 추가 -> 추가 -> 원격 이름 'origin2', url / 경로 'HTTPS 복사붙이기', 디폴트 원격 체크 ->
        - 원격에 origin2가 추가되는 것을 확인할 수 있다.
    - 소스트리 상단 '패치'를 사용하면 원격 저장소 내용을 가져와 로컬환경에서 동기화시켜준다.
    - 원격에서 만든 브랜치를 로컬 브랜치로 가져오는 방법
        - 좌측 원격 -> origin 클릭 -> 새로 만든 브랜치 우클릭 -> 체크아웃 클릭

<br>

- ***2022-06-23 강의: Git을 특별하게 만드는 것***
    - **git의 주요 특징**
        - **Snapshot** : 델타 방식과 비교. 스냅샷은 새로운 버전이 만들어질 때 해당 버전에서의 각 파일이, 최종상태 그대로 저장되는 버전관리 방식이다. commit이 몇 만개 되는 repository를 델타방식으로 사용하게 되면 처음 커밋내용부터 가져와서 느리겠지만, 스냅샷은 현 시점의 각 파일들이 full로 저장되어 있어서 빠르다.
        - **분산 버전 관리** : '중앙집중식 버전관리'를 하는 CVS나 Subversion 등의 VCS는 원격 서버(ex. git의 github)에 모든 관리내역들이 저장된다. 참여하는 개발자들의 로컬 저장소에서는 원격 서버에서 다운받은 파일들로만 작업할 수 있다. 반면 '분산 버전관리'를 하는 github 원격 저장소는 ZIP 다운로드말고 clone 명령어를 써서 받아오면 로컬 파일뿐만 아니라 전체 git commit과 branch까지 받아져서 인터넷 연결상태와 상관없이 로컬에서 작업을 할 수 있다.

<br>

- ***2022-06-23 강의: Git의 3가지 공간***
    - Working directory : 기존 파일에 수정사항이 생기면 이곳에서 관리된다.
        - untracked : Add된 적 없는 파일, ignore된 파일
        - tracked : Add된 적 있고, 변경내역이 있는 파일
        `git add` 명령어로 Staging area로 이동
    - Staging area : 커밋을 위한 준비 단계
    - Repository : commit들이 저장되는 곳. `.git directory`라고도 불린다. 커밋된 상태.
    - 관련 명령어
        - 파일 삭제(`git rm`)
            - 파일을 삭제한 후 `git status`로 살펴보면 파일 삭제가 `working directory`에 있음
                - `git reset --hard`로 복원 가능
            - `git rm 파일명`으로 삭제하고 `git status`로 살펴보면 파일 삭제가 `Staging area`에 있음
                - `git reset --hard`로 복원 가능
        - 파일 이동(`git mv`)
            - 파일 이름 변경 후 `git status`로 살펴보면?
            - 복원 후 `git mv 원래파일명 바꾸려는파일명`로 실행 뒤 비교
        - `staging area`에서 `working directory`로 보내기
            ```bash
            git restore --staged (파일명)
            ```
            - `--staged`를 빼면 `working directory`에서도 제거
        - reset의 3가지 옵션
            - `--soft`: `repository`에서 `staging area`로 이동
            - `--mixed` (default): `repository`에서 `working directory`로 이동
            - `--hard`: 수정사항 완전히 삭제

<br>

- ***2022-06-24 강의: 제코베 호준님 강의***
    - reset과 revert의 차이점
        - reset: 지정한 커밋으로 이동(지정 커밋 이후의 히스토리 초기화)
        - revert : 지정한 커밋의 내용으로 새로운 커밋 생성(히스토리 보존)
            - 반드시 직전 commit으로 되돌아가야 한다. 만약 처음 commit으로 돌아가고 싶다면 revert를 연속으로 하여 되돌아가야 한다.
            ```bash
            git revert (직전커밋 id)
            ```
            - vi editor가 실행되면 `:wq`를 입력한 다음 빠져나온다.

<br>

- ***2022-07-04 강의: 제코베 호준님 강의***
    - Branch와 Fork의 차이
    
    |Branch|Fork|
    |-----|----|
    |하나의 저장소에서 브랜치를 나누어 쓴다. | 여러 저장소를 만들고 브랜치를 만들어 사용한다.|
    |코드 커밋이력을 쉽게 볼 수 있다. | 원본 저장소에 영향을 미치지 않으므로 자유롭게 수정할 수 있다.|
    |소수인원 작업 시 사용하는 것이 좋다. | 원본 저장소의 이력을 보려면 주소를 추가해야 한다.|
    | | 불특정 다수의 사람의 작업 시 사용하는 것이 좋다.|
    
    - PR 취소: Pull Request는 취소가 가능하지만 취소했다는 내역이 남게 된다. 이 내역은 github 정책에 의해서 삭제가 되지 않으므로 정말 삭제하고 싶은 경우 직접 연락해서 삭제할 수 있다.
    - **amend**: 최신 커밋에 누락된 파일을 추가하고 싶을 때 사용
    ```bash
    // 파일 수정 후 저장 먼저 해주세요.
    git add 수정파일명
    git commit --amend

    * Commit_EDITMSG가 켜지면 이전 커밋 메시지를 확인할 수 있다.
    * 메시지를 수정하고 싶으면 i를 누르고 수정
    * ESC > :wq > enter
    * git log로 확인하기
    ```
    - **stash**: 다른 브랜치로 이동하고 싶을 때 수행 중이던 작업을 임시 저장하고 가장 최근 커밋상태로 만든다.
    ```bash
    i) Untracked 파일을 stash 하는 경우

		// 브랜치 이동 전 보관
		git stash --all
		* git 저장소에서 관리하지 않는 파일(add 안해준 파일)까지 모두 저장하고 싶다는 의미
		
		// 보이게 하려면 원래 브랜치로 돌아와서
		git stash pop

    ii) Tracked 파일을 stash 하는 경우

		// 브랜치 이동 전 보관
		git stash
		* 보이지 않게 된다
		
		// 보이게 하려면 원래 브랜치로 돌아와서
		git stash pop
    ```
    - 파일 상태
        - **Untracked(관리대상이 아님)**: 파일 생성 후 한번도 `git add`하지 않은 상태
        - **Tracked(관리대상임)**: git이 관리하는 파일
            - *Unmodified*: 최근의 커밋과 비교했을 때 바뀐 내용이 없는 상태
            - *Modified*: 최근 커밋과 비교했을 때 바뀐 내용이 있는 상태
            - *Staged*: 파일이 수정되고 나서 스테이지 공간에 올라와 있는 상태(`git add` 후의 상태)

<br>

- ***2022-07-04 강의: 코딩애플 쉽게 설명하는 Git 기초 3. git branch***
    - 다른 브랜치의 코드를 main 브랜치에 합치고 싶을 때
    ```bash
    // 1. main으로 가기
    git switch main

    // 2. 합쳐버려!
    git merge coupon
    ```
    - **conflict 발생 시**
    ```bash
    // 1. 원하는 코드만 남기고(=고치고)
    // 2. git add
    // 3. git commit
    // 4. git push
    ```
<br> 

- ***사용해본 명령어 정리***
    - git에서 branch 전환
    ```bash
    git checkout (main 등 가고자하는 브랜치명)
    ```
    - origin 저장소의 main 브랜치로 push하기
    ```bash
    git push origin main
    ```
    - a 브랜치 작업 중 main 브랜치 내용이 수정되었을 때 a 브랜치에 main 브랜치 반영하기
    ```bash
    git checkout a
    git rebase main
    git pull
    git push origin a
    ```
    - 커밋하기 싫은 내용 임시 저장하기
    ```bash
    git stash
    
    // stash 목록 확인
    git stash list
    
    // 가장 최근 stash 가져오기
    git stash apply
    
    // 특정 stash 가져오기(ex. stash@{2})
    git stash apply [stash 이름]
    
    // stash 가져오고 동시에 스택에서 stash 제거
    git stash pop
    ```
    - main 브랜치로 브랜치명 변경
    ```bash
    git branch -m master main
    ```
<br>   
   
## material 
- https://www.yalco.kr/@git-github-dive/5-2/
- 알아서 잘 딱 깔끔하고 센스있게 정리하는 GitHub 핵심 개념
