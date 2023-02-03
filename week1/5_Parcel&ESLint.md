## 학습 키워드

- Bundler(번들러)
    - Parcel
- Lint(린트)
    - ESLint


# Parcel

### Zero Configuration
- 특별한 설정 없이 바로 사용 가능한 빌드 도구. 내부적으로 SWC를 사용해 기존 도구보다 빠르다(ES Module을 적극 활용하는 Vite도 엄청나게 빠름).
- 참고:
    - [https://github.com/ahastudio/til/tree/main/parcel](https://github.com/ahastudio/til/tree/main/parcel)
    - [https://github.com/ahastudio/til/tree/main/vite](https://github.com/ahastudio/til/tree/main/vite)

1. package.json 파일에 source 속성 추가.

```
"source": "./index.html", // 또는 "index.html"
```
설정해주면 매번 npx parcel index.html (port ~)로 실행할 필요 없이 npx parcel 하게 해줌.

2. parcel-reporter-static-files-copy 패키지 설치 후 `.parcelrc` 파일 작성.   
이렇게 하면 static 폴더의 파일을 정적 파일로 Serving할 수 있다(이미지 등 Assets).

```
{
  "extends": ["@parcel/config-default"],
  "reporters":  ["...", "parcel-reporter-static-files-copy"]
}
```

### 빌드 + 정적 서버 실행
```
npx parcel build

npx servor ./dist
```

servor: A dependency free dev server for modern web application development

### 강의내용
간단하게 원래는 번들러라고 하는 것을 빌드툴이라고 부름.
빌드가 뭐냐면, 여러 가지를 하는데, 제일 큰건 번들러의 역할.
번들러는 여러 개의 자바스크립트 파일이 있는데, import, export가 지금은 es모듈에서 지원하는 표준이지만, 예전에는 브라우저에서 직접 지원하지 않아서, 파일들을 하나로 합쳐줘야해 했는데, 그렇게 해주는 과정을 번들링, 해주는 도구를 번들러라고 함.
이런 도구를 어차피 타는 김에, 최신 지원하지 않는 브라우저를 위해 최신 버전의 자바스크립트를 옛날 버전으로 변환해주는 바벨 같은 게 있고, 아니면 아예 타입스크립트를 자바스크립트로 변환해주는 역할 등 까지 총칭해서 빌드라고 함.

Parcel2로 넘어오면서 내부적으로 swc라는 rust로 만든 타입스크립트 컴파일러를 사용해 기존도구보다 엄청 빠름(ESModule을 활욜하는 비트(vite)도 엄청 빠름)

# ESLint

eslint 린팅도구 

무엇을 위해서?
- 스타일 통일
- 잠재적 문제 발견
- 베스트 프랙티스 추천 → 최신 트렌드를 학습하는데 활용!

가만히 있는 소스코드를 가지고 분석하는 정적분석에 속해서 오래 걸리지 않음.

## vsc 기본셋팅_저장시 자동 fix
mkdir .vscode
.vscode/settings.json 
```
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

npm run check // tsc --noEmit 
npm run lint 

npm run lint && npm run check // 엄청 많이 사용.

가능하면 바닥부터 셋팅 매일매일 반복해서 만들어보기 추천해줌.
바닥부터 만드는거 익숙해야함.
