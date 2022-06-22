# Event Loop

자바스크립트는 single thread기반의 언어입니다. 하나의 일을 처리한 뒤 다른 일을 처리할 수 있는 언어이죠. 그치만 우리가 자바스크립트를 사용하여 api요청 등을 보냈을 때, 그렇게 작동하지 않는다는 것을 우리는 알고있습니다. 이는 event loop때문입니다.

해당 글에서는 thread가 무엇인지. event loop는 무엇인지 알아보도록 하겠습니다.

## Thread란 ?

`Thread`란 쉽게 말해 프로세스의 실행 가능한 가장 작은 단위를 말합니다. 즉 돌아가고 있는 프로그램이 처리할 수 있는 일의 가장 작은 단위를 말합니다. 이러한 프로그램이 갖는 스레드의 갯수에 따라 `single thread`와 `multi thread`로 나뉩니다.

### single thread

![](https://velog.velcdn.com/images/kbm940526/post/ce96bb98-538c-4c72-adb7-f57bf738db68/image.png)

- 하나의 프로세스에서 하나의 스레드를 갖기에 작업을 순차적으로 실행
- 여러 개의 작업이 순차적으로 발생 시 작업이 빠르게 이루어지지않음

### Multi THread

![](https://velog.velcdn.com/images/kbm940526/post/bb7022d5-0323-4d20-a8e7-d0c4d4008988/image.png)

- 하나의 프로세스 내에 여러 개의 스레드
- 스레드는 각 각 다른 작업을 할당 받기에 병렬적으로 여러 작업을 동시에 수행
- 프로세스 내에서 Stack만 따로 할당 받고 Code,Data,Heap은 공유
- 한 스레드가 자원을 변경하면 다른 스레드도 그 결과를 즉시 받음
- 여러개의 스레드가 동일한 메모리 주소를 활용하여 작업을 수행하기에 메모리 사용이 효율적

## JavaScript is a single-threaded language?

위에서 던진 질문의 대답은 `Yes`이면서 `No`입니다. 이는 event loop입니다. .

### JavaScript is a single-threaded language

`js`는 `callstack`이란 FILO(선입후출)인 단일 호출 스택을 가지고 있습니다.

> 호출스택
> 프로그램에서 우리가 어디에 있는지 기록하는 데이터 구조

```js
function test(x, y) {
  return x * y;
}

function testPrint(x) {
  const a = test(x, 4);
  console.log(a);
}
testPrint(5);
```

위와 같이 코드를 작성했을 때 `Callstack`에서 흐름을 확인해봅시다

들어온 순서대로 처리하기에 `single thread`언어입니다.

그럼 이때 의문점이 생길 것입니다.
`fetch`, `setTimeout`과 같은 비동기 요청을 보냈을 때 우리는 요청을 보내고 다른 작업을 할 수 있기 때문입니다.

### JavaScript is not a single-threaded language

이 대답에는 맞으면서 아니라고 할 수 있습니다. 그 이유는 `비동기`때문입니다.

## Event Loop

위의 질문에 대답을 위해 `Event Loop`에 대해 알아보겠습니다.

### 구조

우선 이벤트 루프는 아래 그림과 같은 구조를 갖습니다.
![](https://velog.velcdn.com/images/kbm940526/post/27b6d681-d3e7-4185-b30a-c761ed4959a8/image.png)

- Stack (call stack) : 프로그램에서 우리가 어디에 있는지 기록하는 데이터 구조
- Heap : 객체, 변수 등을 저장하는 메모리를 지칭하는 용어
- Queue : 처리할 메시지를 담아두는 리스트, 대기열

### 흐름

![](https://velog.velcdn.com/images/kbm940526/post/938045ce-bb29-4ba3-9a02-8302d563cb50/image.png)

1. **callstack에 web APis 관련 비동기 함수**가 들어오면 web APis로 함수를 던져줍니다.
2. 던져진 함수는 작업이 수행되어지면 **Queue로 이동**을 하게됩니다.
3. Queue에 이동된 데이터는 **들어온 순서에 맞게 다시 Callstack**으로 이동합니다.
4. 이후 **Callstack에서 리턴**을하게 됩니다.
