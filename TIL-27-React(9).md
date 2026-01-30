### export default function

> 리액트19 권장방식
> 

```jsx
// 방식 1: 함수 정의와 동시에 export
export default function MyComponent() {
  return <div>Hello</div>
}

// 방식 2: 함수 정의 후 나중에 export
function MyComponent() {
  return <div>Hello</div>
}

export default MyComponent
```

### 반응형 웹

> 브라우저의 뷰포트(Viewport) 크기를 바탕으로 작동
> 
- @media CSS에서 미디어 쿼리 문법을 사용해 조건을 건다.
- 모바일 퍼스트
- **터치 피드백:** 버튼을 눌렀을 때 살짝 들어가는 애니메이션 (`framer-motion` 라이브러리 추천).
- **스켈레톤 UI:** 로딩 중에 흰 화면 대신 뼈대 보여주기.
- **페이지 전환 효과:** 화면이 넘어갈 때 딱딱 끊기지 않고 부드럽게 넘어가기.
- **토스트 메시지:** 저장했을 때 "저장되었습니다"가 예쁘게 떴다 사라지기.
- **UI Library:** **Radix UI** 또는 **Shadcn/ui**
- **Animation:** **Framer Motion**
- **Icon:** **Lucide React**

### clamp()

> CSS 자동크기 조절 함수
> 
- **최소값(Min), 권장값(Ideal), 최대값(Max)** 세 가지를 정해두고, **상황에 맞춰 그 사이에서 유연하게 변하는** 최신 문법

### 회원가입

| 서비스 | 가격 | 특징 |
| --- | --- | --- |
| NHN KCP | 건당 50~100원 | 대기업 많이 씀 |
| 다날 | 건당 50~80원 | 중소기업 많이 씀 |
| 나이스정보통신 | 건당 50~100원 | 금융권 많이 씀 |
- 이메일 인증

### 프록시

> Ngnix, AWS ALB 등 중계소 역할
> 

1. 보안 (문지기) 역할
2. 부하 분산 : 프록시가 여러서버에 분산해서 보냄
3. HTTPS 처리 : 프록시가 암호화된 껍질을 까고(복호화) → 뒤에 있는 서버에서 순수한 데이터(http)만 넘겨줌
4. 캐싱 : 똑같은 이미지 기억해둔 데이터 바로 보내줌

### HTTPS

> http + SSL/TLS 암호화 기술
> 
- 브라우저가 데이터를 보내기전에 암호화(난수표)로 바꿔서 보냄

**근데 왜 HTTPS처리는 프록시가 함?**

→ 암호화, 복호화 → 수학계산 복잡 → CPU 많이씀

⇒ 서버가 직접하게되면 ⇒ 느려짐 ⇒ 그래서 프록시가 앞에서 ⇒ 막노동(암호풀기) 대신해줌