# getter와 setter

객체의 프로퍼티는 우리가 흔히 사용하는 **데이터 프로퍼티**와 함수로서 값을 획득(get)하고 설정(set)하게하는 **접근자 프로퍼티**로 나뉩니다

오늘은 접근자 프로퍼티 **getter**, **setter**에 대해 알아보도록 하겠습니다.

## getter와 setter

```js
let obj = {
  get propName() {
    // getter, obj.propName을 실행할 때 실행되는 코드
  },

  set propName(value) {
    // setter, obj.propName = value를 실행할 때 실행되는 코드
  },
};
```

객체 안에서 getter는 `get`으로 setter는 `set`으로 나타냅니다.

### getter

`getter`메소드는 obj.propName을 사용해서 프로퍼티를 읽을 때 사용되는 메서드입니다.

```js
let user = {
  name: "Byungmin",
  lastName: "Kim",

  get fullName() {
    return `${this.name} ${this.lastName}`;
  },
};
```

### setter

`getter`의 프로퍼티는 일반 프로퍼티처럼 값을 변경할 수 없습니다. 그래서 `setter`를 사용하여 값을 변경합니다.

```js
let user = {
  name: "Byungmin",
  lastName: "Kim",

  get fullName() {
    return `${this.name} ${this.lastName}`;
  },

  set fullName(value) {
    [this.name, this.lastName] = value.split(" ");
  },
};
```

## 활용

getter와 setter를 실제 프로퍼티 값을 감싸는 wrapper처럼 사용하면 프로퍼티 값을 원하는 대로 제어할 수 있습니다.

```js
//객체 값을 통제할때

let user = {
  get name() {
    return this._name;
  },
  set name(value) {
    if (value.length < 4) {
      alert(
        "입력하신 값이 너무 짧습니다. 네 글자 이상으로 구성된 이름을 입력하세요."
      );
      return;
    }
    this._name = value;
  },
};
// 위 코드에서 _를 빼면 왜 maxium callstack이 뜨는지 모르것다 내일 숙제
```

![](https://velog.velcdn.com/images/kbm940526/post/b870da40-0d63-47fd-b34b-1a89cd5be2e4/image.png)

### 호환성을 위해 사용하기

```js
function User(name, age) {
  this.name = name;
  this.age = age;
}

let john = new User("John", 25);

alert(john.age); // 25
```

다음과 같은 코드에서 age 대신 birthday로 바뀌면 age가 사용된 모든 부분을 바꿔줘야할 것 입니다.

이를 해결하기 위해

```js
function User(name, birthday) {
  this.name = name;
  this.birthday = birthday;

  // age는 현재 날짜와 생일을 기준으로 계산됩니다.
  Object.defineProperty(this, "age", {
    get() {
      let todayYear = new Date().getFullYear();
      return todayYear - this.birthday.getFullYear();
    },
  });
}

let john = new User("John", new Date(1992, 6, 1));

alert(john.birthday); // birthday를 사용할 수 있습니다.
alert(john.age); // age 역시 사용할 수 있습니다.
```

위 와같이 변경하여 `age`도 사용할 수 있는 코드가 됩니다.

> defineProperty
> 설명자에 넣으려는 객체, 키와 `get`,`set`을 넣으면 접근자를 만들 수 있다 .
