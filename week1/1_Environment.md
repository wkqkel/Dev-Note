## 학습 키워드

- Node.js
- NPM(Node Package Manager)
  - package.json / package-lock.json
  - node_modules
  - npx
- ES Modules vs CommonJS

# 1. 용어 정리
## nodejs와 툴체인
    자바스크립트 정확하게는 'nodejs'로 개발할 것.  
    '툴체인' 이라고 부르는 개발도구, 환경들을 nodejs로 쓴다.  
    'deno'를 쓰면 간단할 수 있지만, 현재 대부분 nodejs를 기반으로 해서 사용.  
    도구가 계속 바뀌기 때문에, 상황에 따라 어떤 것을 선택할지 라는 어려움이 있음.  
    그래서 여기있는 요소들은 조금씩 달라질 수 있기에 전체적인 흐름을 다룸.

    nodejs란? Javascript를 실행 시킬 수 있도록 하는 오픈소스 서버 환경
## nvm과 fnm
    'nvm'이란? Node Version Manager, 프로젝트마다 Node.js버전을 다르게 설정 가능하게 해준다.   
    'fnm'이란? Fast and simple Node.js version Manager로 더 빠름   
    노드는 짝수 버전은 안정된 버전

### fnm설치
```
brew install fnm    // fnm 설치
eval "$(fnm env)"   // ~/.bashrc 또는 ~/.zshrc에 다음을 추가
                    // fnm list, fnm use
```
### ~/.zshrc에 추가하기     
'Vim'은 모든 종류의 텍스트를 만들고 변경할 수 있도록 구성 가능한 텍스트 편집기

```
vim ~/.zshrc        // 환경설정창으로 들어간뒤
i                   // insert모드진입 마우스 휠내려서 하단에 텍스트 추가
ESC                 // ESC를 눌러서 noaml 모드 진입
:                   // ":"를 이용하여 command-line 모드 진입.
:wq                 // command-line 모드에서 저장 후 종료
```

## npm과 npx
    'npm'이란? Node Package Manager, 자바스크립트 라이브러리를 설치하고 관리하는 패키지 매니저로, 몇 줄의 명령어로 기존의 공개된 모듈들을 설치하고 활용할 수 있게 해준다.
    'npx'란 패키지를 임시 설치해서 실행(eXecute)하는 용도로 npm 5.2.0버전부터 npm에서 제공해주는 하나의 도구. 모듈을 로컬에 저장하지 않고, 매번 최신 버전의 파일만을 임시로 불러와 실행 시킨 후에, 다시 그 파일은 없어지는 방식으로 모듈이 돌아감. (로컬 -> 글로벌 -> npm(remote) 순으로 찾아 실행). 따라서 컴퓨터의 공간을 낭비하지않고, 최신상태.

## package.json/ package-lock.json
    'package.json'은 project에 대한 정보, 개발과 관련된 모듈 정보(모듈) 등이 포함되어 있는 명세.
      'dependencies'는 프로그램을 실행시키위해 필요한 모듈과 버전
      'devDependencies'는 개발환경에서 필요한 모듈.
      'scripts'는 npm으로 실행시킬 수 있는 명령어를 정의할 수 있다. npm run [명령어]로 실행   
    'package-lock.json'은 파일이 생성되는 시점의 의존성 트리에 대한 정확한 (버전)정보를 가지고 있음. npm을 사용해서 node_modules 트리나 package.json 파일을 수정하게 되면 자동으로 생성.    
    => package.json에는 version range, package.lock.json에는 정확한 version이 들어가는데, 이러한 이유는 크고 작은 패키지들의 릴리즈에 package.json을 항상 추적하고 수정해야하는 것을 version range를 사용함으로써 피함. 
    => package.json을 사용하여 node_modules를 생성하지않고 package-lock.json을 사용하여 node_modules를 생성

## node_modules
    node_modules 디렉토리에는 package.json에 있는 모듈 뿐만 아니라, package.json에 있는 모듈이 의존하고 있는 모듈 전부를 포함하고 있다. npm으로 새로운 모듈(패키지)를 설치하게 되면, package.json과 node_modules에 추가된다.

## ES Modules vs CommonJS
    '모듈'이란 애플리케이션을 구성하는 개별적 요소로서 재사용 가능한 코드 조각
    'ES Modules(MJS)':  EMCA Script modules, 브라우저 JS 환경에서 import, export를 사용.
    'Common JS(CJS)': Node.js는 기본적으로 CommonJS 모듈을 지원. require, module.exports를 사용.
    
# 2. TS + React + Jest + ESLint + Parcel 개발환경셋팅

## 0. 작업폴더 준비

```
mkdir my-app    // 폴더 생성
cd my-app
```
touch test.txt  // 파일 생성        
rm test.txt     // 삭제     
clear           // 터미널 창 비우기     
## 1. npm 설치

```
npm init -y 
```

-y는 다 yes 기본값으로 셋팅해주는 플래그    
init시 package.json이 생성됨.(package.json의 name에는 react-demo와 같은 '케밥케이스' 많이 사용)

## 2. .gitignore 파일 작성
```
touch .gitignore 
```

