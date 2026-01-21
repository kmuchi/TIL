### 리액트를 왜 써야하는가?

**JS**

`(html) 버튼 만듬 → (script) document.getElementById → handClick() 함수 → addEventLister 로 연결`

- 카운트 만드는데 4단계 거쳐야 함 + (페이지 새로고침없이, count클릭할때 HTML 업데이트 과정)
- 매우복잡함

**React**

```jsx
function Counter() {
  // count라는 변수 선언 (바뀌면 화면도 바뀜)
  const [count, setCount] = useState(0);

  return (
    // HTML과 JS가 섞여 있음 (JSX)
    // onClick 안에 함수 바로 넣음. id 찾을 필요 없음.
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

- jsx 안쓰고 react 가능하지만, 굳이? 어려움 JS보단 쉽지만

- <Compone>
    - 대문자로 시작해야함. 소문자면 <button> html태그로 인식

### State

      <어려운 방법> 

1. `<div id = “root”>` 
2. `root = document.getElmentById(”root)`
3. `fucntion countUp()`
4. `function redner(){ ReactDOM.render(<Container/>,root)}`
5. `const Container() ⇒ ( <button onClick={countUp}>`
- 5단계 거쳐야함, 바뀔때마다(카운트) 다시 리렌더링 해줘야 함

리렌더링

- 바뀐부분만 렌더링 해준다 (React가)

<쉬운방법> 

```jsx
const food = [”tomato”, “potato”]

= const [myFavFood, mySecondFavFood] = food;
```

```jsx
const [counter, setCounter] = React.useState(0);
const onClick = () ⇒ {
	setCounter(counter + 1);
};

return 
	<div>
		<button> onClick={onClick}> 클릭 </button>
	</div>
	
ReactDom.redner(</App/>,root)
```

**`state 바뀜 → 리렌링 → 바뀐부분만업데이트 (이벤트리스 이런거 다시 만드는거 x)`**

### State 사용법 2

- setCounter((current) ⇒ current + 1)
    - counter + 1 말고 → 이전값 기준으로 +1 하기
- setCounter(333);    :  특정값으로 바꾸기

### props

- prpos.banana
- {banana} ← 이렇게 인자 받아오는 것도 가능
- return <Btn text={value} onClick={changeValue}/>
    - 이렇게 해도, 이벤트리스너 x , 그냥 props 이름일 뿐임

### Memo

- 메모이제이션
- 부모컴포넌트 바뀜 → 자식컴포넌트 리렌더링
    - 근데 자식컴포넌트는 반영 x (부모컴포넌트의 개별요소만 바뀜) 이럴 때 사용한다.
- `React.memo()`

### useEffect

- 처음실행 될때 한번만 실행 ( [] 빈 괄호로 두면)
- state가 변화해도 한번만 실행
- [괄호]에 해당 변수 넣으면 → 해당 변수 바뀔때 마다 실행

### useRef

1. UI 화면
    - DOM 모아놓았다가 → 업데이트시 반영되는 것으로 보임
2. 내부 데이터(실제값)
    - 실제 메모리는 변화함 (실시간임)

### className

- js에서 class는 이미 선점하고 있어서 ⇒ className 으로 써야 함
- for ⇒ htmlFor

### 라우팅

> `이 url이면 → 이 화면 보여줘`
> 

React Router DOM이 표준

- src/routes/Router.jsx 만들어서 → 정리 → App.jsx에서 연결
- Link는 html a태그 = 이 URL로 이동해!

### useNavigate

> 장고의 redirect() 같은 것
> 
- 화면에서 보이는 링크 : <Link>
- 로직에서 이동시킬 땐 useNavigate()

### Sidebar

- src/components/Sidebar.jsx ⇒ src/components/Layout.jsx
- 실제페이지에서 Layout import 해서 사용

### Axios(라이브러리)

- 자동으로 JSON 바꿔줌
- 에러 → catch로 잡아 줌
- 객체 → 문자 바꿔서 보낼 필요 X  ( 그냥 넣으면 됨)
- 기본설정 만들고 재사용 가능
- useEffect → async → (try) await axios.get(”주소”) →