# Logical Properties

CSS에서 가장 많이 쓰이는 텍스트의 흐름은 좌에서 우로 , 박스의 흐름은 위에서 아래로 이루어진다. 그렇기에 CSS 흐름은 항상 위, 왼 아래, 오른쪽으로 이루어진다. 하지만 텍스트나 박스의 흐름은 다를 수 있어야하며 이것은 CSS로 지정해줘야 flexable interface를 구성할 수 있다.

## Text flow

텍스트의 흐름은 `writing-mode`를 통해 바꿀 수 있다.

!codepen[web-dot-dev/embed/YzNZGam?default-tab=css%2Cresult]

### syntax

>

```css
/* Keyword values */
writing-mode: horizontal-tb;
writing-mode: vertical-rl;
writing-mode: vertical-lr;
>
/* Global values */
writing-mode: inherit;
writing-mode: initial;
writing-mode: revert;
writing-mode: revert-layer;
writing-mode: unset;
```

[mdn참조](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode#values)

>

## Flow relative

텍스트의 흐름을 바꾸었으면 `margin`,`padding`등 흐름도 바꿀 수 있어야할 것이다.
!codepen[byungmin12/embed/xxYoNWm?default-tab=css%2Cresult]

예시 1번과 2번의 차이를 보면 알 수 있다. 2번의 경우 박스의 흐름이 바뀌었기에 `margin` 위치 텍스트의 상단으로 바뀌었고 1번의 경우 `margin`의 값을 여전히 상단을 보고 있다.

## Sizing

`width`와 `height` 또한 텍스트의 흐름에 맞춰 흐름이 바뀌어야 할 것이다.
예를 들어

```css
.my-element {
  max-width: 150px;
  max-height: 100px;
}
```

속성을 준다면 최대 높이,너비가 150,100px로 우리가 흔히 아는 `width=가로`, `height=세로`가 될 것이다.
하지만

```css
.my-element {
  max-inline-size: 150px;
  max-block-size: 100px;
}
```

위와 같이 속성을 준다면 `writing-mode` 속성에 맞춰 `width`,`height`가 정해질 것이다.

## padding, margin, inset, border

이 `padding`, `margin`, `inset` 속성 또한 `writing-mode`에 따라 속성을 줄 수 있다.

```css
.my-element {
  padding-block-start: 2em;
  padding-block-end: 2em;
  margin-inline-start: 2em;
  position: relative;
  inset-block-start: 0.2em;
}
.my-element-border {
  border-block-end: 1px solid red;
  border-inline-end: 1px solid red;
  border-end-end-radius: 1em;
}
```

> inset ?
> The inset CSS property is a shorthand that corresponds to the top, right, bottom, and/or left properties. It has the same multi-value syntax of the margin shorthand.
> 공부 필요

## 사용

### 차트 사용

!codepen[web-dot-dev/embed/zYNZNgE?default-tab=css%2Cresult]
