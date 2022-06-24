# Functions

CSS에도 `Function`이 존재한다는 사실을 아시나요 ?  
`Function`이 존재하는지 몰랐어도 사실 우리는 사용하고 있었습니다. 그럼 이러한 `Function`들에 대해 배워나가 볼까요 ?

> 함수란?
> ![](https://velog.velcdn.com/images/kbm940526/post/63cd1137-1a50-4af8-a6a6-97e35bfd3c48/image.png)
> 프로그래밍에서 `함수(function)`란 특정 목적의 작업을 수행하기 위해 설계된 코드 집합입니다.

## :is() , :not()

가상 클래스를 선택하는 `:is`,`not()` 역시 css함수에 속합니다.

```css
.post :is(h1, h2, h3) {
  line-height: 1.2;
}
.post :not(div) {
  font-weight: 800;
}
```

## 사용자 지정 속성과 var()

사용자 지정 속성은 사용자가 정의하는 속성으로 문서 전반적으로 재사용할 값을 담습니다. 이때 전용 표기법(`--`로 시작해야함)에 맞춰 `:root`에 정의하며, `var()`을 통해 접근합니다.

```css
:root {
  --base-color: #ff00ff;
}

.my-element {
  background: var(--base-color);
}
```

## attr() , url()

```css
a::after {
  content: attr(href);
}
```

`attr()`함수는 요소의 속성 값을 문자열로 반환하는 함수입니다.

이 `attr()`함수는 `href`의 값을 가져와 `content`의 값으로 반환합니다.

```css
.my-element {
  background-image: url("/path/to/image.jpg");
}
```

`url()`함수는 문자열 url을 가져와 이미지, 글꼴 등 컨텐츠를 로드하는데 사용합니다.

## 색상 함수

`rgb()`,`rgba()`,`hsl()`,`hsla` 등이 이에 해당합니다.

자세한 내용은 [여기](https://web.dev/learn/css/color/)를 통해 알 수 있습니다.

## calc()

!codepen[web-dot-dev/embed/PopYema?default-tab=css%2Cresult]
색상과 URL만큼 많이 사용하는 css함수 `calc()`입니다.
`calc()`는 단위를 혼합하여 계산시켜 줍니다.

## min() , max()

```css
.my-element {
  width: min(20vw, 30rem);
  height: max(20vh, 20rem);
}
```

`min()`과 `max()`는 전달된 두개의 인자 중 큰,작은 값을 반환하는 css함수입니다.

## clamp()

`clamp()`는 최소 크기, 이상적 크기, 최대 크기를 반환하는 함수입니다.
기본적으로 이상적 크기를 갖지만 최소크기와 최대 크기까지 변경되게 해주는 함수입니다.

우리가 미디어커뤼로 나누어 작성하던 코드를

다음과 같이`clamp()`로 바꾸면

```css
h1 {
  font-size: clamp(2rem, 1rem + 3vw, 3rem);
}
```

표현할 수 있습니다. 이는 `1rem + 3vw`의 값이 `2rem`보다 작아지면 `2rem`값만 반환하며 `3rem`도 동일하게 작용합니다.

## 모양 관련 함수

`clip-path`와 같이 모양을 사용하여 상자를 `시각적`으로 다르게 보여지게 할 수 있습니다.

```css
.circle {
  clip-path: circle(50%);
}

.polygon {
  clip-path: polygon(
    0% 0%,
    100% 0%,
    100% 75%,
    75% 75%,
    75% 100%,
    50% 75%,
    0% 75%
  );
}
```

## transform

우리가 제일 많은 쓰는 함수 `transform`입니다.
`transform`은 축을 이동하거나 회전 혹스 확대 역할을 합니다.

### rotate()

!codepen[web-dot-dev/embed/MWJOWzP?default-tab=css%2Cresult]

위와 같이 요소를`transform: rotate()` 을 통해 회전시킬 수 있습니다.

### scale()

!codepen[web-dot-dev/embed/vYgWOoq?default-tab=css%2Cresult]

위와 같이 요소를 확대시킬 수 있습니다.

### translate()

!codepen[web-dot-dev/embed/RwKjWgP?default-tab=css%2Cresult]
해당 속성을 통해 축을 이동시킬 수 있습니다.

### skew()

!codepen[web-dot-dev/embed/JjEOYMq?default-tab=css%2Cresult]

`skew()`는 요소에 기울기를 추가합니다.

### perspective

!codepen[desandro/embed/bMqZmr?default-tab=css%2Cresult]

`perspective`를 통해 z값을 변경하여 3차원 효과를 만들 수 있습니다.
