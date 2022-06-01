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
- 

## material 
- https://www.yalco.kr/@git-github/4-3/