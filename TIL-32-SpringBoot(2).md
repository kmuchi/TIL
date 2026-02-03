26.02.03

### DTO (Data Transfer Object)

> 데이터를 실어 나르는 객체 , 로직을 갖지 않는 순수한 데이터 컨테이너
> 
- Django에서 Serializer가 DTO 역할
- **Spring:** `Entity` (DB) ↔ `DTO` (전송)
- **Django:** `Model` (DB) ↔ `Serializer` (전송)

사용자 입력
↓
DTO/Serializer (검증 + 필터링)
↓
Entity/Model (ORM 객체)
↓
ORM이 자동으로 SQL 생성
↓
외부 MySQL에 저장

### Prisma

- nextjs ORM 라이브러리

### Bearer

> 티켓 소지한 사람
> 

## 정리

| 어노테이션 | null | "" | "  " | 사용 상황 |
| --- | --- | --- | --- | --- |
| **@NotNull** | ❌ | ✅ | ✅ | 숫자, Boolean 등 |
| **@NotEmpty** | ❌ | ❌ | ✅ | List, Array |
| **@NotBlank** | ❌ | ❌ | ❌ | **String (제일 많이 씀)** |

| **HTTP Method** | **용도** |
| --- | --- |
| `PUT` | 리소스 전체 교체 |
| `PATCH` | 리소스 일부만 수정 ✅ |

프론트엔드 요청
↓
PATCH /companies/{companyId}/culture-fit
↓
┌────────────────────────────────────────┐
│ 1. companyId로 DB에서 회사 찾기        │
│    → SELECT * FROM companies           │
│      WHERE company_id = {companyId}    │
│                                         │
│ 2. 찾은 Entity의 cultureFit만 수정     │
│    company.setCultureFit("새로운 값")   │
│                                         │
│ 3. 저장 (JPA가 자동으로 UPDATE 실행)   │
│    → UPDATE companies                  │
│      SET culture_fit = '새로운 값'     │
│      WHERE company_id = {companyId}    │
└────────────────────────────────────────┘

## 실행 흐름 예시

```
사용자 요청: "우리 회사 조직문화 '수평적 소통' 으로 변경"
  ↓
Controller에서 updateCultureFit() 호출
  ↓
1. 로그인 정보에서 회사 ID 추출: "abc-123-def"
  ↓
2. 권한 검증: "이 사람이 abc-123-def 회사 관리자 맞나?"
  ↓
3. DB 조회: "SELECT * FROM company WHERE company_id = 'abc-123-def'"
  ↓
4. Entity 업데이트: company.cultureFit = "수평적 소통"
  ↓
5. DB 저장: "UPDATE company SET culture_fit = '수평적 소통' WHERE ..."
  ↓
완료!
```

**@Transactional**

- DB 작업이 전부 성공하거나 전부 실패하도록 보장
- 중간에 에러 나면 자동 롤백