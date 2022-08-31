# 2.1 Hello, World!

웹 페이지에 스크립트를 삽입하기

```html
<script>
  alert();
</script>
```

## 모던 마크업

### `<script>` 태그의 속성들

`type`, `language` : 모던 HTML 표준에서는 사용하지 않는 속성들. 현재는 필수가 아님

```javascript
<script type="text/javascript"></script>
<script language="..."></script>
```

`src` : JavaScript 코드의 양이 많은 경우 파일로 소분해 저장 가능. 해당 속성이 있으면 태그 내부의 코드는 무시

```javascript
<script src="/path/to/script.js"></script>
<script src="https://cdnjs.cloudflare.com/..."></script>
```

스크립트를 별도의 파일에 작성하면 브라우저가 스크립트를 다운받아 캐시(cache)에 저장하기 때문에, 성능상의 이점이 있음. 여러 페이지에서 동일한 스크립트를 사용하는 경우, 브라우저는 페이지가 바뀔 때마다 스크립트를 새로 다운받지 않고 캐시로부터 스크립트를 가져와 사용. 스크립트 파일을 한 번만 다운받으면 됨. 이를 통해 트래픽이 절약되고 웹 페이지의 실제 속도가 빨라짐
