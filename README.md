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
- ***2022-06-21 강의: SourceTree로 진행해보기***
    - 이미 레포(원격저장소)가 있어도 또 레포(원격저장소)를 만들 수 있다.
        - 소스트리 -> 상단 메뉴 '저장소' -> 원격 저장소 추가 -> 추가 -> 원격 이름 'origin2', url / 경로 'HTTPS 복사붙이기', 디폴트 원격 체크 ->
        - 원격에 origin2가 추가되는 것을 확인할 수 있다.
    - 소스트리 상단 '패치'를 사용하면 원격 저장소 내용을 가져와 로컬환경에서 동기화시켜준다.
    - 원격에서 만든 브랜치를 로컬 브랜치로 가져오는 방법
        - 좌측 원격 -> origin 클릭 -> 새로 만든 브랜치 우클릭 -> 체크아웃 클릭
- ***2022-06-23 강의: Git을 특별하게 만드는 것***
    - **git의 주요 특징**
        - **Snapshot** : 델타 방식과 비교. 스냅샷은 새로운 버전이 만들어질 때 해당 버전에서의 각 파일이, 최종상태 그대로 저장되는 버전관리 방식이다. commit이 몇 만개 되는 repository를 델타방식으로 사용하게 되면 처음 커밋내용부터 가져와서 느리겠지만, 스냅샷은 현 시점의 각 파일들이 full로 저장되어 있어서 빠르다.
        - **분산 버전 관리** : '중앙집중식 버전관리'를 하는 CVS나 Subversion 등의 VCS는 원격 서버(ex. git의 github)에 모든 관리내역들이 저장된다. 참여하는 개발자들의 로컬 저장소에서는 원격 서버에서 다운받은 파일들로만 작업할 수 있다. 반면 '분산 버전관리'를 하는 github 원격 저장소는 ZIP 다운로드말고 clone 명령어를 써서 받아오면 로컬 파일뿐만 아니라 전체 git commit과 branch까지 받아져서 인터넷 연결상태와 상관없이 로컬에서 작업을 할 수 있다.
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

- ***사용해본 명령어 정리***
    - git에서 branch 전환
    ```bash
    git checkout (main 등 가고자하는 브랜치명)
    ```
## material 
- https://www.yalco.kr/@git-github-dive/5-2/