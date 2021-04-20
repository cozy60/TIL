## mixin - 자주쓰는 코드 함수로 재활용하기
### 기본 사용법
```scss
// @mixin을 선언하고,
// 함수 이름과 파라미터 작성
@mixin hongsi() {
  color: red;

  .ic-close {
    width: 40px;
  }
}

// 사용할때는 @include를 붙이고,
// 함수이름()으로 호출한다,
p {
  @include hongsi();
}
```
컴파일 하면 아래와 같이 출력된다.
```css
p {
  color: red; }
  p .ic-close {
    width: 40px; }
```
### 인자 활용하기
```scss
@mixin hongsi($color) {
  color: $color;

  .ic-close {
    width: 40px;
  }
}

p {
  @include hongsi(aqua);
}

P {
  @include text-style-12; // 아무런 값을 넣지 않으면, 괄호를 생략해도 된다.
}
```
컴파일 하면 아래와 같이 출력된다.
```css
p {
  color: aqua; }
  p .ic-close {
    width: 40px; }
```
### 예외처리
mixin을 호출할 때, 인자를 받는 mixin에 인자를 넣지 않으면 오류가 난다. 이떄 인자 옆에 콜론을 쓴 뒤 기본값을 지정해주고 예외처리를 하면 된다.
```scss
@mixin text-style-12($color: false) {
  font-size: $font-size-12;
  line-height: $line-hieght_12;
  letter-spacing: $letter-spacing-12;
  color: $color;

  @if ($color != false) {
    color: $color;
  }
}
```
하지만 위와 같은 방법은, 아래와 같은 상황 일 때는 문제가 생긴다.
```scss
p {
  @include text-style-12(13px);
}

P {
  font-size: 12px;
  line-height: 16px;
  letter-spacing: -0.005em;
  color: 13px; } // error
```
이떄 `@typeof`를 사용하면 조금 더 쉽게 예외처리를 할 수 있다.
```scss
// type이 color일때만
@if (type-of($color) == color) {
  color: $color;
}
```
유효성 검사 로직을 분리해 아래와 같이 조금 더 깔끔하게 코드를 작성 할 수 있다.
```scss
@mixin text-style($size, $color: false) {
  @if ($size == 12) {
    @include text-style-12;
  }
  @if ($size == 13) {
    @include text-style-13;
  }
  @if ($size == 14) {
    @include text-style-14;
  }
  @if ($size == 16) {
    @include text-style-16;
  }
  @if ($size == 18) {
    @include text-style-18;
  }
  @if ($size == 24) {
    @include text-style-24;
  }

  @if (type-of($color) == color) {
    color: $color;
  }
}

p {
  @include text-style(14, $secondary);
}
```