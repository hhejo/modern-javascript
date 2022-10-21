# 2.13 while과 for 반복문

## 'while' 반복문

생략..

## 'do...while' 반복문

생략..

## 'for' 반복문

```javascript
for (let i = 0; i < 3; i++) {
  alert(i);
}
```

## 반복문 빠져나오기

`break`

## 다음 반복으로 넘어가기

`continue`

## break/continue와 레이블

```javascript
labelName: for (...) {
  ...
}
```

```javascript
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    let input = prompt(`(${i},${j})의 값`, "");

    // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나옵니다.
    if (!input) break outer; // (*)

    // 입력받은 값을 가지고 무언가를 함
  }
}
alert("완료!");
```

레이블을 별도의 줄에 쓸 수도 있음

```javascript
outer:
for (let i = 0; i < 3; i++) { ... }
```
