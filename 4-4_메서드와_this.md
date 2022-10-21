# 4.4 메서드와 this

객체의 프로퍼티에 함수를 할당

## 메서드 만들기

```javascript
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  alert("안녕하세요!");
};

user.sayHi(); // 안녕하세요!
```



이미 정의된 함수를 이용하는 방법

```javascript
let user = {
  // ...
};

// 함수 선언
function sayHi() {
  alert("안녕하세요!");
};

// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;

user.sayHi(); // 안녕하세요!
```



### 메서드 단축 구문

```javascript
// 아래 두 객체는 동일하게 동작 (미묘한 차이가 있응)

user = {
  sayHi: function() {
    alert("Hello");
  }
};

// 단축 구문을 사용하니 더 깔끔해 보이네요.
user = {
  sayHi() { // "sayHi: function()"과 동일합니다.
    alert("Hello");
  }
};
```



## 메서드와 this

메서드 내부에서 `this` 키워드를 사용하면 객체에 접근 가능

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // 'this'는 '현재 객체'를 나타냅니다.
    alert(this.name);
  }

};

user.sayHi(); // John
```



`this`를 사용하지 않고 외부 변수를 참조해 객체에 접근할 수 있지만, 에러 발생 가능

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(user.name); // 'this' 대신 'user'를 이용함
  }

};
```

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert( user.name ); // Error: Cannot read property 'name' of null
  }

};


let admin = user;
user = null; // user를 null로 덮어씁니다.

admin.sayHi(); // sayHi()가 엉뚱한 객체를 참고하면서 에러가 발생했습니다.
```



## 자유로운 this

JavaScript에선 모든 함수에 this 사용 가능

```javascript
function sayHi() {
  alert( this.name ); // 문법 에러 발생하지 않음
}
```

this 값은 런타임에 결정. 컨텍스트에 따라 달라짐

동일한 함수라도 다른 객체에서 호출했다면 this가 참조하는 값 달라짐

```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// 별개의 객체에서 동일한 함수를 사용함
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
```



### 객체 없이 호출하기 `this == undefined`

```javascript
function sayHi() {
  alert(this);
}

sayHi(); // undefined
```

위 코드를 엄격 모드에서 실행하면 `this`에 `undefined`가 할당

엄격 모드가 아닐 때는 `this`가 전역 객체를 참조 -> 브라우저 환경에선 `window` 전역 객체 참조

그래서 `"use strict"` 도입



### 자유로운 this가 만드는 결과

`this`는 항상 메서드가 정의된 객체를 참조할 거야.. -> bound `this`

자바스크립트에서 `this`는 런타임에 결정

메서드가 어디서 정의되었는지 상관 없이 `this`는 점 앞의 객체가 무엇인가에 따라 자유롭게 결정됨



## this가 없는 화살표 함수

화살표 함수는 일반 함수와 달리 고유한 `this`를 가지지 않음

화살표 함수에서 `this`를 참조하면, 화살표 함수가 아닌 평범한 외부 함수에서 `this` 값을 가져옴

```javascript
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName); // arrow의 this는 외부 함수 user.sayHi()의 this
    arrow();
  }
};

user.sayHi(); // 보라
```

별개의 this가 만들어지는 건 원하지 않고 외부 컨텍스트에 있는 this를 이용하고 싶은 경우 화살표 함수가 유용

