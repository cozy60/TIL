## scss에서 반복문 사용하기 
```scss
$sm-columns: 4;
@for $i from 1 through $sm-columns {
  @debug $i; // 1,2,3,4
}
```
먼저 사용할 변수 `$i`를 선언해준 후, 1부터 반복을 종료할 값을 `through`뒤에 선언해주면 된다.

### 반복문에서 숫자 사용하기
```scss
@for $i from 1 through $sm-columns {
  .col-sm-$i {
    width: $i / $sm-columns * 100%;
  }
}
```
```css
.container .col-sm-$i {
    width: 25%; }
.container .col-sm-$i {
  width: 50%; }
/* .... */
```
위와 같은 값은 `.col-sm`뒤에 숫자가 오지 않고 `$i`가 문자 그대로 출력된다.
```scss
@for $i from 1 through $sm-columns {
  .col-sm-#{$i} {
    width: $i / $sm-columns * 100%;
  }
}
```
`#{$변수명}`과 같은 식으로 작성하면, 변수 안의 값을 출력하게 된다. 

### %(percent) 계산 쉽게하기
%를 계산하기 위해선 위와같이 100%를 곱해줬는데, scss에서 제공하는 내장함수 `percentage`를 사용하면 손쉽게 계산할 수 있다.
```scss
width: percentage($i / $sm-columns);
```
