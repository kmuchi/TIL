### MobaXterm

> 윈도우 → 리눅스 원격서버 접속 관리 / 터미널 프로그램
> 
1. 주요 기능
    - SSH  + 다양한 프로토콜 지원
    - GUI 지원
- ec2(우분투) → 윈도우에서 접근(관리자 계정) → 리눅스 명령어
- **PuTTY** = Windows에서 SSH 접속할 때 쓰는 무료 프로그램
**WinSCP** = Windows ↔ Linux 서버 간 **파일 전송** 프로그램

### SSH (Secure Shell)

> 원격 컴퓨터 안전하게 접속 하는 기술
> 

Windows PC (클라이언트 ) —- SSH  — EC2 (서버)

**SSH 인증 방식**

1. 비밀번호: ID/PW로 로그인 (보안 약함)
2. 공개키/개인키: .pem 파일로 로그인

### Ubuntu

> Linux 기반 운영체제
> 
- git bash = 윈도우 환경에서 리눅스 bash 흉내낸 프로글매
- 명령어 거의 같음

### Ec2 + MobaXterm + Docker + Jenkins + Nginx

1. MobaXterm → EC2 접속
2. Docker 설치
3. Jnkins 설치 및 설정 → 깃허브 연결 → 자동배포 (CI/CD)
4. Nginx 설치 및 연결 (리버스프록시)

### docker

- 레이어공유 + 캐싱
- 레이어공유 (같은 python 3.11 버전 쓰는 사용자 끼리 레이어 공유) → 100명이 써도 1개로 100명분가능
- 레이어 캐싱 - 안바뀌면 캐시 재활용 + 바뀐부분만 빌드

### MobaXterm 실습

```jsx
# 서버 정보 확인
uname -a
df -h          # 디스크 용량
free -m        # 메모리

# docker
docker run hello-world

```

사용자 → :80/:443 (nginx) → 프론트엔드 요청 → protalk_frontend
→ API 요청 (/api) → protalk_backend → MySQL/Redis


### 멀티 스테이지 빌드

> 도커 이미지 효율화
> 
- 실행할 땐 필요없는, 소스 코드 ,빌드 도구, 컴파일러까지 다들어있는 상태
- 다 가져와서 빌드 (무거움) → 가벼운 새 도커 이미지 → 완성된것만  넣음

- 개발할때 Node.js 이미지 전체 사용 (약 800MB)
- 멀티스테이지 빌드
    - 빌드해서 가벼운 build 폴더 생성
    - 약 20MB

**멀티스테이지 빌드란?**

**"빌드할 때 썼던 무거운 도구들은 다 갖다 버리고, 실행에 필요한 결과물만 챙겨서 가볍게 만드는 기술"**


PlayWright MCP
### 1. 로그인/로그아웃 - PASS

| 항목 | 결과 |
| --- | --- |
| 이메일/비밀번호 입력 | 정상 |
| 로그인 후 리다이렉트 | 정상 (`/app/simulation`) |
| 사용자 정보 표시 | 정상 (테스트유저03, 36.5°C) |
| 로그아웃 | 정상 (랜딩 페이지로 복귀) |

### 2. 시뮬레이션 - PARTIAL

| 항목 | 결과 |
| --- | --- |
| 시뮬레이션 리스트 표시 | 정상 (10개 시나리오) |
| 카테고리 필터 (대학생활/신입사원/회사생활) | 정상 |
| 테마 변경 (기본/N사/G사/M사) | 정상 |
| 메일 폼 입력 (받는사람, 제목, 본문) | 정상 |
| 받는사람 태그 입력 (Enter 확정) | 정상 |
| **메일 제출** | **FAIL - 500 Internal Server Error** (`/api/v1/simulations/attempts`) |