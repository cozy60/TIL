## Ref와 DOM

> Ref는 render 메서드에서 생성된 DOM 노드나 React 엘리먼트에 접근하는 방법을 제공한다.

일반적인 React의 데이터 플로우에서 `props` 는 부모 컴포넌트가 자식과 상호작용 할 수 있는 유일한 수단이다. 그러나, 일반적인 데이터 플로우에서 벗어나 직접적으로 자식을 수정해야 하는 경우도 있다. 이때 수정할 자식은 React 컴포넌트의 인스턴스일 수도 있고, DOM 엘리먼트 일수도 있다. React에서는 두 경우 모두를 위한 해결책을 제공한다.

**선언적으로 해결 될 수 있는 문제에서는 `ref` 사용을 지양 해야 한다.** 

예를 들어, `Dialog` 컴포넌트에서 `open()` 과 `close()` 메서드를 두는 대신, `isOpen` 이라는 prop을 넘겨주는게 좋다.

---

### Ref 생성

```jsx
const refContainer = useRef(initialValue);
```

`useRef` 는 `.current` 프로퍼티로 전달된 인자(`initialValue`)로 초기화된 변경 가능한 `ref` 객체를 반환한다. 반환된 객체는 컴포넌트의 전 생애주기를 통해 유지된다.

### Ref에 접근하기

일반적으로 사용되는 경우는 자식에게 명령적으로 접근하는 경우다,

```jsx
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // 마운트된 input text 요소를 current가 가르킨다.
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

본질적으로 `useRef` 는 `.current` 프로퍼티에 변경 가능한 값을 담고있는 상자와 같다.

DOM에 접근하는 방법으로 refs를 사용할때, `<div ref={myRef} />` 를 사용한다고 예를 들자. 이때 React로 ref 객체를 전달한다면, React는 모드가 변경될 때 마다 변경된 DOM 노드에 그것의 `.current` 프로퍼티를 설정한다.

`ref` 속성보다 `useRef()` 가 더욱 유용하다. 이는 **어떤 가변값을 유지하는데 편리**하다.

`useRef()` Hooke은 DOM ref만을 위한 것이 아니다. `ref` 객체는 현재 프로퍼티가 변경 할 수 있고, 어떤 값이든 보유할 수 있는 일반 컨테이너다. 이는 class의 인스턴스 프로퍼티와 유사하다.

이것은 `useRef()` 가 **순수 자바스크립트 객체를 생성**하기 때문이다. `useRef()` 와 `{current: ...}` 객체 자체를 생성하는 것의 유일한 차이점이라면, `**useRef()` 는 매번 렌더링 할때 동일한 `ref` 객체를 제공한다.**

`useRef()` 는 내용이 변경 될 때 그것을 알려주지 않는다. `.current` 프로퍼티를 변형하는 것이 리렌더를 발생하지 않는다. React가 DOM 노드에 `ref`를 붙이거나 제거 할 때 어떤 코드를 실행하고 싶다면 **콜백 ref** 를 사용해야 한다.

### 콜백 ref

```jsx
function MeasureExample() {
  const [height, setHeight] = useState(0);

  const measuredRef = useCallback(node => { // 콜백 ref
    if (node !== null) {
      setHeight(node.getBoundingClientRect().height);
    }
  }, []);

  return (
    <>
      <h1 ref={measuredRef}>Hello, world</h1>
      <h2>The above header is {Math.round(height)}px tall</h2>
    </>
  );
}
```

React는 ref가 다른 노드에 연결될 때마다 해당 콜백을 호출한다. 콜백 ref를 사용하면 자식 컴포넌트가 나중에 측정된 노드를 표시하더라도 (예: 클릭에 대한 응답) 여전히 부모 컴포넌트에서 이에 대한 알림을 받고 측정을 업데이트 할 수 있다.

`[]` 를 `useCallback` 에 종속성 배열로 전달한다. 이렇게 하면 ref 콜백이 다시 렌더링 간에 변경되지 않음으로React가 불필요하게 호출되지 않는다.

Hook을 사용해 이 로직을 추출할 수 있다.

```jsx
function MeasureExample() {
  const [rect, ref] = useClientRect();
  return (
    <>
      <h1 ref={ref}>Hello, world</h1>
      {rect !== null &&
        <h2>The above header is {Math.round(rect.height)}px tall</h2>
      }
    </>
  );
}

