### JDK

- Java Development Kit
- javac(컴파일러) : 코드 → 기계어 번역
- java(jvm, 실행기)
- 라이브러리
- 익스텐션 역할 - 내컴퓨터 java - vs code 연결선 역할

### Gradle

> pip + Venv + manage.py
> 

### 스프링부트 파일구조

src
└── main
├── java
│   └── com.example.demo  (패키지 루트)
│       ├── DemoApplication.java  (메인 실행 파일: [manage.py](http://manage.py/) 역할)
│       │
│       ├── controller        (URL 요청 받는 곳: Django [views.py](http://views.py/))
│       ├── service           (비즈니스 로직: Django에는 없는 계층)
│       ├── repository        (DB 쿼리 날리는 곳: Django ORM)
│       ├── domain (or entity)(DB 테이블 정의: Django [models.py](http://models.py/))
│       ├── dto               (데이터 전달 객체: Django Serializer 비슷)
│       └── config            (설정 파일: Django [settings.py](http://settings.py/) 일부)
│
└── resources
├── static            (css, js, images)
├── templates         (html 파일: React 쓰면 안 씀)
└── application.yml   (환경 설정: 포트, DB 비번 등)

### 핵심 폴더

| **스프링 폴더** | **역할** | **장고(Django) 비교** | **설명** |
| --- | --- | --- | --- |
| **controller** | **웨이터** | `views.py` (함수/클래스) | 손님(React)의 주문(URL)을 받고, 서빙(응답)하는 역할. |
| **service** | **요리사** | (보통 views 안에 짬) | 실제 복잡한 요리(로직)를 하는 곳. 트랜잭션 관리. |
| **repository** | **창고지기** | `.objects.all()` (ORM) | DB에서 재료(데이터)를 꺼내오는 역할. SQL 담당. |
| **domain** | **재료 명세서** | `models.py` | DB 테이블 그 자체. (`@Entity` 붙음) |
| **dto** | **서빙용 접시** | `serializers.py` | Entity(날것)를 그대로 주지 않고, 필요한 것만 담는 객체. |

`Controller` -> `Service` -> `Repository`

### 스프링(자바) .env

- application-local.yml 이게 표준임
- **application.yml / application.properties** - 기본 설정
- **application-{profile}.yml** - 환경별 설정

### Docker

`docker-compose -f docker-compose.dev.yml up -d`