# 데브로드 Git Training

## Git과 GitHub 사용 환경 구축

1. Git 설치

   💡 Mac의 경우 터미널에 git을 입력했을 때 설치가 안 된 상태라면 `brew install git` 으로 설치.
   (Mac에서 의존성 설치는 brew만 사용하여 의존성을 한 곳에서 관리하는 습관이 필요)

   [👉 Git 설치하러 가기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

1. GitHub 연결

- GitHub은 https말고 SSH로 연결하기.
  - [SSH를 통한 GitHub 연결](https://docs.github.com/ko/authentication/connecting-to-github-with-ssh)

## 터미널 환경 설정

Git 명령어 수행은 `반드시 CLI 환경인 터미널`에서 진행합니다. 터미널 환경에 익숙해지기

- Windows
  - WSL2를 공부하고 설치합니다.
    - [WSL란?](https://docs.microsoft.com/ko-kr/windows/wsl/about)
  - Windows terminal 설치합니다.
    - [WSL 설치 및 WSL 2로 업데이트](https://docs.microsoft.com/ko-kr/windows/wsl/install-win10)
- Mac
  - iterm2 설치 후 iterm 터미널에서 진행합니다.
  - iterm2는 소프트웨어 패키지 관리 시스템인 brew를 이용하여 다운받는 것을 권장드립니다.
    - `brew install --cask iterm2`

## GUI 도구 설치

💡 여기서 설명한 습관만 익혀도 Git으로 사고날 확률을 압도적으로 줄여줄 겁니다.

- [Sourcetree](https://www.sourcetreeapp.com/) 를 설치
  - Git 명령어 입력은 반드시 터미널에서 진행합니다. Sourcetree와 같은 GUI도구에서 제공하는 기능은 중간 과정을 생략하고 2개 이상의 명령이 한 번에 수행되어 의도하지 않은 결과가 나타날 수 있습니다.
  - 그러면 GUI 도구는 왜 필요한가?
    - 터미널에서 Git 명령어를 입력 후 `의도한 결과`가 일어났는지 Sourcetree에서 계속 확인해야 합니다. 그래야 예상치 못한 사고를 최대한 방지할 수 있습니다.

## Pull Request 방법

1. 과제 GitHub repository 를 fork 합니다. fork를 하면 본인 계정의 GitHub에 동일한 repositiory가 복사되어 생성됩니다.

   **내 계정**에 복제된 repository에서 초록색 `Code` 버튼을 눌러 나오는 주소를 복사해 줍니다.

2. 로컬 환경에서 터미널을 이용해 새 프로젝트를 clone합니다.

   ```bash
   # origin 원격 저장소 추가
   git clone <복사한 Repository 주소>

   # 예시)
   git clone git@github.com:bbhye1/git-training.git
   ```

3. PR 보낼 저장소 주소를 upstream이라는 이름으로 추가합니다.

   ```bash
   # 생성된 폴더로 이동
   cd git-training

   # upstream 원격 저장소 추가
   git remote add upstream <PR 보낼 원격 Repository 주소>

   # 예시)
   git remote add upstream git@github.com:megaptera-kr/git-training.git
   ```

4. upstream 원격 저장소들이 잘 추가되었는지 확인합니다.

   ```bash
   # 원격 저장소 확인
   git remote -v

   # 아래와 같은 결과가 나왔는지 확인합니다.
   origin      git@github.com:bbhye1/git-training.git (fetch)
   origin      git@github.com:bbhye1/git-training.git (push)
   upstream      git@github.com:megaptera-kr/git-training.git (fetch)
   upstream      git@github.com:megaptera-kr/git-training.git (push)
   ```

5. upstream 원격 저장소의 최신 상태를 반영합니다.

   ```bash
   git fetch upstream

   git rebase upstream/main
   ```

6. 새 브랜치를 생성해줍니다.

   ```bash
   # 새 브랜치 생성 (브랜치 이름은 자신의 깃헙 유저네임으로 설정하기)
   git switch -c <브랜치 이름> upstream/main
   ```

7. 작업을 진행합니다.
8. 작업이 완료된 후 변경된 점을 커밋합니다.

   ```bash
   # 변경된 점 모두 추가
   git add .

   # 변경된 점 커밋
   git commit -m '<메세지내용>'
   ```

9. origin 원격 저장소에 작업 브랜치를 올립니다.

   ```bash
   git push origin <브랜치 이름>
   ```

10. New Pull Request를 보내 과제를 제출합니다.

    과제 레포지토리를 열고 페이지 상단에 `Compare & pull request` 버튼을 클릭합니다.

    PR(Pull Request)을 요청 할 때, base repository의 main에 PR 요청을 보내는 것이 아닌 꼭 이미 생성되어 있는 **본인의 GitHub Username과 동일한 브랜치**에 보내야 한다는 점을 기억해주세요.

---

## 더 알아보기

아래 문서를 통해 Git에 대해 더 깊게 학습해 볼 수 있습니다.

- [Pro Git](https://git-scm.com/book/ko/v2)