function useClientRect() {
  const [rect, setRect] = useState(null);
  const ref = useCallback(node => {
    if (node !== null) {
      setRect(node.getBoundingClientRect());
    }
  }, []);
  return [rect, ref];
}
```

---

## DOM 에 refs 전달하기

```jsx
// 기본 button DOM 요소를 렌더링 하는 FancyButton 컴포넌트를 가정
function FancyButton(props) {
  return (
    <button className="FancyButton">
      {props.children}
    </button>
  );
}
```

`FancyButton` 를 사용하는 다른 컴포넌트들은 일반적으로 내부 `button` DOM 요소에 대한 `ref`를 얻을 필요가 없다.

이런 캡슐화는 재사용성이 높은 "말단" 요소에서는 불편하게 적용된다. 이런 컴포넌트들은 일반적인 DOM `button` 이나 `input` 과 유사한 방법으로 애플리케이션 전체에 걸쳐 사용되는 경향이 있다. 그리고 포커스, 선택, 애니메이션을 관리하기 위해서는 이런 DOM 노드에 접근하는 것이 불가피 할 수 있다.

### forwardRef

`forwardRef` 는 전달받은 `ref` 어트리뷰트를 하부 트리 내의 다른 컴포넌트로 전달하는 React 컴포넌트를 생성한다. 이 기법은 아래 두 시나리오에서 특히 유용하다.

- DOM 엘리먼트로 ref 전달
- HOC로 ref 전달하기

`forwardRef` 는 렌더링에 사용될 함수를 인자로 받을 수 있다. React는 이 함수를 두개 인자 `props` 와 `ref`를 사용해 호출하고, 이 함수는 React 노드를 반환한다.

```jsx
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// 이제 <button> DOM 엘리먼트를 직접 참조할 수 있다.
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

위의 예시에서 React는 `<FancyButton ref={ref}>` 엘리먼트에 주어진 `ref` 를 `React.forwardRef` 호출시 렌더링 함수에 2번째 인자로 전달한다. 이 렌더링 함수는 `ref` 를 `<button ref={ref}>` 엘리먼트에 전달한다. 

따라서 React가 해당 `ref` 를 붙이고 난 뒤, `ref.current` 는 `<button>` DOM 엘리먼트 인스턴스를 직접 가리키게 된다.

단계별로 설명하자면,

1. `createRef` 를 호출해서 React ref를 생성하고 `ref` 변수에 할당
2. `ref` 를 JSX 속성으로 지정해서 `<FancyButton ref={ref}>` 로 전달
3. React는 이 `ref` 를 `forwardRef` 내부의 `(props, ref) => ...` 함수의 두 번째 인자로 전달
4. 이 `ref` 를 JSX 속성으로 지정해서 `<button ref={ref}>` 로 전달
5. ref가 첨부되면 `ref.current` 는 `<button>` 의 DOM 노드를 가르키게 된다.

### useImperativeHandle

```jsx
useImperativeHandle(ref, createHandle, [deps])
// 첫번째 인자: 프로퍼티를 부여할 ref
// 두번째 인자: 객체를 리턴하는 함수. 이 객체에 추가하고 싶은 프로퍼티를 정의
```

`useImperativeHandle` 는 `ref` 를 사용할 때 부모 컴포넌트에 노출되는 인스턴스 값을 사용자화 한다. `useImperativeHandle` 는 `forwardRef` 와 더불어 사용한다.

```jsx
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => { // 함수가 반환하는 값이 부모의 ref객체가 참조하는 값
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput);
```

위의 예제에서 `<FancyInput ref={inputRef} />` 를 렌더링한 부모 컴포넌트는 `inputRef.current.focus()` 를 호출할 수 있다.

### 예

```jsx
// 부모 컴포넌트
function ParentComponent() {
  // inputRef라는 동아줄을 만들어서 자식에게 보낸다
  const inputRef = useRef();
  return (
    <>
          <FancyInput ref={inputRef} />
          <button onClick={() => inputRef.current.realllyFocus()}>포커스</button>
    </>
  )
}
```

```jsx
function FancyInput(props, ref) {
  // 부모가 내려준 동아줄 ref에다가 이것 저것 작업을 한다
  // 부모는 이 로직에 대해 모르고, 위로 끌어올리지 않고도 그냥 ref.current로 접근하여 사용만 하면 된다
  useImperativeHandle(ref, () => ({
    reallyFocus: () => {
      ref.current.focus();
      console.log('Being focused!')
    }
  }));
  // ref는 input을 참조하고 있다. 
  return <input ref={inputRef} />
}

// ref를 컴포넌트에 달 때는 forwardRef로 감싼다
FancyInput = forwardRef(FancyInput)
```

부모 컴포넌트에서 자식 컴포넌트의 값을 호출할 수 있다.
