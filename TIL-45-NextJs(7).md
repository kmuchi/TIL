26-03-18

### proxy.ts

> Next.js 16+ 미들웨어에서 이름 바뀜
> 

```jsx
import { NextResponse } from 'next/server'
```

- redirect
- 그냥 통과 : `next`
- 같은것들 가져오

```jsx
import type { NextRequest } from 'next/server'
```

- request 어떤 구조인지 타입스크립트 한테 알려주는  용도

```jsx
const PUBLIC_PATHS = ['/login', '/signup']
```

- 로그인 안해도 공개된 페이지 목록

### 프록시 함수

```jsx
export function proxy(request: NextRequest) {
```

- 사용자 → 경로 요쳥시 → 페이지 이동전에 → 이 함수가 먼저 실행됨
- 사용자가 `/dashboard` 들어가려 함
- 페이지 보여주기 전에 `proxy()`가 먼저 검사
- 쿠키 있는지, 공개 페이지인지 확인
- 통과시킬지 리다이렉트할지 결정

### 현재 경로 꺼내기

> pathname만 추출해오자 (구조분해할당)
> 

```jsx
const { pathname } = request.nextUrl
```

- `protocol` → `http:`
- `host` → `localhost:3000`
- `pathname` → `/dashboard`
- `search` → `?tab=1`
- `hash` → `#section`

### 쿠키에서 accessToken 꺼내기

```jsx
const token = request.cookies.get('accessToken')?.value
```

- request 받아온거에서 있으면 `value` 꺼내고 없으면 `undefined`

### 그냥 통과

```jsx
return NextResponse.next()
```

- 조건 분기에 해당 안되면, 요청 막지 말고 원래 Next.js 하려던 대로 계속 진행

### 미들웨어/proxy가 할수 있는거

1. 가로채서 다른 페이지로 보냄
2. 아무것도 안 하고 통과시

## 왜 “통과”라고 표현하냐

proxy는 페이지 그 자체가 아니라 **문지기** 같은 거예요.

문지기가 허락만 하고, 안쪽 UI는 원래 페이지가 알아서 렌더링합니다.

### OAuth2

- OAuth 1.0 : 매 요청마다 서명하는 방식
- OAuth2.0 : 토큰으로 권한 위임 방식

### Link vs router

- `Link`는 유저가 클릭해서 페이지 이동하게 만드는 태그 / 컴포넌트
    - 사용자가 눌러서 이동할때 사용
- `router` : 코드 안에서 직접 페이지 이동을 제어하는 객체
    - 조건에 따라 코드로 이동시켜야 할 때 사용
    - 리액트에서는 useNavigate() 사용

```jsx
  const router = useRouter()
```

- 라우터객체 변수 할당

```jsx
const router = {
  push(url) {
    // url로 이동
  },
  replace(url) {
    // 현재 페이지를 대체하며 이동
  },
  back() {
    // 뒤로 가기
  },
}
```

### window.location.href

- 외부 URL or 백엔드 인증 엔드포인트 브라우저 전체이동 (내부SPA 이동이 아니라)
- 그러면 `router.push()` 보다 `window.location.href` 쓰는 경우가 많음