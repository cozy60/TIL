## placeholder
`%`와 placeholder명을 통해 선언하면 된다. 변수명의 작명 규칙과 동일하다.
```scss
%tag-base {
 // 공통 스타일 
}
```
### mixin과 placeholder의 차이점
placeholder는 인자를 받을 수 없다.
연관되고 공통된 스타일을 반복해서 적을 떄, placeholder를 선언한 후 상속받는 식으로 사용한다.

또한 컴파일 후 결과도 mixin과 상이하다. placeholder는 콤마로 연관이 있는 속성을 그룹으로 묶어 렌더링 한다. 일일히 속성을 지정해주는 mixin과는 다르다.
```css
.tag-red, .tag-green, .tag-gray {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  line-height: 16px;
  letter-spacing: -0.005em;
  color: false;
  height: 20px;
  padding: 0 6px;
  font-weight: 700;
  border-radius: 4px; }
```
### 사용방법
```scss
%tag-base {
  @include inline-flexbox;
  @include text-style(12);
  height: 20px;
  padding: 0 6px;
  font-weight: 700;
  border-radius: 4px;
}

.tag-red {
  @extend %tag-base;
}
```
placeholder를 사용시는 @include를 사용하지 않고 `@extend`를 사용한다.