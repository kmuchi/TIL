### Components/index.js

> 주소 깔끔하게 만들기 위해서 사용
> 
- import {Sidebar } from './components';  → 자동으로 index.js 찾아서 → 각 컴포넌트 경로

### 메뉴리스트

> 네비게이션은 계속 바뀌어야 하는 값
> 
- 목업데이터로 만드는건 → API로 받아올값
- 나중에 path: ~ 경로로 바꾸면 된다.

### 템플릿 리터럴

> 백틱 + &{Name} - 변수 or 자바스크립트 코드를 문자열 중간에 넣을 수 있다.
> 

> 파이썬의 f-string과 동일한 개념이다.
> 

| **구분** | **파이썬 (f-string)** | **자바스크립트 (Template Literal)** |
| --- | --- | --- |
| **따옴표** | `f" "` 또는 `f' '` | **`` `` (백틱)** |
| **변수 넣기** | `{변수}` | **`${변수}`** |

**실제 활용 예시**

**① 동적인 `className` 설정 (가장 많이 씀)**

```jsx
function Button ({ isActive }) {
	return(
		<button className = {`btn ${isActive ? 'active' : ' ' }`}>
			클릭
		</button>
	);
}
```

**② 인라인 스타일(style)에 단위 붙일 때**

```jsx
function ProgressBar({ width }) {
  // width가 50이면 "50%"로 변환
  return (
    <div style={{ width: `${width}%` }} className="bg-blue-500 h-2" />
  );
}
```

**③ 이미지 경로가 바뀔 때**

```jsx
function UserProfile({ userId }) {
  return (
    // 예: /images/user_123.jpg
    <img src={`/images/user_${userId}.jpg`} alt="프로필" />
  );
}
```

### 시맨틱 마크업

- Semantice : 의미가 있는
- Markup : HTML 태그 작성 행위
- `CSS 초기화 된 상태에서 ul/li 같은 것들 기능적 /디자인 역할이 아예 없다`
- SEO 최적화 + 웹접근성 (시각장애인)을 위해 사용한다.
- <nav> → <ul> → <li> → <button>

### 리스트 렌더링

> 리스트(map함수) 쓸때 겹치치 않는 key값 달아줘야 함
> 

→ 추후 변경될때, 효율적으로 수정 가능 (중간에 값 추가 등등)

```jsx
{menuItems.map((item) => (
	<li key={item.label}>
```

### 구글 머티리얼 아이콘 (Google Material Icons)

- { icon: ‘settings’ }

```jsx
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons+Outlined" rel="stylesheet">

```

- 글꼴 취급하기 때문에, 따로 import가 필요없다. (Web Font 방식)
- index.html 로딩될 때 → 구글서버 → 아이콘폰트 전체 다운로드 → 해당 글자 렌더링 → CSS가 그 글자를 아이콘 모양으로 바꿔서 보여줌

### SVG Component 방식

> import {FiLogOut} from “react-icons/fi”
> 
- import 해서 가져오는 방식

### Card 컴포넌트

> 정보를 담는 네모난 컨테이너 박스
> 
- 네보 박스 스타일이 반복되니까 → 컴포넌트 미리 만들어 두고 재사용
- `card 컴포넌트에 {children}을 안 써주면 → App.jsx에서 아무리 <h1>, <p> 집어넣어도 Card안에는 아무것도 표시 X`

```jsx
const Card = ({ children, className = '', padding = 'p-6' }) => {
    return (
        <div className={`bg-white rounded-[24px] ${padding} shadow-[0_4px_20px_rgba(0,0,0,0.02)] border border-gray-100 ${className}`}>
            {children}
        </div>
    );
};
```

- 공통 className + (입력)(padding) + (공통) shadow + (공통) border + (입력) className
- Card 그리고 → 이 Card 위에[ Children 그린다.
- Children은 실제 사용하는 코드에서 <card> </Card> 사이에 있는 값들

### interface(인터페이스)(타입스크립트용)

> 객체의 설계도(설명서)
> 

```jsx
// 1. 설계도(약속)를 먼저 만듭니다.
interface User {
  name: string;   // 이름은 무조건 문자열!
  age: number;    // 나이는 무조건 숫자!
  isAdmin: boolean; // 관리자 여부는 참/거짓!
}

// 2. 이제 이 변수는 저 설계도를 따릅니다.
const user: User = {
  name: "홍길동",
  age: 25,
  isAdmin: false
}

// ✅ 장점 1: 오타 잡기
console.log(user.ag); // 🚨 빨간줄 쫙! "ag라는 건 User에 없어요!"

// ✅ 장점 2: 빼먹기 방지
const user2: User = {
  name: "김철수" 
  // 🚨 빨간줄! "age랑 isAdmin이 빠졌어요!"
}
```

- Props 정의할 때 90% 이상

### 호버(Hover)

> 마우스 커서를 요소 위에 ‘둥둥 띄운다(Hover)’라는 뜻에서 나온 말
> 
- transition-colors  이거 추가해야 부드러워지는데, 보통 위에 div 에서 전체 다 적용

### **transition-all**

> 배경, 색상, 크기, 위치 등 모든 속성의 변화를 부드럽게 만들어줌
>