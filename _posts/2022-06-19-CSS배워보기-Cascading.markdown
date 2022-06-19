# CSS배워보기 - Cascading
CSS는 Cascading Stylesheets의 약자입니다. Cascade는 말 그대로 계단식으로 내려와 여러 CSS규칙이 HTML요소에 적용되는 알고리즘입니다. 

```css
button {
  color: red;
}

button {
  color: blue;
}
```
위 CSS코드에서 button의 색상은 무엇일까요 ?  

!codepen[byungmin12/embed/MWQRrzr?default-tab=html%2Cresult]

바로 파란색입니다.  

Cascading 계단으로 내려오기에 ```red```컬러가 된 뒤 다시 ``` blue ``` 컬러로 바뀌는 것입니다.

이러한 Cascading algorythe은 4단계로 나뉩니다.

1. 위치 및 표시 순서: CSS 규칙이 표시되는 순서
2. 특이성 : 가장 일치하는 CSS선택자를 결정하는 알고리즘
3. 오리진: CSS가 나타나는 순서와 출처, 브라우저 스타일인지, 브라우저 확장 프로그램의 CSS인지, 작성한 CSS인지 여부
4. 중요도 :  ```!important``` 규칙은 몇몇 CSS 규칙보다 우선시 된다

자 그럼 보금 더 자세히 확인해보자.

## 등장 위치와 순서

위에서 말한 것과 같이 CSS는 Cascading stylesheets. 즉 계단식 언어이다. 중요도를 나타내는 ```!important```를 제외하면 **제일 마지막에 선언된 규칙이 적용**된다.

하지만 아래와 같이 굳이 두번씩 동일한 규칙을 적용할 때가 있다. 

```
.my-element {
  font-size: 1.5rem;
  font-size: clamp(1.5rem, calc(1rem + 3vw), 2rem);
}
```
```font-size```를 두번 적용한 이유는 무엇일까 ?
바로 특정 브라우저에서 ```clamp```과 같은 규칙을 지원되지 하지 않을 경우에 사용된다. 



## 특이성
특이성은 어떤 CSS 선택자가 가장 구체적인지를 결정하는 알고리즘이다. 쉽게 말해 CSS점수 시스템이라고 생각하면된다. 그리고 이러한 점수가 같으면 뒤에 나오는 클래스가 적영됩니다. 

특이성 점수는 A-B-C-D 4개의 가중치 종류별로 개수 합을 구해서 우선순위 숫자로 비교한다.

>A : 인라인 CSS - 1000포인트
B : ID - 100 포인트
C : 클래스, 가상 클래스, 속성 선택자, 나머지 속성들 - 10 포인트 - is,not 안에 들어가는 건 점수에 포함되지 않는데
D : 요소(태그), 가상 요소 - 1포인트
* 유니버셜이나 그 외 결합 연산자는 영향을 주지 않는다
* !important는 특이성을 무시한다


더 자세한 특이성은 [여기](https://web.dev/learn/css/specificity/)에서 잘 보여준다. 문제도 있따 ! 


## 오리진 

작성한 CSS가 HTML에 적용된 유리한 CSS가 아니다. 이러한 경우 CSS가 적용되는 중요도 순서에 대해 알아야합니다.

![](https://velog.velcdn.com/images/kbm940526/post/b4287d1e-3f2c-440f-b75a-bf52e507e124/image.png)

1. 기본스타일 : 브라우저가 기본적으로 HTML 요소에 적용하는 스타일입니다. 가장 낮은 중요도를 갖습니다.
2. 로컬 사용자 스타일 : 기본 글꼴, 크기 등 운영체저에서 제공하는 스타일
3. 작성된 CSS : 우리가 흔히 style sheets에 작성하는 CSS입니다. 여기서도 ```외부 스타일시트 < 내부 스타일시트```로 적용된다.
4. !important : 위 사진에선 세개로 나뉘지만 하나로 봅니다. 

## 중요도
모든 CSS 규칙이 서로 동일하게 계산되거나 동일한 특이성이 부여되는 것이 아닙니다.

중요도도 순서가 존재합니다. 

1. font-size , background 또는 color와 같은 일반 규칙 유형
2. animation 규칙 유형
3. !important 규칙 유형(원점과 동일한 순서를 따름)
4. transition 규칙 유형

1 < 2 < 3 < 4 순입니다. 
쉽게 말해 일반 규칙들 보다 **애니메이션,important, transition이 중요**합니다. 그리고 **트랜지션은 important보다 중요**하단 것을 알아야합니다. 


# 정리 
그래서 Cascade는 **왜** 사용하냐 ?

1. 하나의 HTML Element에 여러 스타일을 적용할 때 발생하는 충돌을 해결합니다.

2. 각 각 한가지 스타일을 보장합니다.

3. CSS 점수 시스템 및 가중치 스타일 규칙을 적용합니다.

4. 스타일 속성을 정렬하고 필터링합니다. 







