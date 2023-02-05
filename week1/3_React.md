# 4. React

- React란?
- React 컴포넌트
- React 리렌더링
- IoC(Inversion of Control)
- Library vs Framework

## React

`참고자료`

[**React 공식문서**](https://ko.reactjs.org/) → 최근에 업데이트가 됨.

[**React Beta 문서**](https://beta.reactjs.org/) -> 이것부터 읽는 걸 권장

- React로 작업하는 프로세스는 [Thinking in React](https://beta.reactjs.org/learn/thinking-in-react)를 참고. “상태”를 골라내는 게 핵심이다.
- 한국어로 읽고 싶다면 [예전 문서의 설명](https://ko.reactjs.org/docs/thinking-in-react.html)만 살짝 참고하자(코드는 참고하지 말 것!).
- [React 코어 개발자가 쓴 React에 대한 이해를 돕는 글](https://overreacted.io/ko/react-as-a-ui-runtime/) (필독!)

---

## 렌더링

[creatRoot](https://beta.reactjs.org/reference/react-dom/client/createRoot)

```ts
function Greeting() {
  return <p>Hello, world!</p>;
}

function main() {
  const element = document.getElementById("root");

  if (!element) {
    return;
  }

  const root = ReactDOM.createRoot(element);

  root.render(<Greeting />);
}

main();
```

여러 개의 Root를 만들거나, 여러 번 render해도 된다.

여러 번 render하는 카운터 예제. 변경된 부분만 업데이트하기 때문에 하단 입력 컨트롤에 입력한 값이 그대로 유지된다.

[updating-a-root-component](https://beta.reactjs.org/reference/react-dom/client/createRoot#updating-a-root-component)

## 리렌더링

- [React는 컴포넌트를 언제 다시 리렌더링 할까요?](https://velog.io/@surim014/react-rerender)
- [왜 리액트에서 리렌더링이 발생하는가.](https://medium.com/@yujso66/%EB%B2%88%EC%97%AD-%EC%99%9C-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EB%A6%AC%EB%A0%8C%EB%8D%94%EB%A7%81%EC%9D%B4-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94%EA%B0%80-74dd239b0063)
- [React 렌더링 동작에 대한 (거의) 완벽한 가이드](https://velog.io/@superlipbalm/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior)

## Library vs Framework

[면접 때 종종 나오는 (쓸모 없는) 질문인 “React는 프레임워크인가요, 라이브러리인가요?”에 대한 React 개발자의 답변](https://twitter.com/trueadm/status/1194567962784653312)

[제어의 역전](https://martinfowler.com/bliki/InversionOfControl.html)(IoC: Inversion of Control)

제어의 역전이 Framework의 주요한 특징이고, React는 IoC를 통해 상태와 업데이트가 얽힌 복잡한 상황을 간단히 선언형 UI로 구성하는 혜택을 누린다(이게 바로 React의 첫 번째 특징이다). 그 누구도 매번 root를 render하는 방식으로 쓰면서 “이게 라이브러리지!”라며 감탄하지 않는다.

하지만 일반적으로는 (Martin Fowler의 개탄처럼) IoC는 IoC 컨테이너와 엮여서 DI와 동의어처럼 쓰이고, Next.js, Remix 같은 걸 Framework이라고 부르니 면접 때 괜히 이런 걸로 싸우지는 말자. “리액트 개발자가 이렇게 이야기했다니까요!”라고 해봐야 서로 감정만 상할 뿐이다.

---

## 추가자료

`왜 리액트를 사용할까`

- Virtual DOM의 사용
- 실제로 DOM을 제어하지 않고, 중간에 Virtual DOM이라는 가상의 DOM이 변경될 때, 실제 DOM을 변경하도록 설계됨.
  - 이러한 작업을 Reconciliation이라 함. 불필요한 렌더링 과정의 비효율성을 최소화하기 위해 탄생.
  - 하지만 무조건 실제 DOM보다 좋고 빠른 것은 아님.
- 컴포넌트 단위의 개발
  - 작은 단위로 조립하듯이 합쳐서 개발.
  - 가독성이 높아지고, 재사용성, 확장성, 결합성, 캡슐화 등의 이점이 있음.
- JSX지원
  - JSX는 Javascript + xml로 리액트에서 element를 제공해줌.
  - jsx를 얻기위한 알고리즘에 대한 구현이나 리렌더링 여부에 대한 알고리즘을 구현하진않음
  - 화면설계에 초점을 맞춘 높은 생산성
- 서버사이드렌더링과 클라이언트 사이드 렌더링 지원 가능
- 라이브러리이기 때문에 다른 라이브러리와 함께 사용 가능

`Reconciliation(재조정)과 key`

리액트 내부에서 기존의 VDOM과 변경사항이 생긴 VDOM에서 이루어지는 비교작업 과정을 Reconciliation이라고 함.

- 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.
- 개발자가 key prop을 통해, 여러 렌더링 사이에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.

라는 가정을 통해 두 개의 트리를 비교할 때, 두 엘리먼트의 루트 엘리먼트부터 비교 한다고 함.
이 때 엘리먼트 타입이 다르면 버리고 재구축하고, 같으면 속성을 확인하여, 변경된 속성만 갱신.
근데 이 때 키를 이용해서 조금 더 효율적이게 작동함.

아래 예시에서 트리 상의 같은 위치의 텍스트가 달라졌으므로 재렌더링 되는데, (마지막에 추가됐으면 마지막것만 했을 것) 너무 비효율적. key라는 것을 도입해, key속성이 같은 것끼리 비교하면 효율적임.
(key는 항상 같은 부모 React엘리멘트에 대해서만 비교)

(여기서 리렌더링은 render를 호출하는 것이지 React가 언마운트시키고 다시 마운트하는 것은 아님)

```js
// before
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

// after
<ul>
  <li key="Duke">Duke</li>
  <li key="Villanova">Villanova</li>
</ul>

<ul>
  <li key="Connecticut">Connecticut</li>
  <li key="Duke">Duke</li>
  <li key="Villanova">Villanova</li>
</ul>
```

`React Component`

함수들이 React 엘리먼트를 반환하는 것

컴포넌트는 독립적이며, 재사용 가능하게 만든 부품 조각.

`state와 props`

'state'는 컴포넌트내부에서 생성하고, 데이터가 변경될 수 있는 상태

'props'는 외부(부모)컴포넌트로 상속받은 데이터이며 불변값이다.

`IoC(Inversion of Control)`

```js
// 🔴 React는 Layout이나 Article이 존재하는지 모릅니다.
// 컴포넌트를 직접 호출합니다.
ReactDOM.render(Layout({ children: Article() }), domContainer);

// ✅ React는 Layout과 Article의 존재를 알게 됩니다.
// React가 컴포넌트를 호출합니다.
ReactDOM.render(
  <Layout>
    <Article />
  </Layout>,
  domContainer
);
```

## UI 런타임으로서의 React

[UI 런타임으로서의 React(필독!!)](https://overreacted.io/ko/react-as-a-ui-runtime/)

`호스트 트리`

React는 시간이 지남에 따라 변화할 수 있는 트리를 출력. DOM트리, ios계층구조, 심지어 json객체가 될 수 있음. 보통 UI를 표현하는데 사용.

`호스트 객체`

DOM환경에서 호스트객체는 일반적인 DOM노드.

`렌더러`

렌더러는 React가 특정 호스트 환경과 통신하고 호스트 객체를 관리

`React 엘리먼트`

React 엘리먼트는 호스트 객체를 그릴 수 있는 일반적인 자바스크립트 객체

```js
// JSX는 아래 오브젝트를 만들기 위한 편의구문입니다.
// <dialog>
// <button className="blue" />
// <button className="red" />
// </dialog>
{
  type: 'dialog',
  props: {
  children: [{
      type: 'button',
      props: { className: 'blue' }
    }, {
      type: 'button',
      props: { className: 'red' }
    }]
  }
}

```

`진입점`

React가 컨테이너 호스트 객체 내부에 특정 React 엘리먼트 트리를 렌더링 할 수 있게 해주는 API로, ReactDOM.render함수.

`파이버`

파이버는 지역 상태가 실제로 있는 곳입니다. 지역 상태가 업데이트될 때 React는 해당 파이버의 자식들을 재조정하고 해당 컴포넌트들을 호출합니다.