```
// .gitignore에 아래 추가
/node_modules/
/dist/
/.parcel-cache/ 
```
// 는 폴더임을 표시     
github ignore 프로젝트의 node 복붙 추천.

## 3. typescript 설치
```
npm i -D typescript
npx tsc --init
```
tsconfig.json 생성됨
```
// tsconfig.json에 추가
jsx:  'react-jsx'
```
서버에서 배포할땐 devDependencies를 빼고 배포할 수 있음     
'tsc'는 타입스크립트 컴파일러
'npx'는 node_modules 폴더보면 .bin(바이너리)라는 폴더에 실행할 수있는 파일이 있음     
./node_modules/.bin/tsc --help 명령어로 실행할 수 있는데,       
npx tsc --init 으로 간편하게 실행 가능.     
npx는 패키지를 직접 설치 안 했어도, npm 패키지들이 따로 관리(캐시)되는 곳이 있기에 실행을 해줌      
npm i -D typescript는 npm install --save-dev의 줄임말      

## 4. ESLint 설정

```
npm i -D eslint
npx eslint --init
```
ESLint는 린팅하는 정적 분석기
init시 질문을 함
```
1. config 설치여부? y      
2. eslint 어디에 쓸건지? 전부       
3. ESModule과 commonJS 중 어느거? jsmodules(esmoduls)
4. 무슨 프로젝트인지? React
5. typescript 사용여부? y
6. 코드실행환경? browser
7. 코드스타일 가이드 따를건지, 물어볼테니 직접 할건지? 가이드따름
8. 스탠다드,XO 중에? XO(에어비앤비를 제일 선호하지만 빠짐)
9. config파일 뭐로 할건지(JS, YAML, JSON)? JS (많이 사용)
10. 지금까지한거 설치해줄지? Y
11. 어떤 패키지매니저? npm(기본)
하면 .eslintrc.js 생성됨 // js가 안붙으면 json 파일 형식
```

```
// .eslintrc.js에 jest: true, 추가
env: {
    jest: true,
}
```

```
touch .eslintignore
```

```
// .eslintignore에 아래 추가
/node_modules/
/dist/
/.parcel-cache/ 
```
### eslint 자동 fix _ vsc 기본셋팅
```
mkdir .vscode
touch .vscode/settings.json 
```
```
// .vscode/settings.json에 추가
{
    "editor.rulers": [
        80
    ],
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "trailing-spaces.trimOnSave": true
}
```

npx eslint . // 하면 현재폴더 그아래에있는것들검사함        
npx eslint --fix . 

## 5. 리액트 설치
```
npm i react react-dom
npm i -D @types/react @types/react-dom
```

## 6. 테스팅 도구 설치
```
npm i -D jest @types/jest @swc/core @swc/jest \
    jest-environment-jsdom \
    @testing-library/react @testing-library/jest-dom
```
jest랑 swc 같이 사용.   
jest는 기본적으로 swc와 타입스크립트를 사용하지 않아서 jest.config.js 설정으로 변환 필요
```
// jest.config.js에 복붙, ./jest.setup는 지워도 됨.
https://github.com/ahastudio/CodingLife/blob/main/20220726/react/package.json
```

## 7. Parcel 설치
```
npm i -D parcel
```

```
// package.json에 source 추가 및 명령어 셋팅
 "source": "./index.html",
 "scripts": {
    "start": "parcel --port 8080",
    "build": "parcel build",
    "check": "tsc --noEmit",
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
    "test": "jest",
    "coverage": "jest --coverage --coverage-reporters html",
    "watch:test": "jest --watchAll"
  },
```
vsc에서 검색창 띄우기로 폴더 찾아 들어가기: 컨트롤+쉬프트+p       
그냥 parcel 하면 웹서버를 띄우는데 --port 8080하면 포트설정가능     
parcel build 하면 dist 폴더 생김    
check하면 컴파일하면 원래 자바스크립트 파일이 만들어지는데, 안생기고 체크만     


# 기본 리액트 셋팅해보기
// index.html

```
<!DOCTYPE html>
<html lang='ko'>
  <head>
    <meta charset='UTF-8'>
    <title>React</title>
  </head>
  <body>
    <div id='root'></div>
    <p>Hello, world</p> 
    <script type='module' src='./main.tsx'></script> // 2 
  </body>
<html>
```
원래는 esmodule로 돌아가는건데, 직접 쓰지않고 parcel이 변환해줌      
자동으로 parcel이 바로바로 업데이트해줌     

```
// main.tsx
import ReactDOM from 'react-dom/client';
import App from './App';

function main() {
	const element = document.getElementById('root');

	if (!element) {
		return;
	}

	const root = ReactDOM.createRoot(element);

	root.render(<App />);
}

main();
```

### import react from 'react' ESLint 안잡히게
```
//.eslintrc.js에서 extends에 추가
'plugin:react/jsx-runtime'
```

npm run lint 또는 npx eslint --fix // lint 실행


# 추가공부하면 좋을 사항
eslint나 prettier, tsconfig.json 항목들과 best practice
터미널부터 혼자서 그냥 많이 셋팅해보기 => 많이 해봐야 셋팅에 대한 자신감 생김