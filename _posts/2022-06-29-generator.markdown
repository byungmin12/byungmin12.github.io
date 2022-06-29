# Generator

일반적인 함수는 하나의 값을 반환합니다. 하지만 `제너레이터`를 사요하면 여러 개의 값을 필요에 따라 하나씩 리턴할 수 있습니다. 오늘은 이 이터레이터를 정리해보겠습니다.

## iteration interface

iteration interface는 `iterable`,`iterator`,`iterator result`로 구성됩니다.

### iterable

값을 반복할 수 있는 객체 쉽게 말해 `for..of`을 사용할 수 있는 객체
JS에서 객체가 `iterable`하기 위해서는 내부에 `[@@iterator]`프로퍼티가 존재해야합니다.
이 말은 Symbol.iterator가 반드시 구현되어 있어야합니다.

### iterator

`next`메서드를 가지고 있는 객체

### iterator result

boolean값만을 가지는 `done`과 모든 타입을 가질 수 있는 `value`를 프로퍼티로 갖는 객체

## generator

gererator는 iterable 인터페이스와 iterator 인터페이스를 동시에 갖는 generator 인스턴스를 갖는 함수이다. 이러한 제너레이터함수는 `for..of`, `스프레드` 등을 사용할 수 있습니다.

### 생성

```js
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}
let generator = generateSequence();
console.log(generator);
```

![](https://velog.velcdn.com/images/kbm940526/post/b5bf1520-3de6-4668-b923-9178270ca814/image.png)

제너레이터는 `function`뒤에 `*`를 붙여 생성한다. 이러한 함수는 제너레이터 함수라고 한다.

### yield

`yield`는 생성하다라는 뜻을 가진 단어로 generator에서 **값을 생성**하는 역할을 한다.
쉽게 말해 일반 함수의 `return`역할을 하는 것이다. 단, 제너레이터 함수는 `iterable`한 함수이므로 값을 여러개 생성해야하기에 return이 아닌 `yield`를 사용합니다.

> 물론 return 사용이 가능합니다. 단, 마지막 리턴 값에 value가 없어 next로 받아올 수 없습니다.

### next

```js
function* generateSequence() {
  yield 1;
  yield 2;
  yield 3;
}

let generator = generateSequence();

let one = generator.next();
```

마지막 줄과 같이
` generator.next();`를 통해 `yield`의 값을 가져옵니다.
제너레이터는 이터러블한 객체이기에 `for..of`을 사용할 수 있습니다.

```js
function* generateSequence() {
  yield 1;
  yield 2;
  yield 3;
}

let generator = generateSequence();

for (let value of generator) {
  alert(value);
}
```

### yield\*

`yield*`는 또 다른 이터러블 객체를 위임해서 사용하기 위한 키워드입니다.

```js
function* generateSequence() {
  yield* [1, 2, 3];
}
let generator = generateSequence();

for (let value of generator) {
  alert(value);
}
```

배열도 이터러블 객체죠 위 코드는 사실상

```js
function* generateSequence() {
  for (const el of [1, 2, 3]) {
    yield el;
  }
}
let generator = generateSequence();

for (let value of generator) {
  alert(value);
}
```

과 같은 것 입니다.

### yleid를 통한 데이터 교환

```js
function* generateSequence() {
  let result = yield "first console";
  console.log(result);
}
let generator = generateSequence();
let firstVal = generator.next().value;
console.log(firstVal);
generator.next("second console");
```

![](https://velog.velcdn.com/images/kbm940526/post/687f14a3-99ff-45d2-8425-5aaec987fc57/image.png)

`yield`를 통해 데이터 교환이 가능합니다.

### generator.throw

에러를 `yield`안으로 전달하려면 `generator.throw(err)`를 호출하면 됩니다.

```js
function* generateSequence() {
  try {
    let result = yield "first console";
    console.log("success");
  } catch (e) {
    alert(e);
  }
}
let generator = generateSequence();
let firstVal = generator.next().value;

generator.throw(new Error("failure"));
```
