### const Login: React.FC

> `React.FC`는 **React Functional Component** (리액트 함수형 컴포넌트)의 줄임말
> 

### 로그인 : 리다이렉트

> 성공 : 어디서 왔는지 확인 있으면 → 그 페이지로 보냄 (없으면 홈)
> 
- 리다이렉트(Redirect) : 다른 페이지로 자동 이동
- 네비게이션(Navigation) : 페이지 이동 전반
- 라우팅(Routing) : URL에 따라 페이지 연결

### 로그인 : 실패

**① 인라인(Inline) 방식 (가장 추천 )**

입력창 테두리를 빨간색으로 바꾸고, 바로 아래에 작은 글씨로 경고 문구를 띄우는 방식입니다.

- 장점: 사용자가 어디를 고쳐야 할지 직관적으로 알 수 있습니다.

**② 상단 경고 박스 방식**

**③ 토스트/스낵바 (Toast) 방식**

화면 하단이나 상단에서 잠시 떴다가 사라지는 팝업 메시지입니다.

### useNavigate

|  | **Link** | **useNavigate** |
| --- | --- | --- |
| **유형** | 컴포넌트 (JSX) | 훅 (함수) |
| **사용 위치** | JSX 안에서 | 이벤트 핸들러, 로직 안에서 |
| **렌더링** | `<a>` 태그로 렌더링됨 | 렌더링 없음 |
- Link : `사용자가 클릭해서 이동할때`
- useNavigate : `코드에서 이동시킬때`

### e.preventDefault()

> 웹 브라우저의 기본 성격(Default)은 폼(Form) 안의 **전송(Submit) 버튼을 누르면 무조건 페이지를 새로고침**해버림
> 
- 안쓰면 → 써놓은 ID, PW 사라짐 (페이지 새로고침)
- 쓰면 → (실패시) → 에러메시지만 띄움 (값은 그대로 남아있다)

### setError(null)

> 화면에 떠 있는 **"로그인 실패" 메시지를 초기화**
> 

### trim()

> 앞 뒤 공백자르기
> 

```tsx
        if (!email.trim()) {
            setError('이메일을 입력해 주세요.');
            return;
        }
```

### axios

> HTTP 요청을 쉽게 보내주는 라이브러리예요. 백엔드 API랑 통신할 때 사용
> 

```jsx
import axios from 'axios';
// GET 요청 (데이터 가져오기)
axios.get('/api/users')
// POST 요청 (데이터 보내기)
axios.post('/api/users', { name: '홍길동', age: 25 })
// PUT 요청 (데이터 수정)
axios.put('/api/users/1', { name: '김철수' })
// DELETE 요청 (데이터 삭제)
axios.delete('/api/users/1')
```

### async / await란?

> 비동기 처리를 쉽게 만드는 문법
> 

**왜 필요한가?**

- 서버 요청은 시간이 걸림 (1초, 2초...)
- 그 동안 화면이 멈추면 안 되니까 "나중에 처리"하는 방식