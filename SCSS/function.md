## scss에서 function 사용하기
### function 사용하기
`@function`키워드를 사용한 뒤, `@return`키워드를 사용해 반환값을 지정해준다.
```scss
@function _get-flex-value() {
  @return 1;
}
```
### function과 mixin의 차이점
1. 믹스인을 사용할 때는 `@include`를 사용했지만, `@function`은 따른 키워드 없이 바로 사용할 수 있다.
```scss
@function _get-flex-value() {
  @return #ff11ff;
}

@mixin flexbox($jc: center, $ai: center) {
  display: flex;
  align-items: $ai;
  justify-content: $jc;
}

p {
  @include flexbox; // mixin, @include 사용
  font-size: _get-flex-value(); // function, 사용 x
}

```
2. function은 값을 반환한다. 특정 값만 반환을 한다. mixin은 코드 자체를 반환한다.
```scss
p {
  display: flex;
  align-items: center;
  justify-content: center; /* mixin의 값, 코드 자체를 반환함. */
  font-size: #ff11ff; /* 특정 값만을 반환함. */ }
```