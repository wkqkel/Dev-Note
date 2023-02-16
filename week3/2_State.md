# React State

## Thinking in React

- “Step 3: Find the minimal but complete representation of UI state”
  상태가 뭔지를 찾자
- “Step 4: Identify where your state should live”
  걔네가 어디에 있게 할건지
- “Step 5: Add inverse data flow”

## React의 State

React의 state는 “변경”을 다루기 위한 요소. “Re-rendering”이란 주제에서 다뤄진다. 거칠게 이야기하면, 어떤 컴포넌트의 state가 바뀌면 해당 컴포넌트와 하위 컴포넌트를 다시 렌더링하게 된다.

아무렇게나 막 만들어도 되지만, 일관성과 효율을 위해 DRY 원칙을 따르는 SSOT를 만든다.

React State의 조건:

1. 변경돼야 함. 변경되지 않는 건 state로 다룰 가치가 없다.
2. 부모 컴포넌트가 props를 통해 전달한다면 state가 아님.
3. 다른 state나 props를 이용해 계산 가능하다면 state가 아님.
   다루는 상태가 너무 많으면 복잡함. TypeScript를 잘 쓰면 직접 관리하는 상태의 수를 줄여줄 수 있다.

그렇다면 그 상태를 누가 관리해야 할까? 더 정확히는, 상태를 누가 소유해야 할까?

(React만 쓴다면) 해당 상태에 의존적인 컴포넌트를 모두 포함하는 컴포넌트가 상태를 소유해야 함.

