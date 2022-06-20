# git-practice
## what I learned
- 2022-06-01 강의
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
- 2022-06-20 강의
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

## material 
- https://www.yalco.kr/@git-github/4-5/