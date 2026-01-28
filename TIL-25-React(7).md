### index.css

> 프로젝트 전체에 적용되는 css
> 

### @theme

> css파일 @theme 블록안에 변수선언만 하면 → Tailwind가 알아서 클래스 만들어줌
> 
- index.css에 정의하면 됨
- (기존방식 v3는 tailwind.config.js → (v4 이후) → index.css에서)
- 

### npm install

- 이미 있는 패키지 → 건드리지 않음
- 새로 추가된 패키지 → 다운로드
- 버전 바뀐 패키지 → 업데이트
- 삭제된 패키지 → 그대로 남음 (직접 삭제 필요)

### 조건부 렌더링

> swtich문 사용한 코드
> 

```jsx
const renderPage = () => {
  // currentPage 상태값에 따라 다른 컴포넌트 보여주기
  switch (currentPage) {
    case 'simulation':
      return <SimulationPage />;  // 시뮬레이션 페이지
    case 'chat':
      return <div>채팅 페이지 (준비중)</div>;  // 임시 div
    case 'vocabulary':
        return <MyVocabPage />;
```

- 페이지전환용으로는 안씀 (그냥 빠르게 SPA 구현용으로)
- 로그인여부 / 로딩상태 / 에러처리 등등에서 많이 사용함

### switch문

- 상태값이 여러개 일때 (if문, 삼항연산자 느낌으로 씀)  (자주안씀)
- 근데 실무 ⇒ 객체 매핑을 더 많이 씀

```jsx
// ✅ 객체 매핑 (더 선호)
const STATUS_BADGE = {
  pending: <Badge color="yellow">대기</Badge>,
  paid: <Badge color="green">완료</Badge>,
  cancelled: <Badge color="red">취소</Badge>
};
```

### Outlet

> 장고 템플릿 상속이랑 비슷한 개념
> 
- 각 페이지마다 → 컴포넌트 불러와서 조립 ⇒ 중복
- 메인 Layout에 구멍 뚫어놓음 → 그 구멍에 각각 파일이 들어가는 구조

**장점**

1. Outlet 안쓰고 페이지마다 <Sidebar/> 쓰면?
    - 페이지 이동시 → 사이드바 새로고침 (UX 저하)
2. 복붙 줄이기
3. 코드 깔끔함

**안쓰는 경우**

- 로그인 페이지 : (헤더/사이드바 아예없어야 함)
- 랜딩페이지
- 대시보드

### 호버 리프트 이펙트 (Hover Lift Effect)

> 마우스 위로 가면 → 위로 붕 뜨면서 → 그림자 진해지고 넓어지는 이펙
> 
- css로 구현하면 됨
- `cursor-pointer hover:-translate-y-1 hover:shadow-lg`

### 달력(Calendar)

> `import { DayPicker } from "react-day-picker"`
> 

shadcn/ui의 캘린더(`react-day-picker` 기반)

⇒ 프론트엔드(브라우저)에서 실시간으로 계산

- DB에서 달력 가져오는것보다 훨씬 더 빠르다.

### Select (셀렉트) = 드롭다운 (Dropdown)

> 클릭하면 목록이 툭 떨어져서 하나 고르는 것
> 
- **Select:** 화면 맨 아래에 있는 걸 눌렀을 때, 목록이 화면 밖으로 잘리면 안 되니까 **알아서 위로 솟구쳐야** 하는데, 그 계산이 귀찮

### Accordion (아코디언)

> 누르면 내용이 스르륵 펼쳐지는 목록
> 
- 열릴 때 뚝! 하고 나오는 게 아니라, **부드럽게 스르륵~** 나오게 애니메이션 넣기가 CSS만으로는 까다로

⇒ 그래서 라이브러리 쓴다  (복잡한거 가져다가 → CSS만 바꿈)

### Popover(팝오버)

> 아이콘 클릭 → 화면뜸 (다시클릭 or X 누르면 닫힘)
> 

### Tooltip(툴팁)

> 마우스 살짝 올리면(Hover)뜸
> 

### Modla(모달) / Dialog(다이얼로그)

> 화면 정중앙에 뜨면서 배경이 어두워짐
>