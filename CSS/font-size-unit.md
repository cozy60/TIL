## font-size: 1em;
저번 설명에서도 언급했다 싶이 `em`단위는 font-size의 영향을 받는다. 그러나 코드를 살펴보면 `font-size: 1em;`과 같이 작성되어 있는 경우가 있는데, 이는 어떻게 되는걸까?

답은 간단하다. 전체 페이지에서 폰트 크기를 정의하지 않으면 일반적으로는 브라우저의 기본값인 16px로 지정된다.
![image](https://user-images.githubusercontent.com/49024995/118906912-9bad8400-b959-11eb-83fd-d8910e7bc674.png)

브라우저의 기본 폰트값을 변경하면 1em의 값도 변하게 된다. 이는 브라우저의 폰트 사이즈를 상속받게 됨을 알 수 있다.
![image](https://user-images.githubusercontent.com/49024995/118907032-c8619b80-b959-11eb-9128-11c8a81b3e28.png)
![image](https://user-images.githubusercontent.com/49024995/118907003-bd0e7000-b959-11eb-8b92-0345472e8421.png)

만약 body에서 font size를 지정해주면, body에서 지정한 font size의 값을 상속받게 되고 사용자가 브라우저에서 지정하는 폰트 크기에 영향을 받지 않게 된다.
```css
body {
  font-size: 10px;
}

p {
  font-size: 1em;
}
```
![image](https://user-images.githubusercontent.com/49024995/118907200-137bae80-b95a-11eb-875c-5d23c8a735a1.png)

기본 폰트 사이즈를 px로 지정하면 어떤 브라우저, 어떤 운영체제에서든 동일한 결과값을 나타낸다. 그러나 이는 웹 접근성을 저하시키는 요인이므로 웹 접근성이 중요한 페이지를 설계할 시 px사용은 지양해야 한다. 

### px처럼 em을 사용하고 싶을 때
> 구하고자 하는 엘리먼트의 px값 / 부모 엘리먼트의 font-size px 값

페이지의 폰트 크기가 1em이고, 브라우저의 기본 값이 1em=16px일때 12px 폰트 크기로 지정하고 싶다면 `12/16=0.75`로 계산하면 된다. (0.75em)

## 번외
자주쓰이는 %나 em, rem, px같은 단위외의 존재도 알게 되었다.
```css
/* <absolute-size> 값 */
font-size: xx-small;
font-size: x-small;
font-size: small;
font-size: medium;
font-size: large;
font-size: x-large;
font-size: xx-large;

/* <relative-size> 값 */
font-size: larger;
font-size: smaller;

/* 전역 값 */
font-size: inherit;
font-size: initial;
font-size: unset;
```
- xx-small, x-small, small, medium, large, x-large, xx-large
사용자가 설정한 기본 폰트 크기에 따라 정해진다. `<font size="1">`부터 `<font size="7">` 와 같은 HTML 과 유사하게 표현된다. 기본 유저 폰트 크기는 `<font size="3">` 이다.

따로 기본 폰트 사이즈를 지정하지 않을 시 medium이 가장 기본적인 사이즈(브라우저의 기본 사이즈인 16px)이고, large는 18px, x-large는 24px, xx-large는 32px이다. x-small은 10px, small은 13px이다.

`inherit`는 부모 요소의 값을 상속받고, `initial`는 기본값으로 설정한다. `unset`은 부모로부터 상속받을 값이 존재하면 상속값을, 그렇지 않다면 초깃값을 사용하도록 한다.


