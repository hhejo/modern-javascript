# 2.12 nullish 병합 연산자 '??'

`??`

- 여러 피연산자 중 그 값이 '확정되어 있는' 변수를 찾을 수 있음

`a ?? b`

- `a`가 `null`도 아니고 `undefined`도 아니면 `a`
- 그 외의 경우는 `b`

```javascript
x = a !== null && a !== undefined ? a : b;
```

```javascript
let firstName = null;
let lastName = null;
let nickName = "바이올렛";

// null이나 undefined가 아닌 첫 번째 피연산자
alert(firstName ?? lastName ?? nickName ?? "익명의 사용자"); // 바이올렛
// nickname도 값이 없었다면 "익명의 사용자" 출력
```

## '??'와 '||'의 차이

- `||`는 첫번째 truthy 값을 반환
- `??`는 첫번째 정의된(defined) 값을 반환

`null`과 `undefined`, `0`을 구분해 다뤄야할 때 중요

```javascript
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

## 연산자 우선순위

안전성 관련 이슈 때문에 `??`는 `&&`나 `||`와 함께 사용할 수 없음
