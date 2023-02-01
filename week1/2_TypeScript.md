## 학습 키워드

- REPL
- TypeScript
  - Interface vs Type
  - 타입 추론
  - Union Type vs Intersection Type
  - Optional Parameter

# 1. 용어정리

## REPL
    "REPL"이란 Read-Eval-Print-Loop의 약자로 컴파일 과정 없이 즉석에서 코드를 입력해 결과를 바로 알 수 있는 방식을 말함.  
    개발 시에 코드를 즉시 테스트함으로써 디버깅을 할 수 있음.    
    npx ts-node 를 사용하여 repl환경을 사용할 수 있음.

## TypeScript
    타입을 가진 자바스크립트로, 자동완성과 실시간 오류검사를 제공해줌.

## Interface(인터페이스) vs Type(타입별칭)
    둘다 해당 키워드를 사용하여 반복되는 타입을 인터페이스 또는 타입으로 지정해 재사용가능하게 합니다.
    인터페이스는 extends키워드 타입은 & 연산자를 사용해 확장한다.
    인터페이스는 동일한 이름을 통해 재정의함으로써 선언적 확장이 가능하지만 type는 생성된 뒤에는 달라질 수 없다.

```
interface Itest1 {
	a: string;
}

interface Itest1 {
	b: string;
}

const test1: Itest1 = {
	a: 'a',
	b: 'b',
};
```

computed value는 type은 사용가능하지만, interface는 불가
```
type keyType = 'a' | 'b';

type type1 = {
  [key in keyType]: string
}

const typeA: type1 = {
  a: 'a',
  b: 'b',
}

interface interface1 {
  [key in keyType]: string  // 에러 
}
```

## 타입추론
    타입을 일일히 입력 안해도 타입을 추론해줌. 적절히 활용

## 유니온과 인터섹션타입
    유니온 | 인터섹션 &   
    유니온은 합집합 속성, 인터섹션은 교집합 속성(교집합이 더 작은 집합)
    합집합은 매개변수를 제한할 수 있고, 교집합은 타입을 간단하게 확장할 수 있음.

```
type Category = 'food' | 'toy' | 'bag';

function fetchProducts({ category }: { category: Category }) {
  console.log(`Fetch ${category}`);
}
```

```
type Measure = { radius: number };
type Style = { color: string };

// typed { radius: number; color: string }
type Circle = Measure & Style;
```

## 옵셔널 파라미터
파라미터가 올수도있고 안올수도있을때 ?(옵셔널 파라미터)를 사용하거나 =을 사용해 기본값 설정할 수 있다.
```
function greeting({ name , age }: { name: string; age?: number; } = { name: 'hong' }): string {
  return age ? `${name} (${age})` : name;
}
```

## 튜플 타입
    let arr : [string, number] // 아주 깐깐하게 잡아주려할때. 갯수도 지켜야함.
## Generics 제네릭
  제네릭은 타입을 마치 함수의 파라미터 개념으로 받아, 다양한 타입으로 재사용가능하게 해주는 문법    
  꺽새<>를 이용해 사용.
```
function identity<Type>(arg: Type): Type {
    return arg;
}
```
# Utility 추후 추가 공부 필요_ 자주 쓰일만한 것 먼저!
https://www.typescriptlang.org/docs/handbook/utility-types.html   
제네릭하고 익숙해지면 더 보기
### Awaited<Type>
```
type A = Awaited<Promise<string>>; // type A = string
// type A는 스트링으로 잡힘. 프로미스에 담긴 스트링을 스트링으로 지정하고싶을 경우 사용
```

### Record<Keys, Type>
Keys가 key가 되고, Type이 value가 되는 객체 타입
```
interface CatInfo {
  age: number;
  breed: string;
}
 
type CatName = "miffy" | "boris" | "mordred";
 
const cats: Record<CatName, CatInfo> = {
  miffy: { age: 10, breed: "Persian" },
  boris: { age: 5, breed: "Maine Coon" },
  mordred: { age: 16, breed: "British Shorthair" },
};
```
### Pick<Type, Keys>
기존 타입에서 필요한 타입만 추출해서 새로운 타입
```
type User = {
    age: number;
    gender: string;
    country: string;
    city: string
};
// type Demographic = { age: number: gender: string; };
type Demographic = Pick<User, 'age'|'gender'>;
```

