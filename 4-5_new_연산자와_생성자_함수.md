# 4.5 new 연산자와 생성자 함수

`new` 연산자와 생성자 함수를 사용하면 유사한 객체를 여러 개를 쉽게 생성



## 생성자 함수

constructor function와 일반 함수에 기술적인 차이는 없음 다만

1. 함수 이름의 첫 글자는 대문자
2. 반드시 `new` 연산자를 붙여 실행



```javascript
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("보라");

alert(user.name); // 보라
alert(user.isAdmin); // false
```

1. 빈 객체를 만들어 `this`에 할당
2. 함수 본문 실행. `this`에 새로운 프로퍼티를 추가해 `this`를 수정
3. `this`를 반환



`new User(...)`가 실행되면 일어나는 일

```javascript
function User(name) {
  // this = {};  (빈 객체가 암시적으로 만들어짐)

  // 새로운 프로퍼티를 this에 추가함
  this.name = name;
  this.isAdmin = false;

  // return this;  (this가 암시적으로 반환됨)
}
```



아래와 동일하게 동작

```javascript
let user = {
  name: "보라",
  isAdmin: false
};
```



### new function() {...}

익명 생성자 함수

```javascript
let user = new function() {
  this.name = "John";
  this.isAdmin = false;

  // 사용자 객체를 만들기 위한 여러 코드.
  // 지역 변수, 복잡한 로직, 구문 등의
  // 다양한 코드가 여기에 들어갑니다.
};
```



## new.target과 생성자 함수

`new.target`의 반환 값

- 일반적인 방법으로 함수 호출 -> `undefined` 반환
- `new`와 함께 호출 -> 함수 자체를 반환



## 생성자와 return문

생성자 함수에는 보통 `return`문이 없음. 반환해야 할 것들은 모두 `this`에 저장되고, `this`는 자동으로 반환되기 때문에 반환문을 명시적으로 쓸 필요 없음

`return`문이 있다면

- 객체를 `return`한다면 `this` 대신 객체가 반환됨
- 원시형을 `return`한다면 `return`문이 무시됨



### 괄호 생략하기

인수가 없는 생성자 함수는 괄호를 생략해 호출 가능

```javascript
let user = new User; // <-- 괄호가 없음
// 아래 코드는 위 코드와 똑같이 동작합니다.
let user = new User();
```



## 생성자 내 메서드

