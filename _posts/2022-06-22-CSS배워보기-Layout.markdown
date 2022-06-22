# Layout

우리는 앞서 CSS 기본 사항, 스타일링 등에 대해 배워보았습니다. 이제는 뷰포트와 관련하여 컴포넌트, 상자를 올바른 장소에 배치하는 방법에 대해 알아보도록 하겠습니다.

## 일반적인 방법

페이지 레이아웃을 정하지 않았을 경우 HTML은 Cascading에 의해 계산신으로 배치된다.

```html
<p>오늘의 메뉴</p>

<ul>
  <li>치킨</li>
  <li>김밥</li>
  <li>삼겹살</li>
</ul>

<p>뭐먹지 ?!</p>
```

> 오늘의 메뉴

- 치킨
- 김밥
- 삼겹살
  > 뭐먹지 ?!

자 그럼 일반적인 흐름에서 벗어나도록 하는 방법에 대해 알아보도록 하겠습니다.

## display속성

### inline , block

`display`를 통해 상자를 `inline`,`block`으로 바꿀 수 있습니다.

#### display: inline;

`inline`속성은 상자의 크기를 내부 크기와 동일하게 맞춥니다. 그렇기에 나란하게 배치가 가능합니다.
![](https://velog.velcdn.com/images/kbm940526/post/18aeb746-a1fb-461d-8422-c401ee8074c0/image.png)
그렇기 때문에 `width`,`height`값을 설정할 수 없습니다. `span`,`strong` 등이 있습니다.

#### display: block;

`div`같이 한 라인을 전부 차지하는 태그를 말하며 나란히 배치되지 않는다. 또한, `width`,`height`값을 설정할 수 있다.

### display: flex;

`flex`는 `Flexible Box` 모듈의 약칭으로 단일 축을 기준으로 레이아웃을 반영합니다. 기본적으로 `flex`는 인라인 방향(가로)으로 정렬하고 높이를 나란히 맞춥니다. 이러한 축 방향은 `flex-direction`을 통해 설정이 가능합니다.

> flex 특징

- 행, 열로 표시 가능 (여기서 행,열이 축)
  `flex-direction`
- 기본적으로는 한줄이지만 여러 줄로도 변경 가능
  `flex-wrap`
- 정렬 기능
  `justify-content`,`align-items`
- 태그의 순서와 상관없이 재정렬 가능
  `reverse 속성주기`

[flex기본 1](https://studiomeal.com/archives/197)
[flex기본 2](https://web.dev/learn/css/flexbox/)

### display: grid;

`gird`는 `flex`와 비슷하지만 **다축 레이아웃을 제어하도록 설계**되었습니다.

> flex vs grid
> ![](https://velog.velcdn.com/images/kbm940526/post/9f9f2984-9a80-4caf-afb2-fea2774479b9/image.png)
> 출처 : [1분코딩 이미지](https://studiomeal.com/archives/533)

```css
.my-element {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 1rem;
}
```

- display로 grid를 선언합니다
- grid-template-columns를 통해 12개 컬럼을 반복 비율로 설정합니다.
- fr은 fraction으로 숫자 비율대로 크기를 나눕니다.
- gap : grid간 갭을 둡니다.

> grid-column-start
> grid-column-end
> grid-column
> grid-row-start
> grid-row-end
> grid-row

위 속성을 통해 특정 grid만 크기를 잡을 수 있습니다.

!codepen[web-dot-dev/embed/YzNwrwB?default-tab=css%2Cresult]

> 자세한 내용은
> [web.dev](https://web.dev/learn/css/grid/)
> [1분코딩](https://studiomeal.com/archives/533)

## float

![](https://velog.velcdn.com/images/kbm940526/post/cc00352f-cf47-42c6-a99f-b37ad36a2fc4/image.png)
예를 들어 신문과 같이 이미지 옆에 자연스럽게 글이 이어지게 하고 싶을 때 `float`속성을 줄 수 있다.

!codepen[web-dot-dev/embed/VwPaLMg?default-tab=css%2Cresult]

## li tag layout

!codepen[byungmin12/embed/RwQzrVe?default-tab=css%2Cresult]

!codepen[byungmin12/embed/RwQzrVe?default-tab=css%2Cresult]

첫번째와 두번째 중 뭐가 더 눈에 보이는 지를 확인해보자.

`li` tag가 많은 시 하나의 컬럼으로 하는 것보다 `column-count`속성을 주어 나누는 것이 보기 좋을 것이다.

## position

`position`속성은 일반적인 문서의 흐름과는 다르게 작동하는 방식입니다.
`position`에는 `relative`,`absolute`,`fixed`,`sticky`,`static`이 존재합니다.

### position : relative;

`relative`는 현재 위치를 기준으로 잡습니다.

```css
.test {
  position: relative;
  top: 100px;
}
```

현재 위치를 기준으로 잡기에 태그는 100px아래로 움직입니다.

### position : absolute;

`absolute`는 `relative`를 기준으로 잡습니다. 부모 태그에 `relative`속성이 있다면 해당 속성을 기준으로 잡습니다.

```css
.parent {
  position: relative;
  width: 100px;
  height: 100px;
}

.child {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 50px;
  height: 50px;
}
```

### position: fixed;

`fixed`는 `absolute`와 동일하게 작동하나 루트요소 `html`을 기준으로 잡습니다. `html`을 기준으로 잡기에 항상 그 위치에 고정됩니다.

### position: sticky;

`sticky`는 `fixed`와 `absolute`를 섞은 느낌입니다. `relative`속성이 존재하는 부모태그를 기준으로 하나 `sticky`속성이 있는 태그가 뷰포트에서 지나갈 때 `fixed`와 같은 화면에 고정됩니다.

!codepen[byungmin12/embed/jOZjWzW?default-tab=css%2Cresult]
