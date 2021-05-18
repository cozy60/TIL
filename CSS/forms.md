## select box
### icon 적용후 클릭시 액션이 트리거가 안될떄
```css
.ic-carret {
  pointer-event: none;
}
```
셀렉트 박스에 icon을 추가해서 요소를 나타낼 때 icon 부분을 클릭하면 아무런 액션이 취해지지 않는다. 이는 select 요소의 position이 static이여서 그런것인데, 액션을 적용하려는 요소에 `pointer-event: none;`을 적용하면 해당 아이콘의 이벤트가 무시되고 select box로 위임된다.

### text 요소가 너무 많아 넘쳐날때
```html
<select class="form-select">
  <!--option[value="$"]*5{선택 사항 $}-->
  <option value="1">선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1 선택사항 1</option>
  <option value="2">선택사항 2</option>
  <option value="3">선택사항 3</option>
  <option value="4">선택사항 4</option>
  <option value="5">선택사항 5</option>
</select>
```
```css
.form-select {
  padding-right: 40px;
  text-overflow: ellipsis;
}
```
`overflow` 속성말고도 `text-overflow` 속성이 존재한다. 글자가 해당 요소에서 넘쳐날 때의 옵션을 선택하는데, `ellipsis`를 적용할 시 말줄임표가 나타난다.