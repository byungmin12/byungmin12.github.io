프로젝트를 진행하다보면 router를 사용하여 페이지 이동하는 경우가 생길 것이다.
이런경우 우리는 흔히 **useNavigate**을 사용할 수 있다.

# useNavigate

```js
import { useNavigate } from "react-router-dom";
.
.

let navigate = useNavigate();
.
.
.
<button onClick={()=>{navigate("/")}}>
  home
</button>
```

대충 이러한 사용법이다 .
navigate안에는 첫번째 인자로 Path가 들어간다는 것만 기억하자.

## option

### 상황 1 => props,state 전달

홈페이지가 이동했을 때 우리는 state을 전달하고 싶은 경우가 있을 것이다.
물론 useState이나 redux, recoil들을 사용하여 저장하는 방법도 있겠찌만, useNavigate을 사용하면 보다 편하게 사용이 가능하다

```js
import { useNavigate } from "react-router-dom";
.
.

let navigate = useNavigate();
.
.
.
<button onClick={()=>{navigate("/",{state:내가원하는 값})}}>
  home
</button>
```

이런식으로 navagate의 두번째 옵션으로 state을 넣어주면 된다.

그리고 이것을 사용하려는 component에서 useLoaction을 사용하여 state값을 받아오자

```js
import { useLocation, useParams } from "react-router";
.
.
.
 const { state } = useLocation()
```

#### type

typescript를 사용한다면 타입을 설정해줘야한다.

useLocation의 타입을 보면 Location이라는 타입을 갖는다.
그러다보니 state의 타입은 unknown으로 받아온다. (이유는 Location 타입에 state을 unKnown으로 되어있음 )

reat router에 이슈를 올려보니 v6 이상부터는 Location에 generic이 들어가서

```js
const { state } = useLocation<{state:string}>()
```

이런식으로 들어가면 된다고한다.

**하지만 본인은 v6.3.0을 사용함에도 불구하고 안된다 ...**

그래서 찾은 해결책은 unknown으로 만들고 그 위에 타입을 입히는 것이었다.

```js
 const { state } = useLocation() as unknown as {
    state: string;
  };
```

이러면 타입을 넣어줄수있따.

**물론 답은 아니다.**

### 상황 2 => 뒤로가기 시 홈으로

사용자가 뒤로가기 버튼을 눌렀을 때 이전 페이지가 아닌 홈으로 보내고 싶을 때는

```js
import { useNavigate } from "react-router-dom";
.
.

let navigate = useNavigate();
.
.
.
<button onClick={()=>{navigate("/test",{replace: true})}}>
  home
</button>
```

로 넣어주면 된다 (default = false)
