## 학습 키워드

- React란?
- React 컴포넌트
- React 리렌더링
- IoC(Inversion of Control)
- Library vs Framework

# 1. 용어정리

## React

    UI(사용자 인터페이스를 만들기위한) JS라이브러리
    특징
    01. React는 선언형이다.
    02. React는 컴포넌트 기반으로 재사용성이 뛰어나다.
    03. React는 Virtual DOM(가상돔)기반으로 가볍다.
    04. React 컴포넌트는 state와 props 을 가진다.

### 왜 리액트를 사용할까

    1. Virtual DOM의 사용
        실제로 DOM을 제어하지 않고, 중간에 Virtual DOM이라는 가상의 DOM이 변경될 때, 실제 DOM을 변경하도록 설계됨. 이러한 작업을 Reconciliation이라 함. 불필요한 렌더링 과정의 비효율성을 최소화하기 위해 탄생. 하지만 무조건 실제 DOM보다 좋고 빠른 것은 아님.
    2. 컴포넌트 단위의 개발
        작은 단위로 조립하듯이 합쳐서 개발. 가독성이 높아지고, 재사용성, 확장성, 결합성, 캡슐화 등의 이점이 있음.
    3. JSX지원
        JSX는 Javascript + xml로 리액트에서 element를 제공해줌.
        jsx를 얻기위한 알고리즘에 대한 구현이나 리렌더링 여부에 대한 알고리즘을 구현하진않음
        => 화면설계에 초점을 맞춘 높은 생산성
    4. 서버사이드렌더링과 클라이언트 사이드 렌더링 지원 가능
    5. 라이브러리이기 때문에 다른 라이브러리와 함께 사용 가능

## Reconciliation(재조정)과 key

    리액트 내부에서 기존의 VDOM과 변경사항이 생긴 VDOM에서 이루어지는 비교작업 과정을 Reconciliation이라고 함.
    1. 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.
    2. 개발자가 key prop을 통해, 여러 렌더링 사이에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.
    라는 가정을 통해 두 개의 트리를 비교할 때, 두 엘리먼트의 루트 엘리먼트부터 비교 한다고 함.
    이 때 엘리먼트 타입이 다르면 버리고 재구축하고, 같으면 속성을 확인하여, 변경된 속성만 갱신.
    근데 이 때 키를 이용해서 조금 더 효율적이게 작동함.

    아래 예시에서 트리 상의 같은 위치의 텍스트가 달라졌으므로 재렌더링 되는데, (마지막에 추가됐으면 마지막것만 했을 것) 너무 비효율적. key라는 것을 도입해, key속성이 같은 것끼리 비교하면 효율적임.
    (key는 항상 같은 부모 React엘리멘트에 대해서만 비교)

    (여기서 리렌더링은 render를 호출하는 것이지 React가 언마운트시키고 다시 마운트하는 것은 아님)

```
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
    <li key='Duke'>Duke</li>
    <li key='Villanova'>Villanova</li>
</ul>

<ul>
    <li key='Connecticut'>Connecticut</li>
    <li key='Duke'>Duke</li>
    <li key='Villanova'>Villanova</li>
</ul>
```

## 리액트 리렌더링

    얕은비교? 불변성?
    바뀐부분만 하기때문에 인풋창의 상태값이 그대로 있을 수 있음.

## React Component

    함수들이 React 엘리먼트를 반환하는 것
    컴포넌트는 독립적이며, 재사용 가능하게 만든 부품 조각.

### state와 props

    'state'는 컴포넌트내부에서 생성하고, 데이터가 변경될 수 있는 상태
    'props'는 외부(부모)컴포넌트로 상속받은 데이터이며 불변값이다.

### IoC(Inversion of Control)

    제어의 역전

``
// 🔴 React는 Layout이나 Article이 존재하는지 모릅니다.
// 컴포넌트를 직접 호출합니다.
ReactDOM.render(
Layout({ children: Article() }),
domContainer
)

// ✅ React는 Layout과 Article의 존재를 알게 됩니다.
// React가 컴포넌트를 호출합니다.
ReactDOM.render(
<Layout><Article /></Layout>,
domContainer
)

```


### Library vs Framework

## Thinking in React => react 작업 프로세스, 상태를 골라내는게 핵심

# UI 런타임으로서의 React(필독!!)
https://overreacted.io/ko/react-as-a-ui-runtime/

### 호스트 트리
React는 시간이 지남에 따라 변화할 수 있는 트리를 출력. DOM트리, ios계층구조, 심지어 json객체가 될 수 있음. 보통 UI를 표현하는데 사용.

### 호스트 객체
DOM환경에서 호스트객체는 일반적인 DOM노드.

### 렌더러
렌더러는 React가 특정 호스트 환경과 통신하고 호스트 객체를 관리

### React 엘리먼트
React 엘리먼트는 호스트 객체를 그릴 수 있는 일반적인 자바스크립트 객체
```

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

### 진입점
React가 컨테이너 호스트 객체 내부에 특정 React 엘리먼트 트리를 렌더링 할 수 있게 해주는 API로, ReactDOM.render함수.

### 파이버
파이버는 지역 상태가 실제로 있는 곳입니다. 지역 상태가 업데이트될 때 React는 해당 파이버의 자식들을 재조정하고 해당 컴포넌트들을 호출합니다.

# 추가공부하면 좋을 사항

리액트 beta 공식문서 한 페이지씩 읽고 정리해보기.
https://overreacted.io/ko/react-as-a-ui-runtime/ 다시 제대로 읽고 정리하기
이상한 키워드에 꽂힌 다음 가볍게 찾지말고, 먼저 중요한 키워드부터 하나라도 제대로 정리해보자.
```
