# css animation vs Js animation

우리는 웹 사이트에 애니메이션을 적용할 때 `CSS`의 `tansition`이나 `animation`을 사용하거나 `JS`의 `setInterval, setTimeOut`이나 `requestAnimationFrame, cancelAnimationFrame`을 사용합니다.

이 두개가 무슨 차이가 있는지에 대해 알아도보록 하겠습니다.

## CSS Animation

CSS로 애니메이션을 처리하게되면 엘레멘트를 다시 그리는 작업을 하기에 성능 개성에 효과적이지가 않다. 단, css는 웹의 요소 중 하나이기에 어떤 환경에서도 애니메이션 구현이 가능하다. 또한 미디어 쿼리를 통해 반응형으로 구현이 가능하다.

## JS Animation

CSS보다 복잡하고 어려운 애니메이션 구현이 가능하다. `requestAnimationFrame, cancelAnimationFrame` 이전에는 `setInterval, setTimeOut` 사용했기에 성능 문제가 존재했지만 현재는 이를 해결했기에 좋은 성능을 낸다. 또한 호환성에 구애받지않는다. 마지막으로 GPU를 통한 하드웨어 가속을 제어할 수있다.
