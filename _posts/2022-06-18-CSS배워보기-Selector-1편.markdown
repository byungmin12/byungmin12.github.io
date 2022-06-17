# Selector - 1편

> 해당글은 [web.dev](https://web.dev/learn/css/selectors/)를 정리한 글입니다.

HTML Element 특정 요소에 CSS를 적용하기 위해서는 그 요소를 선택할 수 있어야한다. 해당 포스팅에서는 이러한 선택자 Selector에 대해 알아보려한다. 단 1편 ,2 편으로 나누어 2편에서는 CSS pseudo selector에 대해 알아볼 것이다.

## CSS 규칙

Selector을 이해하려면 당연히 CSS규칙을 알아야 할 것이다.

![](https://velog.velcdn.com/images/kbm940526/post/21e57d19-dc89-43b6-959b-6ed7e87ef414/image.png)

CSS규칙은

- Selector : 태그나 클래스 네임 등을 선택하는 부분
- Delaration : Property와 Value, 즉 키와 쌍으로 이루어진 부분
- Property : 특성 키값의 부분
- Value : 키에 맞는 값 부분

으로 이루어진다.

## 단순 선택자

**단순 선택자는 HTML Element와 ClassName, ID 및 기타 속성을 대상**으로 선택하는 선택자입니다.

## 범용 선택자

와일드카드라고도 하는 범용 선택자는 모든 요소를 선택하는 선택자입니다.

```css
* {
  color: hotpink;
}
```

## 유형 선택자

HTML Element를 직접 선택하는 요소입니다.

```css
selection {
  padding: 2em;
}
```

> 확인!
> 유형 선택자와 단순 선택자의 차이
> 유형 선택자는 **HTML Element를 직접 선택**하는 것이고 단순 선택자는 **HTML Element + 속성**을 선택하는 것입니다.

위와 같이 selection 태그에 속성값을 주면 모든 selection은 해당 css규칙이 적용됩니다.

## 클래스 선택자

HTML Element에 주어진 Class Name를 선택합니다.

```html
<div class="post-example">hello world!</div>
<div class="post-example">hello my velog!</div>
```

```css
.post-example {
  color: red;
}
```

이렇게 하면 ` post-example`이라는 class name갖는 모든 태그들에게 `color: red;`라는 속성을 줍니다.

여기서 `.`은 class name을 선택하는 css에만 존재하는 선택자입니다. 단 주의점으로 class name 및 id는 숫자로 시작할 수 없습니다..

## ID 선택자

ID 속성이 있는 HTML Element에 속성을 부여합니다.

```html
<div id="rad">hello world!</div>
```

```css
#rad {
  border: 1px solid blue;
}
```

ID의 선택자는 `#`입니다.

> Class와 ID의 차이
> Class는 여러개의 중복을 갖고 그에 맞는 CSS규칙을 줄 수 있습니다.
> ID는 HTML안에서 고유하게 존재해야함으로 단 하나의 태그가 하나의 값을 갖을 수 있습니다.

## 속성 선택자

HTML 속성이 있거나 HTML 속성에 대한 특정 값이 있는 요소를 찾는 선택자입니다. 이때 선택자는 `대괄호[]`를 사용합니다.

```html
<div data-type="primary"></div>
```

```css
[data-type="primary"] {
  color: red;
}
```

data-type이 primary인 태그들에게 속성을 제공합니다.

```html
<div data-type="primary"></div>
<div data-type="secondary"></div>
```

```css
[data-type] {
  color: red;
}
```

첫번째 예시와 지금 나온 예시의 차이점이 무엇일까요 ?

지금 나온 예시는 data-type이 있는 모든 요소에 `color: red;` 속성을 제공합니다.

!codepen[byungmin12/embed/WNMWrww?default-tab=html%2Cresult]

위 에디터를 통해 여러 속성 선택자를 확인하자

## 그룹 선택자

선택자는 하나의 요소만을 선택할 필요가 없다 여러 선택자를 한번에 `,`로 구분하여 선택하다.

```css
strong,
em,
.my-class,
[lang] {
  color: red;
}
```

`strong`,`em`, `class name이 my-class` , `lang 속성` 에 `color: red;`를 적용한다.
