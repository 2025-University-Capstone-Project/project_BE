# ⚾️ Y.P.T (Your Pitch Ticket) - BE
> **Spring Boot 기반의 안정적인 야구 팬 커뮤니티 백엔드 시스템**

Y.P.T 백엔드는 사용자 인증, 데이터 영속성 관리, 대용량 이미지 처리 및 서드파티 API 연동을 담당하는 핵심 엔진입니다. 확장성 있는 레이어드 아키텍처(Layered Architecture)를 채택하여 유지보수성을 높였으며, JWT 기반의 보안 시스템을 구축했습니다.

---

## 🛠 Tech Stack

- **Lanuage & Framework**: Java 17, Spring Boot 3.3.x
- **Security**: Spring Security, JWT (JSON Web Token)
- **Database**: MySQL, Spring Data JPA
- **Cloud Storage**: AWS S3 (Diary 이미지 및 프로필 관리)
- **OAuth**: Kakao Login API 연동
- **API Docs**: SpringDoc OpenAPI (Swagger UI)
- **Build Tool**: Gradle

---

## 🚀 Key Features (BE Focus)

### 1. Security & Authentication (보안 및 인증)
- **JWT 기반 무상태(Stateless) 인증**: `JwtFilter`와 `JwtUtil`을 커스텀 구현하여 토큰 기반의 안전한 인증 환경을 구축했습니다.
- **Spring Security**: 보안 설정을 통해 역할 기반의 접근 제어(RBAC) 및 CORS 정책을 중앙 집중식으로 관리합니다.

### 2. AWS S3 Media Handling (미디어 처리)
- **S3 Service**: 직관 일지의 사진 업로드 및 사용자 프로필 이미지 처리를 위해 `aws-java-sdk-s3`를 연동했습니다.
- **ImageController**: 파일 업로드 시 파일 유효성 검증 및 S3 버킷 관리 로직을 구현했습니다.

### 3. Kakao OAuth Integration (서드파티 연동)
- **외부 API 통신**: `WebClient`를 활용하여 카카오 인증 서버와 통신하고, 액세스 토큰 획득 및 유저 정보 매핑 로직을 추상화했습니다.
- **Social Service**: 소셜 로그인 유저와 로컬 DB 유저를 통합 관리하는 로직을 구현했습니다.

### 4. Quiz & Point System (비즈니스 로직)
- **점수 관리**: 사용자의 승부 예측 성공 및 퀴즈 정답 여부에 따른 실시간 포인트 적립 및 랭킹 정산 API를 설계했습니다.
- **JPA Optimization**: 불필요한 쿼리를 방지하기 위해 Fetch Join 및 DTO 매핑을 활용한 최적화된 데이터 조회를 수행합니다.

---

## 📁 Project Architecture

```text
java/com/baseballweb/auth/
├── config/          # Security, Web, S3 등 전역 설정
├── controller/      # REST API 엔드포인트 설계
├── service/         # 비즈니스 로직 및 트랜잭션 관리
├── repository/      # Spring Data JPA를 이용한 데이터 접근
├── model/           # Entity 정의 (Domain)
├── dto/             # 계층 간 데이터 전송을 위한 객체
└── jwt/             # 토큰 생성 및 필터링 핵심 로직
```

---

## 💡 Technical Excellence (Interview Point)

### ✔️ 확장 가능한 이미지 업로드 설계
단순 업로드를 넘어, `S3Service`를 인터페이스화하여 향후 로컬 저장소나 다른 클라우드(GCP, Azure)로 쉽게 교체할 수 있도록 확장성을 고려해 설계했습니다.

### ✔️ 예외 처리 및 유효성 검증
`@Valid` 어노테이션과 커스텀 예외 처리를 통해 클라이언트의 잘못된 요청에 대해 일관된 에러 응답 형식을 유지하도록 했습니다.

### ✔️ Swagger UI를 통한 API 명세화
협업의 효율성을 높이기 위해 모든 API 엔드포인트에 Swagger(OpenAPI 3.0)를 적용하여 프론트엔드 개발자와의 명확한 통신 규약을 확립했습니다.