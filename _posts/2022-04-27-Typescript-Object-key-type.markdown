# Typescript object key type

typescript를 사용하다보면

> Element implicitly has an 'any' type because expression of type 'string' can't be used to index type '{ test: string; }'.
> No index signature with a parameter of type 'string' was found on type '{ test: string; }'.ts(7053)

이러한 에러를 만나는 경우가 있을 것이다.
아마 그런 코드는 대부분

```js
const test = { test: "test" };
let j = "test";
console.log(test[j]);
```

이와같은 형태로 객체에 접근하려했기 때문이다.

그럼 여기서 왜? Typescript는 컴퍼일에러를 발생시키는 것일까?

## why?

typescript의 string type은 두가지 형태로 나뉜다.

일반정인 **String**타입과 **String Literal** 타입니다.

> Literal
> 사전적 의미 =>
> 정확한
> 융통성 없는
> 사람 융통성 없는
> 문자 그대로 정확한
> 문자의
> 문자상의
> 문자대로의
> 머리가 융통성 없는

말 그대로 **융퉁성이 없는 문자형 타입**인 것이다.

javascript를 사용하다보면 const가 어떤 기능이 있는지 알것이다.

>

```js
const test = "test";
test = "other test";
//TS2588: Cannot assign to 'test' because it is a constant.
```

const는 let,var과는 다르게 블록 범위 안에서만 사용이 가능하며 **재할당이 안되는 특징**이 있다. 여기서 주목해야할 것은 재할당이 안된다는 것이다.

재할당이 안되다보니 test라는 변수는 사실상 아래와 같은 형태를 띄고있는 것이다.

```ts
let test: "test" = "test";
```

## use

그럼 어떻게 해야 타입스크립트에서 객체키에 string을 넣을 수 있는 것일까?

답은 간단하다. String Literal을 사용해주면 된다.

```ts
const test = { test: "test" };
const j = "test";
console.log(test[j]);
console.log(test["test"]);
```

모두 사용이 가능하다.

### loop

반복문에서는 과연 사용이 가능할까?

```ts
const test = {
  a: "a",
  b: "b",
  c: "c",
};
for (const key in test) {
  test[key];
}
```

위와 같이 사용하다보면 다시

> TS7053: Element implicitly has an 'any' type because expression of type 'string' can't be used to index type '{ a: string; b: string; c: string; }'.
> No index signature with a parameter of type 'string' was found on type '{ a: string; b: string; c: string; }'.

컴파일 에러가 우리를 반길 것이다.
const key 인데 왜 에러가 나는 것일까?

```ts
// 1. Type
const test1 = "test";

// 2. const key type
for (const key in test) {
  test[key];
}
```

1번과 2번의 타입을 비교해보자
1번같은 경우는 type이 "test"로 들어가있을 것이다.
2번같은 경우는 typedl string으로 들어가있을 것이다.

자 우리는 위에서 본 것과 같이 하나는 String Literal, 다른 하나는string인 것을 알 수 있을 것이다.

그럼 여기서 어떻게 접근해야하는가 ?

### 해결

객체의 타입을 설정해줄때 , 키 타입도 설정해주면 되는 것이다.

```ts
interface ITest {
  [key: string]: string;
  a: string;
  b: string;
  c: string;
}

const test: ITest = { a: 1, b: 2, n: 3 };

for (const key in test) {
  test[key];
}
```

만약 key나 value값이 바뀐다면 그에 맞는 설정이 필요할 것이다.
