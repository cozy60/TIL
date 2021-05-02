## map
scss에서 map은 우리가 js에서 사용하는 map과 유사하다. key-value 형식으로 짝지어서 사용한다. 변수를 선언하는 것처럼 선언한 후, 소괄호를 이용해 내용을 작성하면 된다.
```scss
$flex-map: (
  start: flex-start;
  end: flex-end;
  between: space-between,
  arround: space-around,
  stretch: stretch,
  center: center;
);
```

### map-get()
`map-get()`은 scss가 제공하는 함수이다.
```scss
map-get($map: , $key: );
```

map과 `map-get()`함수를 사용하면 `@if`를 사용한 번거로운 분기문 처리등을 손쉽게 사용할 수 있다.
* 리팩토링 전
```scss
@function _get-flex-value($key) {
  @if ($key == start) {
    @return flex-start;
  }
  @if ($key == end) {
    @return flex-end;
  }
  // ...
}
```
* 리팩토링 후
```scss
$flex-map: (
  start: flex-start,
  end: flex-end,
  between: space-between,
  arround: space-around,
  stretch: stretch,
  center: center,
);

@function _get-flex-value($key) {
  @return map-get($flex-map, $key);
}
```