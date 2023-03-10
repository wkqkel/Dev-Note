# 2. TypeScript

π [**TypeScript κ³΅μλ¬Έμ**](https://www.typescriptlang.org/ko/)
β νκ΅­μ΄λ₯Ό μ λλ‘ μ§μνμ§ μμ§λ§, λͺλͺ λ¬Έμλ₯Ό νκ΅­μ΄λ‘ μ½μ μ μκΈ΄ νλ€.

- [TypeScript for the New Programmer](https://www.typescriptlang.org/ko/docs/handbook/typescript-from-scratch.html)
- [TypeScript for JavaScript Programmers](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html)

## `Interface(μΈν°νμ΄μ€) vs Type(νμλ³μΉ­)`

[νμ λ³μΉ­κ³Ό μΈν°νμ΄μ€μ μ°¨μ΄μ ](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%ED%83%80%EC%9E%85-%EB%B3%84%EC%B9%AD%EA%B3%BC-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

- λλ€ ν΄λΉ ν€μλλ₯Ό μ¬μ©νμ¬ λ°λ³΅λλ νμμ μΈν°νμ΄μ€ λλ νμμΌλ‘ μ§μ ν΄ μ¬μ¬μ©κ°λ₯νκ² ν©λλ€.
- μΈν°νμ΄μ€λ extendsν€μλ νμμ & μ°μ°μλ₯Ό μ¬μ©ν΄ νμ₯νλ€.
- μΈν°νμ΄μ€λ λμΌν μ΄λ¦μ ν΅ν΄ μ¬μ μν¨μΌλ‘μ¨ μ μΈμ  νμ₯μ΄ κ°λ₯νμ§λ§ typeλ μμ±λ λ€μλ λ¬λΌμ§ μ μλ€.

```js
interface Itest1 {
  a: string;
}

interface Itest1 {
  b: string;
}

const test1: Itest1 = {
  a: "a",
  b: "b",
};
```

- computed valueλ typeμ μ¬μ©κ°λ₯νμ§λ§, interfaceλ λΆκ°

```js
type keyType = 'a' | 'b';

type type1 = {
  [key in keyType]: string
}

const typeA: type1 = {
  a: 'a',
  b: 'b',
}

interface interface1 {
  [key in keyType]: string  // μλ¬
}
```

## `μ λμ¨κ³Ό μΈν°μΉμνμ`

- μ λμ¨ | , μΈν°μΉμ &
- μ λμ¨μ ν©μ§ν© μμ±, μΈν°μΉμμ κ΅μ§ν© μμ±(κ΅μ§ν©μ΄ λ μμ μ§ν©)
- ν©μ§ν©μ λ§€κ°λ³μλ₯Ό μ νν  μ μκ³ , κ΅μ§ν©μ νμμ κ°λ¨νκ² νμ₯ν  μ μμ.

```js
type Category = "food" | "toy" | "bag";

function fetchProducts({ category }: { category: Category }) {
  console.log(`Fetch ${category}`);
}
```

```js
type Measure = { radius: number };
type Style = { color: string };

// typed { radius: number; color: string }
type Circle = Measure & Style;
```

## `μ΅μλ νλΌλ―Έν°`

- νλΌλ―Έν°κ° μ¬μλμκ³  μμ¬μλμμλ ?(μ΅μλ νλΌλ―Έν°) μ¬μ©
- λλ =μ μ¬μ©ν΄ κΈ°λ³Έκ° μ€μ ν  μ μλ€.

```js
function greeting({ name, age }: { name: string, age?: number } = { name: "hong" }): string {
  return age ? `${name} (${age})` : name;
}
```

## `νν νμ`

- μμ£Ό κΉκΉνκ² μ‘μμ£Όλ €ν  λ μ¬μ©, κ°―μλ μ§μΌμΌν¨.

```js
let arr: [string, number];
```

## `Generics μ λ€λ¦­`

- μ λ€λ¦­μ νμμ λ§μΉ ν¨μμ νλΌλ―Έν° κ°λμΌλ‘ λ°μ, λ€μν νμμΌλ‘ μ¬μ¬μ©κ°λ₯νκ² ν΄μ£Όλ λ¬Έλ²
- κΊ½μ<>λ₯Ό μ΄μ©ν΄ μ¬μ©.

```js
function identity<Type>(arg: Type): Type {
  return arg;
}
```

## Utility μΆν μΆκ° κ³΅λΆ νμ\_ μμ£Ό μ°μΌλ§ν κ² λ¨Όμ !

- [utility λ¬Έμ](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- μ λ€λ¦­νκ³  μ΅μν΄μ§λ©΄ λ λ³΄κΈ°

### `Awaited<Type>`

- νλ‘λ―Έμ€μ λ΄κΈ΄ νμμΌλ‘ μ§μ νκ³  μΆμ λ μ¬μ©

```js
type A = Awaited<Promise<string>>; // type A = string
```

### `Record<Keys, Type>`

- νλΌλ―Έν°λ‘ λ°λ Keysκ° keyκ° λκ³ , Typeμ΄ valueκ° λλ κ°μ²΄ νμμ μ§μ ν  λ μ¬μ©.

```js
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

### `Pick<Type, Keys>`

- FκΈ°μ‘΄ νμμμ νμν νμλ§ μΆμΆν΄μ μλ‘μ΄ νμ

```js
type User = {
  age: number,
  gender: string,
  country: string,
  city: string,
};
// type Demographic = { age: number: gender: string; };
type Demographic = Pick<User, "age" | "gender">;
```

### `Omit<Type, Keys>`

- κΈ°μ‘΄ νμμμ νΉμ  νμμ λΊ μλ‘μ΄ νμ

```js
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

### `ReturnType<T>`

- ν¨μμ λ°ν νμμ λ³΅μ νλ λμ  μ¬μ©

```js
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

### `Partial<Type>`

- νΉμ  νμμ λΆλΆ μ§ν©μ λ§μ‘±νλ νμμ μ μ
- λͺ¨νΌ νλ‘νΌν°κ° μ΅μλλ‘ λ€μ΄κ° κ²κ³Ό κ°μ ν¨κ³Ό

```js
interface Address {
  email: string;
  address: string;
}

type MyEmail = Partial<Address>;
const me: MyEmail = {}; // κ°λ₯
const you: MyEmail = { email: "noh5524@gmail.com" }; // κ°λ₯
const all: MyEmail = { email: "noh5524@gmail.com", address: "secho" }; // κ°λ₯
```

## `λ μ’μ νμμ€ν¬λ¦½νΈ νλ‘κ·Έλλ¨Έλ‘ λ§λλ 11κ°μ§ ν`

[μλ£ λ§ν¬](https://velog.io/@lky5697/11-tips-that-help-you-become-a-better-typescript-programmer)

### `μ΅μλ νλ λμ  κ΅¬λΆλ μ λμ¨ μ¬μ©`

before

```js
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

### `νμλ¨μΈ(as)λ₯Ό νΌνκΈ° μν νμλͺμ (is) μ¬μ©`

```js
type Circle = { kind: "circle", radius: number };
type Rect = { kind: "rect", width: number, height: number };
type Shape = Circle | Rect;

function isCircle(shape: Shape) {
  return shape.kind === "circle";
}

function isRect(shape: Shape) {
  return shape.kind === "rect";
}

const myShapes: Shape[] = getShapes();

// νμμ€ν¬λ¦½νΈκ° νν°λ§ λ κ²μ λͺ¨λ₯΄κΈ° λλ¬Έμ μλ¬κ° λ°μν©λλ€.
// νμ μ’νκΈ°
const circles: Circle[] = myShapes.filter(isCircle);

// λ€μκ³Ό κ°μ λ¨μΈμ μΆκ°νκ³  μΆμ μ μμ΅λλ€.
// const circles = myShapes.filter(isCircle) as Circle[];
```

λ³΄λ€ μ°μν ν΄κ²°μ±μ isCircleκ³Ό isRectλ₯Ό νμ λͺμ λ₯Ό λ°ννλλ‘ λ³κ²½νμ¬

filter νΈμΆ ν νμμ€ν¬λ¦½νΈκ° νμμ μ’ν μ μλλ‘ λμμ£Όλ κ²

```js
function isCircle(shape: Shape): shape is Circle {
    return shape.kind === 'circle';
}

function isRect(shape: Shape): shape is Rect {
    return shape.kind === 'rect';
}

...
// μ΄μ  Circle[] νμμ μ¬λ°λ₯΄κ² μ μΆν©λλ€.
const circles = myShapes.filter(isCircle);
```

### `as const`

as const λ κ°μ₯ κ΅¬μ²΄μ μΈ νμμΌλ‘ λ²μλ₯Ό μ’ν.

```
let a = [1, 2]; // typed: number[]
let b = [1, 2] as const; // typed: [1, 2]

// typed { kind: 'circle; radius: number }
let circle = { kind: 'circle' as const, radius: 1.0 };
// circleμ΄ const ν€μλλ₯Ό μ¬μ©ν΄ μ΄κΈ°ν λμ§ μμλ€λ©΄
// λ€μμ΄ λμνμ§ μμ΅λλ€.
let shape: { kind: 'circle' | 'rect' } = circle;
```

## μ©μ΄ μ λ¦¬

`REPL`

- "REPL"μ΄λ Read-Eval-Print-Loopμ μ½μλ‘ μ»΄νμΌ κ³Όμ  μμ΄ μ¦μμμ μ½λλ₯Ό μλ ₯ν΄ κ²°κ³Όλ₯Ό λ°λ‘ μ μ μλ λ°©μμ λ§ν¨.
- κ°λ° μμ μ½λλ₯Ό μ¦μ νμ€νΈν¨μΌλ‘μ¨ λλ²κΉμ ν  μ μμ.
- npx ts-node λ₯Ό μ¬μ©νμ¬ replνκ²½μ μ¬μ©ν  μ μμ.

`TypeScript`

- νμμ κ°μ§ μλ°μ€ν¬λ¦½νΈλ‘, μλμμ±κ³Ό μ€μκ° μ€λ₯κ²μ¬λ₯Ό μ κ³΅ν΄μ€.

`νμμΆλ‘ `

- νμμ μΌμΌν μλ ₯ μν΄λ νμμ μΆλ‘ ν΄μ€. μ μ ν νμ©
