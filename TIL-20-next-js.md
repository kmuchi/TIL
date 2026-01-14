
Next js

### 프로젝트 생성

```jsx
npx create-next-app@latest 폴더명
```

### 폴더구조

- /app : 앱의 모든 경로, 구성요소 + 로직  ⇒ 주로 이 영역에서 작업
- /app/lib : 함수들(기능 위주)
- /app/ui : react 컴포넌트 (html 위주)
- /app/layout.tsx : 장고의 base.html 과 비슷 (import 안해서 app폴더 내 자동 적용) / 폴더별로 layout.tsx 만들어서 적용 가능
- 

my-app/
├── src/
│   ├── app/
│   │   ├── page.tsx          # 홈페이지 (/)
│   │   ├── layout.tsx        # 전체 레이아웃
│   │   └── globals.css       # 전역 스타일
│   ├── components/           # 재사용 컴포넌트
│   └── styles/              # 추가 스타일
├── public/                   # 정적 파일 (이미지, 폰트 등)
├── .env.local               # 환경 변수
├── next.config.ts           # Next.js 설정
├── package.json
├── tsconfig.json
└── tailwind.config.ts       # Tailwind 설정

### 프로젝트 실행

```jsx
npm run dev
```

### 페이지 이동

```jsx
<Link href=""> </Link>
```

- 버튼/글자/이미지 뭐든지 Link로 감싸면 클릭 시 해당주소로 이동

### 클라이언트 컴포넌트

```jsx
"use client"
```

- 파일 상단에 선언시 → CSR (기본은 서버사이드)

### 동적 라우팅

- app/comic/[id]/page.tsx

```jsx
// params에는 주소창에 적힌 id가 들어옵니다.
export default function ComicDetail({ params }: { params: { id: string } }) {
  return (
    <div>
      <h1>이곳은 {params.id}번 만화 상세페이지입니다!</h1>
    </div>
  );
}
```

- 라우팅이 폴더 → page.tsx 생성해야 → 해당 url접근 가능해짐
- `“/” : 루트페이지(메인페이지)로 돌아가기`
- **`@/`** =  **`src/`**

### not-found.tsx

- app/not-found.tsx → 경로 없는거는 이파일 실행

### CSR

- CSR  자바스크립트 꺼놓으면 불가
- 빈 html 받아오고 → 클라이언트에서 js 렌더링
    - **`느리거나 성능 안좋으면 오래 걸릴수도`**
- 구글 크롤링봇이 Js 실행할수도 있지만, 보통 안함
- 클라이언트 → JS 로드 → UI 빌딩

### SSR

- JS 기능 꺼도 → 보임 → why? 그냥 html이니까
- 개발자 도구 가면 → script 코드 보임 (최초 UI빌드 서버에서 해줘서 보냄)
- SSR이 기본이기 때문에, API나 DB같은 거 써도 Client로 전달안됨 (그냥 page.tsx에서 써도!)

### use client

| **구분** | **'use client' 필요함?** | **예시 코드** |
| --- | --- | --- |
| **상호작용** | **YES** | `onClick`, `onChange`, `onSubmit` |
| **상태관리** | **YES** | `useState`, `useReducer`, `useEffect` |
| **브라우저 전용 API** | **YES** | `window`, `document`, `localStorage`, `sessionStorage` |
| **커스텀 훅** | **YES** | `usePathname()`, `useRouter()` 등 `use`로 시작하는 대부분 |
| **단순 출력** | **NO** (서버가 더 좋음) | 그냥 HTML 보여주기, DB에서 데이터 가져와서 뿌리기 |
- html을 interactive 하게 바꿈
- use client 붙여도 초기 HTML은 서버에서 만들어서 보내줌
    - 다만, 기본상태는 JS 아예 안보내는데, 선언시 리액트의 훅 같은 JS로직 보냄
    - 따라서, JS보내는 코드양 절약
- `use client의 의미는 backend에서 렌더링 → client에서 hydrate 한다는 의미`

### hydration

1. Next.js는 서버에서 **HTML(뼈대)**을 먼저 보내줘서 화면을 빨리 보여준다.
2. 그 뒤에 브라우저에서 **JS(기능)**를 입히는데, 이 과정을 **Hydration**이라고 한다.
3. 이 과정 덕분에 **검색 엔진(SEO)**에도 좋고 **사용자 경험(UX)**도 좋다.

| **구분** | **use client 없음 (Server)** | **use client 있음 (Client)** |
| --- | --- | --- |
| **JS 코드 전달** | **X (안 함)** | **O (함)** |
| **HTML 렌더링** | O (서버에서 만듦) | O (서버에서 만듦) |
| **Hydration** | **X (안 함)** | **O (함)** |
| **상호작용** | **불가능** (그냥 문서 읽기만 가능) | **가능** (클릭, 입력, 상태변경) |
| **느낌** | 종이 신문, PDF 문서 | 우리가 아는 웹 앱 |

### Link

- onClick 같은거 쓸려면 “use client” 필요하지만,
- Next.js로 만든 사이트에 접속하면 브라우저는 **아주 기본적인 자바스크립트 뭉치(Bundle)**를 무조건 다운로드
- SPA처럼 부드럽게 화면 이동 가능 (SSR + “use client” 안해도)

**`그니까 JS 계산한 결과값 + HTML → 보냄 → 사용자가 화면 봄 → 그 다음 천천히 JS 로직 보냄`**


- 임베딩벡터 api도 있다.
- 근데 모델 바뀌면 다시 만들어야함