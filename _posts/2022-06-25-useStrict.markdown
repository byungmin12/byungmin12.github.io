# use Strict mode

ECMAScript 5에서 소개된 엄격모드 `use stric`에 대해 알아보도록 하겠습니다.

`use stric`은 ECMAScript5가 출시되며 이전 하위 버전과 호완성 문제를 개선(?)하기 위해 새롭게 추가된 기능입니다. 이러한 엄격모드는 다음과 같은 행동을 합니다.

1. 기존에 통과되던 에러들을 잡아냅니다.
2. 자바스크립트 엔진의 최적화 작업을 어렵게 만드는 실수들을 바로잡습니다.
3. 문제를 일으키는 문법들을 금지합니다.

## 사용법 - 스크립트

엄격모드의 사용법은 매우 간단합니다. 스크립트 최상단에 `"use strict"`만 추가한다면 스크립트 전체가 영향을 받습니다.

```js
"use strict";

console.log("hello world");
```

> 주의 사항

- `use stric`은 반드시 최상단에 위치해야합니다.
  최상단에 위치하지 않으면 자바스크립트는 이를 읽지 못합니다.
- 취소할 수 없습니다.
  한번 적용하면 중간에 취소를 할 수 없습니다.

## 사용법 - 함수

엄격모드는 함수 내부에서도 사용이 가능합니다. 스크립트와 동일하게 함수 내부 최상단에 사용합니다.

```js
function exampleOne() {
  "use strict";
  console.log("hello world~");
}

function exampleTwo() {
  console.log("hello world~");
}
```

여기서 우리가 알아야할 것은 `exampleOne`는 엄격모드가 적용되고 `exampleTwo`는 적용되지 않는다는 것을 인지해야한다.

## 사용법 - 모듈

```js
function example() {
  console.log("hello world?");
}

export default example;
```

위 코드와 다른 점은 `use strict`가 없어지고 `export`가 추가되어 `모듈화`를 했다는 것이다.
이런 경우 자동으로 자바스크립트는 이를 엄격모드를 적용시킨다

# 결론

## use strict 엄격모드를 무조건 사용해야 할까?

이 질문에 대한 대답은 `그렇다`면서 `아니다`도 될 수 있다. 이유는 이제 자바스크립트는 **클래스**와 **모듈**을 통해 `use strict` 엄격모드를 자동으로 적용하기 때문이다.

위 질문에 `그렇다`라는 대답을 받기 위해서는 `**클래스**와 **모듈**를 사용해야만할까요?`라고 변경해야한다.
