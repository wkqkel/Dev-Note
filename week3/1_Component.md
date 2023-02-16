# React Component

## Thinking in React

> [Thinking in React](https://beta.reactjs.org/learn/thinking-in-react)

- “Step 1: Break the UI into a component hierarchy”

  UI를 어떤 계층 구조로 쪼개는 것. 좀 거칠게 얘기하면, 돔트리 처럼 컴포넌트 트리를 만든다고 생각.

- “Step 2: Build a static version in React”

  리액트로 정적인 버전을 만들어라(동작 X)

동적으로 작동하지만, 처음에는 정적인 것을 만드는 것에서부터 시작. 이후 상태를 관리함으로써 동적인 것을 만듬.

이 작업은 예전의 프론트엔드, 퍼블리싱의 작업과 크게 다르지 않음. => 변하지않는 프론트엔드의 기초.

## 데이터

**REST API**

- GET, POST, PUT/PATCH, DELETE (CRUD)
- Resource 중심

**GraphQL**

- Graph 자료 구조
- Query에서 얻고자 하는 걸 지정
- Query(Read), Mutation(Command: Create, Update, Delete), Subscription(Event)

B/E에서 위와 같은 JSON 형태를 돌려주는 API를 제공.

rest api는 기존의 fetch API를 이용해 기본적인 crud를 리소스 중심으로 조작.

그에반해 graphQL은 graph라는 자료구조를 이용해, query에서 얻고자하는 것을 스키마처럼 지정해서 넣어줌.

예를 들어, rest api는 게시물을 요청하면, 거기 있는 댓글도 같이 오는 반면, graphql은 쿼리 자체에서 지정해줌.

> JSON이란?

[MDN_JSON으로 작업하기](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/JSON)

JS Object Notation 자바스크립트 객체 표기법

데이터를 교환하기 위해 만들어짐. 프론트와 백이 다른 언어로 뭔가를 만들었는데, 그대로 보낼 수 없음.

http 사용 시 문자열로 데이터를 주고 받는데, 오브젝트 형태를 만족시킬 수 있도록 만든 포멧.

> F/E는 이 데이터를 사용자가 볼 수 있도록 UI를 구성한다. React는 선언형(HTML과 유사한 모양의 DSL을 사용)으로 UI를 구성할 수있다.

DSL이란 도메인 특화 언어로, 특정 도메인에 해당하는 문제를 좀 풀기 쉽게 한 언어. html이 대표적인 dsl.
리액트는 jsx를 사용함으로써 선언형으로 UI를 구성할 수 있게 해줌.

## 컴포넌트 계층 구조

- “Component-Based”
- “Build encapsulated components that manage their own state, then **compose** them to make **complex UIs**.”

복잡한 UI를 만들기 위해 자신의 상태를 캡슐화하고 있는 컴포넌트들을 만들어서 조립하는 것이 리액트의 장점.

간단한 컴포넌트를 조립해서 복잡한 UI를 만들어낸다. 만약 컴포넌트가 복잡하다면, 리액트의 장점을 못 살리고 있음.

## 어떻게 (잘) 나눌 것인가에 대한 기준

우리가 원하는 UI를 구성할때, UI를 통으로 만들면, 비슷한 뭔가를 만들때 전체를 복붙한 다음에 조금만 고치거나 하게되는데. 그렇게 안하고 다 작게 나눠두면(컴포넌트를 잘 만들면), 부품을 다르게 조합하거나 하나의 부품만 바꿔도, 우리가 원하는 걸 만들수있음.

복잡한 컴포넌트를 작고 심플한 컴포넌트를 조합해서 가지수를 폭발적으로 늘릴 수 있음.
이 때 작고 심플함의 기준.

- [SRP (Single Responsibility Principle)](https://ko.wikipedia.org/wiki/단일_책임_원칙)

`SRP 단일책임원칙`

객체지향에서 많이 다루는 5가지 원칙 중 하나(이렇게 하면 견고한 객체지향 프로그램을 만들 수 있더라 5가지)

거기에 나오는 클래스를 컴포넌트로 생각.

클래스는 객체지향 프로그래밍을 지원하는 언어에서 컴포넌트를 구현할 수 있는 기술 중에 하나.

하나의 책임을 가지고 캡슐화해야 한다. => 즉, 하나의 컴포넌트가 변경되는 것은 하나의 이유여야 한다.

컴포넌트를 쪼개놓으면, 사소한 변경이 있을 때, 길다란 코드에서 막 여러개를 고치지않고 관련된 것 하나만 고칠 수 있다.

- CSS, Design’s Layer → 이미 알고 있는 기준을 재활용.

기존에 html의 id 또는 클래스 (주로 클래스) 및
디자인 측면에서도 트리 형태의 레이어로 많이 나누는데, 이를 활용하여 나눔.

- Information Architecture (JSON Schema의 영향)

→ 실제로 엄청 많이 쓰게 됨. 자연스러운 SRP를 위해서 사실상 강제됨.(연습 많이 하면 늘게됨)

JSON과 UI의 위계가 다를 수 있음.

그럴 땐 백엔드에서 얻자말자 재가공을 하기도 하고(리덕스를 이용한 노멀라이즈), 보여줄 때 형태를 바꾸기도 하고, 애초에 백엔드에 요청해서, 프론트에서 이런 식으로 보여줄거기 때문에 이런 형태가 필요하다. 라는 여러 가지 대등이 가능

- [Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/)

우리가 잘 알고 있는 계층형 구조를 몇 가지 카테고리로 묶은 방법.

아톰+분자(MOLECULES)+유기체(ORGANISMS)+템플릿+페이지

이대로 만드는 것이 아닌, 이미 우리가 쓰고 있는 개념적인 것.

## Extract Function

아주 흔히 쓰이는 SRP를 위한 수단. 변화의 크기(영향 범위)를 제약한다.

일단 길게 코드를 작성하고, 적절히 자를 수 있는 부분이 보일 때 “함수로 추출”한다.

또는 코드를 작성하기 어려운 상황에 직면했을 때 함수로 추출. 바로 다른 파일을 만들어야 한다고 생각하지 않아도 됨.

컴포넌트 나누는 기준이 애매하면 다시 하나의 컴포넌트로 합쳤다가(Inline Method) 다시 나눠줘도 됨. => `이 부분 이해가 잘 안됨`

## Thinking In React 코딩하기

### `테이블태그 작성`

th는 표의 제목(table head), tr은 가로줄(table row), td는 셀(table data)
colSpan은 차지하는 칸수.

### `checkbox 만드는 2가지 방법`

```js
<div>
  <input type="checkbox" id="only-stock" />
  <label htmlFor="only-stock">
    Only show products in stock
  </label>
<div>

<div>
 <label>
    <input type="checkbox"  />
    Only show products in stock
 </label>
<div>
```

### `임포트 순서`

컴포넌트 먼저 써주고, 타입-> 유틸 하나씩 띄워서 써주면, 분리됨.

### `Record`

function select<T>(items: T[], field,value)

특정 키와 벨류의 타입을 지정할 때 Record를 사용. Record<keyType, valueType>

key는 스트링이 될거고 나머지는 T

```js
export default function select(
  items: Record<string, T>[],
  field: string,
  value: T
) {
  return items.filter((item) => item[field] === value);
}
```

### `useRef 활용`

내부에서 유지해야할 때 제일 쉬운 것 중에 하나가 useRef 사용

```ts
const id = useRef<string>`checkbox-${label}`.replace(/ /g, "-").toLowerCase();

<input type="checkbox" id={id.current} />;
```

### `Props type`

```ts
type ProductRowProps = {
  product: Product;
};
```

### `조건부 클래스네임`

```js
className={!product.stocked && 'soldout'}
```

## Props

> [Passing Props to a Component](https://beta.reactjs.org/learn/passing-props-to-a-component)

> [Components와 Props](https://ko.reactjs.org/docs/components-and-props.html)

나눠진 컴포넌트를 서로 연결하는 방법.

TypeScript를 잘 쓰거나 잘못 쓰게 되는 포인트 중 하나. 적절한 균형점을 잡는 게 중요하다.

테스트 코드를 작성하면 재사용성을 평가하기 쉬워짐.

Props를 넘겨줄 때

방법1은, product={product} 넘겨주고,
방법2는 name={product.name} price={product.price}를 넘겨줌.

타입스크립트 사용 시에는 여러 개를 넘겨주기보다 하나를 적절하게 묶어서 넘겨주면, 변경이 용이.

---

`reflect` 추후 공부

```js
export default function select<T1 extends object, T2>(
  items: T1,
  field: string,
  value: T2,
) : T1[] {
  return items.filter((item) => Reflect.get(item, field) === value);
}
```

### 어떤 식으로 전개하는지

0. UI를 기준으로 자리를 잡고,
1. 간단한 HTML을 작성해준 뒤
2. 데이터를 적용시키고,
3. 컴포넌트로 분리(이 때 컴포넌트의 이름은 className이나 디자인 등을 참고하면 좋음)
4. 컴포넌트 내에 함수를 유틸로 분리

```live
export default function App() {
  return (
    <div>
      <div>
        <div>
          <div>
            <input type="text" placeholder="Search..." />
          </div>
        <div>
          <input type="checkbox" id="only-stock" />
          <label htmlFor="only-stock">
            Only show products in stock
          </label>
        </div>
      </div>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Price</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th colSpan={2}>
              Name
            </th>
          </tr>
          <tr>
            <td>Name</td>
            <td>Price</td>
          </tr>
        </tbody>
      </table>
    </div>
  );
}
```

### 폴더구조

```mkdir
├─ .eslintignore
├─ .eslintrc.js
├─ .gitignore
├─ .parcel-cache
│ ├─ data.mdb
│ └─ lock.mdb
├─ .vscode
│ └─ settings.json
├─ README.md
├─ dist
│ ├─ index.96e2502d.js
│ ├─ index.96e2502d.js.map
│ └─ index.html
├─ index.html
├─ jest.config.js
├─ package-lock.json
├─ package.json
├─ src
│ ├─ App.tsx
│ ├─ components
│ │ ├─ CategoryRow.tsx
│ │ ├─ CheckBoxField.tsx
│ │ ├─ FilterableProductTable.tsx
│ │ ├─ ProductRow.tsx
│ │ ├─ ProductTable.tsx
│ │ ├─ ProductsInCategory.tsx
│ │ └─ SearchBar.tsx
│ ├─ main.test.tsx
│ ├─ main.tsx
│ ├─ types
│ │ └─ Product.ts
│ └─ utils
│ ├─ selectCategories.ts
│ └─ selectProducts.ts
└─ tsconfig.json
```

### 궁금한점

이번 주차 강의에서는 큰 컴포넌트에서 작은 컴포넌트로 쪼개는 방식으로 강의가 진행됐는데,

예를 들어 테이블과 서치폼을 분리시키고, 또 그 안의 체크박스를 분리시키는 방식이었는데,

이와 다르게 체크박스를 먼저 만들고 더 큰 서치폼을 만들고 하는 방식은 어떨까.
