# CSS Sizing Units

인터페이스의 질을 높이기 위해서는 적절한 단위 설정이 필요합니다. 해당 포스트에서는 이에 대해 알아보도록 하겠습니다.

## Numbers

!codepen[byungmin12/embed/dydEJym?default-tab=css%2Cresult]
Numbers 값는 `opacity`,`line-height`,`rgb` 등 에서 사용되어지며 단위는 사용되지 않는다.

> Number unit이 사용되는 경우

- `filter` 에 사용 ( %를 넣을 수 있는 경우 )
- `opacity: 0.5;`에 사용
- `color: rgb(255,255,255)`에 사용
- `transform: scale(1,2)`에 사용

## Percentage

percentage가 무엇인지 보다 percentage가 어떻게 작동하는 지에 대해 알아보겠습니다.

```css
div {
  width: 300px;
  height: 100px;
}

div p {
  width: 50%;
}
```

`p`의 부모로 `div`가 온다면 `p`태그의 width는 몇일까요 ?

부모의 `50%`, `150px`이겠죠

자 그럼

```css
div {
  width: 300px;
  height: 100px;
}

div p {
  margin-top: 50%;
  padding-left: 50%;
}
```

여기서 `margin-top`, `padding-left`에 대한 값을 얼마일까요 ?

`margin`과 `padding`은 모두 `width`의 영향을 받아 `150px`을 갖는다.

그럼 `transform`은 어떨까 ?

```css
div {
  width: 300px;
  height: 100px;
}

div p {
  width: 50%; /* calculated: 150px */
  transform: translateX(10%); /* calculated: 15px */
}
```

`transform`의 퍼센트는 **자기 자신을 비율**로 갖는다.

## Dimensions and lengths

길이는 단위에 따라 **절대적, 상대적**으로 결정된다.

### 절대 단위

![](https://velog.velcdn.com/images/kbm940526/post/e8f04788-2224-457e-8f6f-c8417b4f83c5/image.png)

### 상대 단위

![](https://velog.velcdn.com/images/kbm940526/post/c6f8669a-f9bc-4cfb-906e-e5bf38da0de8/image.png)

> rem vs em
> font-size를 기준으로 크기를 잡는 것이 em이다.
> rem과 em의 차이는 기준이 누구냐에 따라 다르다.
> rem은 Root em으로 root Element를 기준으로 em은 본인 ELement를 기준으로 한다.

### Viewport-relative units

- vw : width의 퍼센트
- vh : height의 퍼센트
- vi : root 요소의 인라인 축 방향으로 퍼센트
- vb : root 요소의 블록 축 방향으로 퍼센트
- vmin, vmax : viewport width, heigth 중 크고 작은거 기준 퍼센트

## Angle units

`deg`단위를 사용한다.

```css
div {
  width: 150px;
  height: 150px;
  transform: rotate(60deg);
}
```
