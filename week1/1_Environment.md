# 1. 개발 환경

## [MINE](https://github.com/wkqkel/frontend-survival-week01/tree/wkqkel)

개발자는 개발 환경을 제대로 이해하고 능숙하게 설정할 줄 알아야 합니다.

따라서 이번 주차에 나오는 내용을 제대로 학습하지 않으면 앞으로 계속 발목을 잡히게 됩니다.

아샬의 개발 환경에 대한 습관을 제대로 훔치시기 바랍니다

가능하면 바닥부터 셋팅 매일매일 반복해서 만들어보기 추천

---

자바스크립트(정확히는 Node.js)로 개발

툴체인라고 부르는 개발도구, 환경들은 Node.js를 기반(deno보다 설치하기 까다로움)

도구가 계속 바뀌기 때문에, 상황에 따라 어떤 것을 선택할지 라는 어려움이 있음.

기본적인 도구들과 개발 환경 세팅의 전체적인 흐름을 이해한는 것이 중요.

---

## JavaScript 개발 환경 (Node.js) 세팅

- [**참고 문서**](https://github.com/ahastudio/til/blob/main/javascript/20181212-setup-javascript-project.md) → fnm + jest + eslint
- [**Node.js**](https://nodejs.org/ko/)
  최신 버전인지 확인 필요
- [**fnm (Fast Node Manager)**](https://fnm.vercel.app/)

`fnm 설치`

```bash
brew install fnm  # fnm 설치
eval "$(fnm env)" # ~/.bashrc 또는 ~/.zshrc에 다음을 추가
```

`~/.zshrc에 추가하기`

'Vim'은 모든 종류의 텍스트를 만들고 변경할 수 있도록 구성 가능한 텍스트 편집기

```bash
vim ~/.zshrc        # 환경설정창으로 들어간뒤
i                   # insert모드진입 마우스 휠내려서 하단에 텍스트 추가
ESC                 # ESC를 눌러서 noaml 모드 진입
:                   # ":"를 이용하여 command-line 모드 진입.
:wq                 # command-line 모드에서 저장 후 종료
```

---

## TS + React + Jest + ESLint + Parcel 개발환경셋팅

`0. 작업 폴더 준비`

`1. npm 설치 및 .gitignore 파일 생성`

`2. TypeScript 설치`

`3. ESLint 설치`

`4. 리액트 설치`

`5. 테스팅 도구 설치`

`6. Parcel 설치`

`7. 리액트 기본 파일 셋팅`

## 용어 정리

`npm과 npx`

- 'npm'이란? Node Package Manager, 자바스크립트 라이브러리를 설치하고 관리하는 패키지 매니저
  - 몇 줄의 명령어로 기존의 공개된 모듈들을 설치하고 활용할 수 있게 해준다.
- 'npx'란 패키지를 임시 설치해서 실행(eXecute)하는 용도로 npm 5.2.0버전부터 npm에서 제공해주는 하나의 도구.
  - 모듈을 로컬에 저장하지 않고, 매번 최신 버전의 파일만을 임시로 불러와 실행 시킨 후에, 다시 그 파일은 없어지는 방식으로 모듈이 돌아감.
  - 로컬 -> 글로벌 -> npm(remote) 순으로 찾아 실행. 따라서 컴퓨터의 공간을 낭비하지않고, 최신상태.

`package.json/ package-lock.json`

- 'package.json'은 project에 대한 정보, 개발과 관련된 모듈 정보(모듈) 등이 포함되어 있는 명세.
  - 'dependencies'는 프로그램을 실행시키위해 필요한 모듈과 버전
  - 'devDependencies'는 개발환경에서 필요한 모듈.
  - 'scripts'는 npm으로 실행시킬 수 있는 명령어를 정의할 수 있다. npm run [명령어]로 실행
- 'package-lock.json'은 파일이 생성되는 시점의 의존성 트리에 대한 정확한 (버전)정보를 가지고 있음. npm을 사용해서 node_modules 트리나 package.json 파일을 수정하게 되면 자동으로 생성.
- package.json에는 version range, package.lock.json에는 정확한 version이 들어가는데, 이러한 이유는 크고 작은 패키지들의 릴리즈에 package.json을 항상 추적하고 수정해야하는 것을 version range를 사용함으로써 피함.
- package.json을 사용하여 node_modules를 생성하지않고, package-lock.json을 사용하여 node_modules를 생성

`node_modules`

- node_modules 디렉토리에는 package.json에 있는 모듈 뿐만 아니라, package.json에 있는 모듈이 의존하고 있는 모듈 전부를 포함하고 있다.
- npm으로 새로운 모듈(패키지)를 설치하게 되면, package.json과 node_modules에 추가된다.

`ES Modules vs CommonJS`

- '모듈'이란 애플리케이션을 구성하는 개별적 요소로서 재사용 가능한 코드 조각
- 'ES Modules(MJS)': EMCA Script modules, 브라우저 JS 환경에서 import, export를 사용.
- 'Common JS(CJS)': Node.js는 기본적으로 CommonJS 모듈을 지원. require, module.exports를 사용.
