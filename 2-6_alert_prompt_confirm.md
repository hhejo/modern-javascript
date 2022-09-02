# 2.6 alert, prompt, confirm



## alert

`alert()` : 모달 창 띄움



## prompt

```javascript
result = prompt(title, [default]);
```

title : 사용자에게 보여줄 문자열

default : 입력 필드의 초깃값(선택값)

`[...]`는 필수가 아닌 선택값인 매개변수

문자열을 반환하고, 사용자가 입력을 취소한 경우 null을 반환



## confirm

```javascript
result = confirm(question);
```

true, false 둘 중 하나 반환

