# WAI-ARIA Roles

`<div role="region">` `<li role="panel">`에서 role은 무엇일까?👀
WAI-ARIA중 하나인 role 속성이다. WAI-ARIA중 하나인 aria-label은 스크린리더상에서 읽어주는 의미있는 마크업을 할때 썼고, aria-hidden은 의미없는 마크업일 경우 붙혀 사용한다. role도 그런 속성중 일부로, 마크업만으로는 태그의 의미를(뉘앙스를)전달할 수 없을땐 `role`을 사용해 의미를 전달시켜준다.

## ARIA: article role, ARIA: form role..

ARIA Role중 article, form과 같이 HTML상에서 충분히 표현 가능한 요소임에도 정의된 role이 있다. 그러나 가끔 `<article>`과 같은 시맨틱 태그를 사용할 수 없는 경우가 나타나는데, 이 경우 `<div role="article">`과 같이 우회해서 사용할 수 있다. 임시방편(?) 우회책처럼 사용 가능한 친구이나, 가능한 시맨틱태그로 작성하는 걸 권장한다.

### region

region은 중요한 컨텐츠, 랜드마크 컨텐츠를 갖고있는 요소를 표현할때 `role=region`을 사용한다. 이를 사용하면 스크린리더가 굉장히 쉽게 액세스 할 수 있게 반응한다(라고 한다).

### tab

요소간의 관계성을 표현할때 사용한다. tab과 tabpanel을 같이 사용하므로써 관계성을 표현할 수 있다.
예를 들자면 tab은 원하는 매뉴를 선택하면 관련된 요소를 선택할 수 있게 할때 쓴다. 원하는 메뉴를 tab으로 표현하고, 그와 관련된 요소를 정의할때 tabpanel를 사용하면 두 요소가 관련된 요소임을 알 수 있다.

## 좀더 밀접한 관계성을 표현하기 - aria-labelledby

표현하려는 요소에 id값을 준 뒤(예: `div id="item1"`), 연관된 요소에 `aria-labelledby=작성한 id값`을 사용하면 두 요소간의 관계성을 확실히 정의해 연결할 수 있다. 이러한 관계성은 마치 `<label for="test">`과 `<input id="test">`를 사용해 두 요소가 연결됨을 표현할때와 유사하다. 해당된 요소는 id를 통해 라벨링이 되었다-와 연결해서 이해하면 쉽다.

## role

role속성을 추가한다고 해서 실제로 마크업된 내용이 달라지진 않다. 그러나 이러한 태그를 사용해 작성한 태그의 의미와 관계를 확실히 정의하고 접근성을 향상시키는 효과를 발생한다.

정리하자면 role은..
HTML5로 표현할 수 없는 뉘앙스, 맥락을 role로 표현할 수 있다!

예를 들자면 아래와 같이 서로 연관된 리스트를 마크업 하고싶은데 HTML자체로는 의미가 전달되지 않을때, role 속성을 사용해주면 연관된 요소임을 파악할 수 있게 된다. 

```html
<div role="region">
    <ol>
      <li role="tabpanel">
        <!-- 내용 -->
      </li>
    </ol>

    <ol role="tablist">
      <li role="tab">
        <!-- 내용 -->
      </li> 
    </ol>
  </div>
```

