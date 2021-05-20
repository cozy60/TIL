## `&`선택자
```css
/* 기존 css */
.gnb {
  position: relative;
}

.gnb-icon-button {
  background-color: hotpink;
}
```
위와 같이 gnb라는 접두어를 쓸 경우 접두어를 꼭 붙어줘야 한다. 하지만 scss에서 `&` 선택자를 사용하면 해당 요소 안에 들어간 선택자는 자동으로 부모 선택자의 이름이 들어가게 된다.

```scss
.gnb {
  position: relative;

  &-icon-button {
    background-color: hotpink;
  }
}
```
```css
/* 컴파일 후 */
.gnb {
  position: relative;
}
.gnb-icon-button {
  background-color: hotpink;
}
```