### Omit<Type, Keys>
기존 타입에서 특정 타입을 뺀 새로운 타입
```
interface Todo {
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
}

type TodoInfo = Omit<Todo, "completed" | "createdAt">;
 
const todoInfo: TodoInfo = {
  title: "Pick up kids",
  description: "Kindergarten closes at 5pm",
};
```

### ReturnType<T>
함수의 반환 타입을 복제하는 대신 사용
```
function createCircle() {
    return {
        kind: 'circle' as const,
        radius: 1.0
    }
}
// circle: { kind: 'circle'; radius: number }
function transformCircle(circle: ReturnType<typeof createCircle>) {
    ...
}
```


### Partial<Type>
특정 타입의 부분 집합을 만족하는 타입을 정의
모튼 프로퍼티가 옵셔널로 들어간 것
```
interface Address {
  email: string;
  address: string;
}

type MyEmail = Partial<Address>;
const me: MyEmail = {}; // 가능
const you: MyEmail = { email: "noh5524@gmail.com" }; // 가능
const all: MyEmail = { email: "noh5524@gmail.com", address: "secho" }; // 가능
```

# 더 좋은 타입스크립트 프로그래머로 만드는 11가지 팁
https://velog.io/@lky5697/11-tips-that-help-you-become-a-better-typescript-programmer

## 옵셔널 필드 대신 구분된 유니온 사용
before
```
type Shape = {
  kind: 'circle' | 'rect';
  radius?: number;
  width?: number;
  height?: number;
}

function getArea(shape: Shape) {
  return shape.kind === 'circle' ? 
    Math.PI * shape.radius! ** 2
    : shape.width! * shape.height!;
}
```
after
```
type Circle = { kind: 'circle'; radius: number };
type Rect = { kind: 'rect'; width: number; height: number };
type Shape = Circle | Rect;

function getArea(shape: Shape) {
    return shape.kind === 'circle' ? 
        Math.PI * shape.radius ** 2
        : shape.width * shape.height;
}
```

## 타입단언(as)를 피하기 위한 타입명제(is) 사용
```
type Circle = { kind: 'circle'; radius: number };
type Rect = { kind: 'rect'; width: number; height: number };
type Shape = Circle | Rect;

function isCircle(shape: Shape) {
  return shape.kind === 'circle';
}

function isRect(shape: Shape) {
  return shape.kind === 'rect';
}

const myShapes: Shape[] = getShapes();

// 타입스크립트가 필터링 된 것을 모르기 때문에 에러가 발생합니다.
// 타입 좁히기
const circles: Circle[] = myShapes.filter(isCircle);

// 다음과 같은 단언을 추가하고 싶을 수 있습니다.
// const circles = myShapes.filter(isCircle) as Circle[];
```
보다 우아한 해결책은 isCircle과 isRect를 타입 명제를 반환하도록 변경하여 filter 호출 후 타입스크립트가 타입을 좁힐 수 있도록 도와주는 것
```
function isCircle(shape: Shape): shape is Circle {
    return shape.kind === 'circle';
}

function isRect(shape: Shape): shape is Rect {
    return shape.kind === 'rect';
}

...
// 이제 Circle[] 타입을 올바르게 유추합니다.
const circles = myShapes.filter(isCircle);
```

## as const
as const 는 가장 구체적인 타입으로 범위를 좁힘.
```
let a = [1, 2]; // typed: number[]
let b = [1, 2] as const; // typed: [1, 2]

// typed { kind: 'circle; radius: number }
let circle = { kind: 'circle' as const, radius: 1.0 };
// circle이 const 키워드를 사용해 초기화 되지 않았다면
// 다음이 동작하지 않습니다.
let shape: { kind: 'circle' | 'rect' } = circle;
```

# 추가공부하면 좋을 사항 
infer   
satisfies   