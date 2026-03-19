### 에러 트래킹 서비스

**error.tsx**

```jsx
console.error(error) // 사용자 브라우저에서만 보임

// Sentry 연동하면
Sentry.captureException(error) // Sentry 대시보드에 자동 수집
```

- 에러 모니터링

### 에러로그 보기

```jsx
return (
  <main className="mx-auto flex max-w-lg flex-col items-center gap-4 p-4 pt-20">
    <p className="text-sm text-muted-foreground">데이터를 불러오는 중 오류가 발생했습니다.</p>
    {/* 이 부분 추가 */}
    {process.env.NODE_ENV === 'development' && (
      <pre className="text-xs text-destructive">{error.message}</pre>
    )}
    <Button onClick={reset} variant="outline">
      다시 시도
    </Button>
  </main>
)
```

- `npm run dev` 돌릴 때만 에러메시지 보임 (프로덕션 빌드)에서는 안보임

### utils

> 공통 작은 유틸 함수 모아둠
> 
- 컴포넌트의 주된 목적은 UI를 그리는 것
- utils는 코드재사용 목적 함수

**언제씀?**

- State 나 생명주기 의존 x → 순수함수 일때
1. **데이터 포맷팅** : 날짜, 시간, 통화, 전화번호 → 사용자가 보기 쉬운 형태로 변환
2. **데이터 파싱 및 가공** : API 받아온 객체 → 프론트에서 쓰기 쉽게 다듬을 때
3. **정규식 및 유효성 검사** : 이메일 형식 확인, 비밀번호 규칙 검사 등
4. **공통 비지니스 로직** : 도메인 특화된 계산식

**굳이?**

- 추상화의 딜레마 → 코드 중복 보다 나쁜것이 잘못된 추상화
- 코드길이 x → (비지니스 룰 → 한곳에서 관리하기 위해 뺴는것에 가깝다)

### MSW (Mock Service Worker)란?

> 브라우저 안에 숨어있는 가짜 백엔드 서버(스파이)
> 
- 프론트 → 백엔드 API 요청 ( MSW가 중간에서 요청 가로챔)
- Mock Data → 프론트에서 돌려

**1단계: `handlers` (어떤 요청을 가로채서, 어떤 가짜 데이터를 줄지 정의)**

```jsx
import { http, HttpResponse } from 'msw'
import { mockSchedules, mockPortfolio } from '@/lib/mocks/home'

export const handlers = [
  // 1. 프론트엔드에서 '/api/ipo/weekly' 주소로 GET 요청을 보내면...
  http.get('/api/ipo/weekly', () => {
    // 진짜 서버 대신, 미리 만들어둔 'mockSchedules' 데이터를 JSON 형태로 던져줘라!
    return HttpResponse.json(mockSchedules)
  }),

  // 2. 프론트엔드에서 '/api/portfolio/report' 주소로 GET 요청을 보내면...
  http.get('/api/portfolio/report', () => {
    // 'mockPortfolio' 데이터를 던져줘라!
    return HttpResponse.json(mockPortfolio)
  }),
]
```

**2단계: `worker` (가짜 서버 작동시키기)**

```jsx
import { setupWorker } from 'msw/browser'
import { handlers } from './handlers'

// 위에서 만든 대본(handlers)을 서비스 워커(worker)에게 쥐여주고 세팅합니다.
export const worker = setupWorker(...handlers)
```

위에서 만든 시나리오를 바탕으로 **실제로 브라우저에서 요청을 가로챌 요원(Worker)을 생성**하는 코드입니다. 나중에 앱의 최상단(주로 `_app.tsx`나 `layout.tsx` 등)에서 `worker.start()`를 호출해주면, 그때부터 이 요원이 활동을 시작하며 네트워크 요청을 가로채게 됩니다.

### mockServiceWorker.js

> 자동생성 세팅 파일
>