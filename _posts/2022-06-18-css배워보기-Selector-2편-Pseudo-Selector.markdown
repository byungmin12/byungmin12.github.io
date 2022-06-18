# CSS배워보기 - Selector - 2편 - Pseudo Selector

## Pseudo Selector

HTML Element는 다양한 상태(마우스 포인터로 가리키는 등)에 놓였을 때 pseudo selector를 사용하여 CSS 규칙을 적용한다.

```css
/* a tag에 마우스 포인터가 올려져있었을 때 */
a:hover {
  outline: 1px dotted green;
}

/* 모든 짝수 p tag에 다른 배경 설정 */
p:nth-child(even) {
  background: floralwhite;
}
```

많은 Pseudo Selector는 [여기](https://web.dev/learn/css/pseudo-classes/)에서 확인하자

## Pseudo elements

Pseudo element는 선택한 요소의 일부분에만 스타일을 입히는 규칙이다.

```css
/* The first line of every <p> element. */
p::first-line {
  color: blue;
  text-transform: uppercase;
}
```

> 확인 !
> `pseudo selector`는 요소의 `특정 상태`에 스타일을 적용하며 `:`를 하나만 사용
> `pseudo element`는 요소의 일부분에 스타일을 적용하며 `::`를 두개 사용

많은 Pseudo elements는 [여기](https://web.dev/learn/css/pseudo-elements/)에서 확인하자

## 복합 셀렉터

html 계층 구조 안에서 부모요소와 자식요소간의 관계를 파악하고 상속을 통해 CSS 속성 적용이 어떻게 이루어지는지 학습합니다.

### Combinators

상속 구조 관계에서 원하는 요소를 선택하기 위해 결합하는 것을 말합니다.

#### Descendant Selector - 후손 선택자

```css
p strong {
  color: blue;
}
```

` ` 공백을 활용하여 P tag 안 strong tag에 속성을 줍니다. 단 strong 태그는 p 태그 안 다른 요소의 자식이어도 규칙이 적용됩니다.

#### Child Selector - 자식 선택자

```css
p > strong {
  color: blue;
}
```

` >` 활용하여 P 태그의 직접적인 자식인 strong 태그를 선택합니다.

> Descendant selector vs Child Selector
> 후손 선택자는 부모안에 있는 모든 태그에게 규칙을 적용합니다.
> 자식 선택자는 부모의 직접적인 자식에게만 규칙을 적용합니다.

#### Adjacent Sibling Selector - 인접 형제 선택자

```css
p + strong {
  color: blue;
}
```

`+`를 활용하여 P태그와 바로 인접한 형제 태그에게 속성을 부여한다. 단, p와 strong은 같은 부모 요소를 가지고 있어야 한다.

#### General Sibling Selector - 일반 형제 선택자

```css
p ~ strong {
  color: blue;
}
```

`~`를 활용하여 p태그와 형제인 모든 strong 태그를 선택하여 속성을 부여한다.

> Adjacent Sibling Selector vs General Sibling Selector
> Adjacent Sibling Selector 는 인접한 형제 태그만
> General Sibling Selector는 모든 형제 태그에 속성 부여

#### Compound selector

```css
section.awesome {
  border: 1px solid hotpink;
}
```

section이면서 classname이 awesome인 태그에만 속성을 부여한다 .
