# 1. JSX

> JSX란? XML-like syntax extension to ECMAScript

JSX라 하며 JavaScript를 확장한 문법, JSX는 React “엘리먼트(element)” 를 생성

> React에서 JSX를 사용하는 목적

JSX 사용이 필수가 아니지만, JavaScript 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다

이러한 접근방식이 React의 선언적 API를 가능하게 한다.

> Syntactic sugar

근본적으로, JSX는 React.createElement(component, props, ...children) 함수에 대한 문법적 설탕을 제공할 뿐

Babel은 JSX를 React.createElement() 호출로 컴파일하고, JavaScript 코드와 1:1로 매칭된다.

> React.createElement

createElement(type, props, ...children)

React.createElement()는 버그가 없는 코드를 작성하는 데 도움이 되도록 몇 가지 검사를 수행하며, 기본적으로 다음과 같은 객체를 생성(리액트 앨리먼트)

```js
// 주의: 다음 구조는 단순화되었습니다
const element = {
  type: "h1",
  props: {
    className: "greeting",
    children: "Hello, world!",
  },
};
```

> React Element

위의 객체를 “React 엘리먼트”라고 하며, 화면에서 보고 싶은 것을 나타내는 표현이다.

React는 이 객체를 읽어서, DOM을 구성하고 최신 상태로 유지하는 데 사용한다.

또 엘리먼트는 불변객체로, 특정 시점의 UI를 보여준다.(리액트 앨리먼트는 객체를 앱 컴포넌트에 리턴함으로써, 리액트에게 다음에 뭘 할지 알려준다.)

UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고 이를 root.render()로 전달하는 것

> React StrictMode

StrictMode는 애플리케이션 내의 잠재적인 문제를 알아내기 위한 도구

개념적으로 React는 두 단계로 동작

렌더링 단계는 render를 호출하여 이전 렌더와 결과값을 비교

커밋 단계는 React가 변경 사항을 반영하는 단계입니다(React DOM의 경우 React가 DOM 노드를 추가, 변경 및 제거하는 단계)

메서드들은 여러 번 호출될 수 있기 때문에, 부작용을 포함하지 않는 것이 중요

함수를 의도적으로 이중으로 호출하여 문제가 되는 부분을 발견할 수 있게 도와준다.

> VDOM(Virtual DOM)이란?

Virtual DOM (VDOM)은 UI의 이상적인 또는 “가상”적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” DOM과 동기화하는 프로그래밍 개념.

React의 세계에서 “virtual DOM”이라는 용어는 보통 사용자 인터페이스를 나타내는 객체

> DOM이란?

> DOM과 Virtual DOM의 차이

브라우저 DOM 엘리먼트와 달리 React 엘리먼트는 일반 객체이며(plain object) 쉽게 생성할 수 있다.

Myth: React is “faster than DOM”. Reality: it helps create maintainable applications, and is _fast enough_ for most use cases.

빠르기때문에 쓰는게 아니라 유지보수 가능하고 충분히 빠르

> Reconciliation(재조정) 과정은 무엇인가?

리액트는 선언적 api를 제공하기 때문에 우리는 매번 무엇이 바뀌었는지 걱정할 필요가 없다.

render() 함수는 새로운 React 앨리먼트 트리를 반환하는데, 이 때 트리에 맞게 가장 효과적으로 UI를 갱신하는 비교 알고리즘을 사용하는데, 이러한 과정을 재조정 이라고 한다.

이는 거의 대부분의 상황에 맞는 아래 두 가지 가정을 기반하여 O(n)의 알고리즘을 구현했다.

1. 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.

2. 개발자가 key prop을 통해, 여러 렌더링 사이에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.

> 비교 알고리즘 (Diffing Algorithm)

리액트는 두 개의 트리를 비교할 때, 두 앨리먼트의 루트 앨리먼트부터 비교한다.

앨리먼트 타입이 다른 경우에는 React는 이전 트리를 버리고 완전히 새로운 트리를 구축한다.

엘리먼트의 타입이 같은 경우에는 두 엘리먼트의 속성을 확인하여, 동일한 내역은 유지하고 변경된 속성들만 갱신한다.

즉, render() 메서드가 호출되고 비교 알고리즘이 이전 결과와 새로운 결과를 재귀적으로 처리한다.

> Keys

근데 이렇게 단순하게 구현하면, 리스트의 맨 앞에 엘리먼트를 추가하는 경우 성능이 좋지 않다.

이러한 문제를 해결하기 위해, React는 key 속성을 지원한다.

React는 key를 통해 기존 트리와 이후 트리의 자식들이 일치하는지 확인한다.

이 때, 배열의 인덱스를 key로 사용할 경우 재배열되는 경우 비효율적으로 동작할 수 있다.
