![](https://velog.velcdn.com/images/kbm940526/post/918882a7-00a6-4623-b2b8-fe3db7d71650/image.png)

위 [책](http://www.yes24.com/Product/Viewer/Preview/5692122)을 읽고 작성하였습니다.

# 스코프 관리

## 스코프

스코프란 **참조 대상 식별자를 찾아내기 위한 규칙**입니다.
참조 대상 식별자란 말이 쉽게 말해 변수라고 생각하면 됩니다.

```js
const here = "kitchen";

function whereIsMyCheese() {
  console.log(here);
}
whereIsMyCheese();
```

자 여기서 함수 `whereIsMyCheese` 안에는 `here`이라는 변수가 존재하지 않습니다. 그치만 위 코드를 실행한다면 콘솔에는 `kitchen`이라는 값이 출력될 것입니다. 여기서 `here`이 `whereIsMyCheese`의 **참조 대상 식별자**입니다.

함수 `whereIsMyCheese`는 here이라는 값을 찾기 위해 **지역 스코프**를 확인할 것입니다. 그리고 지역 스코프에 이것이 없으면 상위 지역 즉 `whereIsMyCheese`의 **전역 스코프를 확인**하여 `here`을 찾아낼 것입니다.

![](https://velog.velcdn.com/images/kbm940526/post/922a2b4e-16d8-4a3a-a054-fce80d918e25/image.png)
이렇게 값을 찾아가는 일련의 과정을 `스코프 체이닝`이라하며 이러한 관계는 `스코프 체인`이라고 합니다.

## 스코프 관리

그럼 이러한 스코프를 어떻게 관리해야 자바스크립트의 성능를 최적화할 수 있을까요 ?

### 적절한 위치에 값 선언하기

사실 가장 좋은 방법은 적절한 위치에 변수를 선언하는 것입니다.

```js
function rusianDoll() {
  const here = "Doll!";

  function rusianDollOne() {
    function rusianDollTwo() {
      function rusianDollThree() {
        console.log(here);
      }
    }
  }
}
rusianDoll();
```

극단적인 이 코드를 한번 봐봅시다.
이 코드에서 here은 맨 처음 `rusianDoll` 안에서 선언되었지만 사용은 `rusianDollThree`에서 이루어졌습니다.

해당 함수는 `here`의 값을 찾기 위해 `rusianDollThree => rusianDollTwo => rusianDollOne`까지 확인을 한 뒤에야 `here`값을 가지고 올 것입니다. 이러한 과정이 쌓이고 쌓이다보면 성능 저하로 이루어지겠죠.

```js
function rusianDoll() {
  function rusianDollOne() {
    function rusianDollTwo() {
      function rusianDollThree() {
        const here = "Doll!";
        console.log(here);
      }
    }
  }
}
rusianDoll();
```

위와 같이 here을 적절한 위치로 수정하여 체이닝 과정을 줄입시다.

### 중복값 처리

```js
function iniUI() {
  let bd = document.body,
    links = document.getElementByTagName("a"),
    i = 0,
    len = links.length;
  while (i < len) {
    update(links[i++]);
  }

  document.getElementById("go-btn").onClick = function () {
    doSomeThing();
  };
  bd.className = "active";
}
```

사실 이 유형은 제가 가장 많이 하는 실수 중 하나입니다.

여러분들은 이 코드를 보며 문제점을 파악하셨나요 ??

정답은 바로 `document`의 중복 사용입니다.

자 `document`를 찾는 과정을 설명하면 빠를 것입니다. `iniUI`함수를 실행하면 `document`를 찾기위해 `iniUI`의 상위 지역 스코프를 확인할 것입니다. 그렇게 확인을 반복하다가 마지막 전역스코프를 확인하고 거기서 `document`를 가져올 것입니다.

그 과정을 `bd`,`links`,`onClick할당` 총 세번 이루어집니다. 이것은 간단한 로직이라 그렇지만 엄청 복잡하고 긴 함수라면 더 많은 스코프체이닝이 이루어질 것입니다.

이러한 문제점을 피하기 위해 우리는 `document`를 찾는 과정을 한번만 하게 해줘야 합니다.

```js
function iniUI() {
  let doc = document,
    bd = doc.body,
    links = doc.getElementByTagName("a"),
    i = 0,
    len = links.length;
  while (i < len) {
    update(links[i++]);
  }

  doc.getElementById("go-btn").onClick = function () {
    doSomeThing();
  };
  bd.className = "active";
}
```

그렇게 코드를 변경한다면 단 한번의 스코프체이닝만 이루어질 것입니다.

### try..catch를 활용한 스코프 체인 확장

`try..catch`를 활용하면 스코프 체인을 확장한다면 성능 하락을 최소화할 수 있습니다.

```js
try {
  error();
} catch (ex) {
  handleError(ex); //에러처리 함수에 에러처리를 위임합니다.
}
```

여기서 `handleError`는 에러가 났을 때 생성되는 예외 객체를 넘겨받아 적절한 방법으로 처리합니다. catch절에는 실행문 하나만 있고 지역 변수가 없으므로 임시 스코프 체인 확장이 성능에 영향을 주지 않습니다.

또한 catch문은 스코프에 영향을 주지 않습니다.

```js
let sports = "a";
try {
  let sports = "basketball";
  abc = error;
  console.log("try : ", sports);
} catch (e) {
  sports = "football";
  console.log("catch : ", sports);
}

console.log("밖 : ", sports);
```

위 코드를 실행하면 `console.log("catch : ", sports);`와 `console.log("밖 : ", sports);`의 결과가 `football`이라는 것을 알 수 있습니다. 이는 스코프에 영향을 받지 않는다는 것 또한 알 수 있습니다.

하지만 catch를 마구 사용하면 안됩니다. `try-catch`문을** 에러가 있을지도 모를 때 쓰는 것**이지 에러 처리를 위한 것이 아닙니다. 에러가 자주 발생할 것이라고 생각한다면 코드를 수정하는 것이 맞습니다.
