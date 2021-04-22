## DOM
문서개체모델 DOM(Document Object Model)은 자바스크립트의 Node 개체의 계층화된 트리다.

1. HTML 문서 작성 
2. HTML 콘텐츠를 다른 HTML 콘텐츠 내에 캡슐화
3. 2를 통해 트리로 표현 가능한 계층 구조 생성
4. 해당 구조는 HTML 문서 내 들여쓰기를 통해 시각적으로 표시됨
5. 브라우저는 HTML 문서를 로딩 시, 계층 구조를 해석하고 마크업이 어떻게 캡슐화 됐는지 보여주는 노드 개체 트리, 구조화된 노드를 갖고있는 DOM을 생성

HTML 문서가 브라우저에 의해 해석되어 실제 문서를 나타내는 노드 개체들의 트리 구조로 변환된다. DOM의 목적은 JS를 사용해 이 문서에 대한 스크립트 작성(삭제, 추가, 바꾸기, 이벤트 처리, 수정)을 위한 인터ㅔ이스를 제공하는 것이다.

DOM은 원래 XML 문서를 위한 애플리케이션 프로그래밍 인터페이스 였지만, HTML 문서 내에서도 사용되도록 확장됐다.

## 노드 개체 유형
가장 일반적인 노드 유형(nodeType)
* DOCUMENT_NODE
  예: window.document
* ELEMENT_NODE
  예: `<body>`, `<a>`, `<p>`, `<script>`
* ATTRIBUTE_NODE
  예: `class="funEdges`
* TEXT_NODE
  예: 줄바꿈과 공백을 포함한 HTML 문서 내 텍스트 문자
* DOCUMENT_FRAGMENT_NODE
  예:  `document.createDocumentFragmet()`
* DOCUMENT_TYPE_NODE
  예: `<!DOCTYPE html>`

이 목록에 있는 노드 유형 형식은 JS 브라우저 환경에서 Node 개체의 속성으로 기록되는 상수 값의 속성과 동일하다. Node의 이 속성들은 상수값이며, Node 개체의 특정 유형에 매핑되는 숫자 코드 값을 저장하는데 사용된다.

nodeType은 단지 특정한 JS 인터페이스/생성자로부터 생성되는 노드가 유형을 기술하는 데 사용되는 숫자 분류에 불과하다는 점이다.

## Node 개체로부터 상속받은 하위 노드 개체
통상적인 DOM 트리의 각 노드 개체는 Node로부터 속성과 메소드를 상속받는다. 문서 내의 노드 유형에 따라 Node 개체를 확장한 하위 노드 개체/인터페이스가 추가로 존재한다. 
모든 노드 유형은 Node로부터 상속받고, 상속 체인이 길어질 수도 있다. Node는 JS의 생성자 함수에 불고화고, 논리적으로 볼 때 Node는 JS의 다른 개체들처럼 `Obejct.prototype` 으로부터 상속받는다.
이때 중요한 점은, 모든 노드가 prototype 체인의 속성뿐만 아니라 생성자로부터 일련의 기본 속성 및 메서드를 상속받는다. 