- [“Lifting State Up”](https://ko.reactjs.org/docs/lifting-state-up.html)
- [Sharing State Between Components](https://beta.reactjs.org/learn/sharing-state-between-components)

데이터라고 해서 다 state가 되는 건 아님. 리액트의 state라는게 있고, 얘는 변경을 다루기 위한 요소.

리렌더링 - 거칠게 얘기하면 해당컴포넌트와 하위컴포넌트의 state가 바뀌면 해당과 하위 컴포넌트를 다시 렌더링

아무렇게 만 만들어도 되지만, 가능하면
dry Don't repeat yoursef 중복배제 반복하지마라
: 소프트웨어 개발 원리의 하나로, 모든 형태의 정보 중복을 지양하는 원리

SSOT 단일진심공급원
: 데이터 스키마를 모든 데이터 요소를 한 곳에서만 제어 또는 편집하도록 조직하는 관례를 이른다.
데이터 요소로의 가능한 연결은 으뜸되는 "진실 공급원"의 위치에 대한 참조로만 이루어져, 으뜸되는 위치의 데이터 요소를 갱신하면 수정 사항 반영을 빠뜨릴 데이터의 사본이 존재할 가능성 없이 시스템 전체에 전파되게 된다.

```js
// bad 작동안하는건 아닌데, 이렇게 하지말라는거.
// you might not need effects
// 상태가 아니니까 상태처럼 관리 X
const [categories, setCategories] = useState<string[]>([]);

useEffect(()=>{
   setCategories(selectCategories(products))
}, [products])

// good
const categories = selectCategories(products)
```

위의 예시처럼, 지난 시간에 selectCategories라는 게 있었는데,
이를 상태로 관리했다면, products가 바꼈을 때, 같이 갱신해줘야 했음.
이렇듯 상태로 하게 되면, 중복으로 데이터를 갖게 돼서 둘 다 갱신을 안해주면, 틀리게 될 수 있으므로,
굳이 상태로 안해도 되는건 만들어서 사용.

상태가 늘어나서 값으로 하나씩 다룰 수 있는데, 그것 자체가 변할 순 없음.
그런데 타입스크립트를 활용하여 얘네들을 잘 묶어줘서 관리하는 상태의 수를 줄여줄 수는 있음.
잘 정의된 타입이나 인터페이스를 이용하면, 재사용할 때 굉장히 편해짐.

### Lifting State Up

원론적으로 얘기하면 해당 상태에 의존적인 컴포넌트를 모두 포함하는 최상위 컴포넌트가 소유해야함.

상태를 더이상 올라갈 필요가 없을 때까지 올림.

먼저 상태를 누가 쓰는지 보고, 해당 컴포넌트들이 겹치는, 만나는 컴포넌트에 상태가 있고, props로 내려줌.

`React.ChangeEvent<HTMLInputElement>`

HTMLInputElement는 브라우저에서 제공하는 그냥 돔의 타입이지만, ChangeEvent는 리액트의 이벤트.

### inverse Data Flow

하위 컴포넌트의 props로 함수를 전달. 흔히 콜백 함수라고 부름.

TypeScript(정확히는 JavaScript)는 함수가 일급(first-class) 객체다. 즉, 어떤 함수를 다른 함수에 인자로 넘겨주거나, 어떤 함수를 리턴값으로 사용할 수 있다. 익명 함수, 클로저 등과 함께 사용하면 시너지가 큼.

일급함수란 함수를 다른 변수와 동일하게 다루는 언어는 일급 함수를 가졌다고 표현합니다. 예를 들어, 일급 함수를 가진 언어에서는 함수를 다른 함수에 인수로 제공하거나, 함수가 함수를 반환할 수 있으며, 변수에도 할당할 수 있습니다.

데이터가 위에서 아래로 흐르는 것은 괜찮은데, 아래에서 위로 올릴 땐 어떻게 하느냐.

set함수를 프롭스로 전달

`타입 확장`

```js
type SetFilterTextComponentProps = {
  setFilterText: (value: string) => void,
};
// 또는  (value: string) => void 에 대해서 타입을 만들 수 도 있음.

type TextFieldProps = {
  // ...생략
} & SetFilterTextComponentProps;
```

### utils

```js
import Product from "../types/Product";

function normalize(text: string) {
  return text.trim().toLowerCase();
}

type FilterConditions = {
  filterText: string,
  inStockOnly: boolean,
};

export default function filterProducts(
  products: Product[],
  { filterText, inStockOnly }: FilterConditions
): Product[] {
  const filteredProducts = products.filter(
    (product) => !inStockOnly || product.stocked
  );
  const query = normalize(filterText);

  if (!query) {
    return filteredProducts;
  }

  const contains = (product: Product) =>
    normalize(product.name).includes(query);

  return filteredProducts.filter(contains);
}
```

위의 예시에서는 if문으로 처리를 해줬는데, let으로도 해줄 수 있음.
임뮤터블하게 하라고 하기도 하는데, 이는 바깥에서 봤을 때 임뮤터블이고 내부에서는 괜찮음.

또 filter의 조건이 여러 개가 되니까 객체로 넘겨줌.

```js
// FilterableProductTable
import { useState } from "react";

import ProductTable from "./ProductTable";
import SearchBar from "./SearchBar";

import Product from "../types/Product";

import filterProducts from "../utils/filterProducts";

type FilterableProductTableProps = {
  products: Product[],
};

function FilterableProductTable({ products }: FilterableProductTableProps) {
  const [filterText, setFilterText] = useState < string > "";
  const [inStockOnly, setInStockOnly] = useState < boolean > false;

  const filteredProducts = filterProducts(products, filterText);
  return (
    <div className="filterable-product-table">
      <SearchBar
        filterText={filterText}
        setFilterText={setFilterText}
        inStockOnly={inStockOnly}
        setInStockOnly={setInStockOnly}
      />
      <ProductTable products={filteredProducts} />
    </div>
  );
}

export default FilterableProductTable;
```

이렇게 props로 상태를 넘겨주게 되면 하나에 한쌍씩 컨트롤할게 너무 많아짐.
타입스크립트에서는 얘네를 묶어서 하나로 만들기도 함
External Store라는 것을 만들어서 처리하기도 함.

## 참고

아이템 목록에서 key가 value인 것만 선택하기.

```jsx
function select<ItemType, ValueType>(
	items: ItemType[],
	key: keyof ItemType,
	value: ValueType,
) {
	return items.filter((item) => item[key] === value);
}
```

## component와 props

컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나눔.

개념적으로 컴포넌트는 JavaScript 함수와 유사합니다. “props”라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환

- 컴포넌트 합성
  컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있습니다. 이는 모든 세부 단계에서 동일한 추상 컴포넌트를 사용할 수 있음을 의미합니다. React 앱에서는 버튼, 폼, 다이얼로그, 화면 등의 모든 것들이 흔히 컴포넌트로 표현됩니다.

- 컴포넌트 추출
  컴포넌트를 여러 개의 작은 컴포넌트로 나누는 것을 두려워하지 마세요.
  이 컴포넌트는 구성요소들이 모두 중첩 구조로 이루어져 있어서 변경하기 어려울 수 있으며, 각 구성요소를 개별적으로 재사용하기도 힘듭니다. 이 컴포넌트에서 몇 가지 컴포넌트를 추출하겠습니다.

- props는 읽기 전용

  모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다
  순수함수란 입력값을 바꾸려 하지 않고 항상 동일한 입력값에 대해 동일한 결과를 반환하는 함수

## Sharing State Between Components

https://beta.reactjs.org/learn/sharing-state-between-components

아코디언 컴포넌트가 있고, 부모 컴포넌트에서 해당 컴포넌트를 두개 불러온다.
이 때 하나가 열리면, 다른 하나는 닫히게 하고 싶을 때, 어떻게 해야할까?

서로 영향을 준다면, 해당 아코디언 컴포넌트에 상태가 있는게 아닌 부모컴포넌트에서 state를 만들어놓고 공유하는 방식으로 가능하다.

아래와 같은 방식

```js
<Panel
  isActive={activeIndex === 0}
  onShow={() => setActiveIndex(0)}
/>
<Panel
  isActive={activeIndex === 1}
  onShow={() => setActiveIndex(1)}
/>
```

Controlled and uncontrolled components

이 떄 state가 자식에 있을 경우, 부모가 영향을 끼칠 수 없기에 uncontrolled components라고 부른다.
컴포넌트를 만들 때, props를 통해 제어되어야 하는 정보와 state를 통해 제어되지 않아야 하는 정보를 구분하면 유용하다.
