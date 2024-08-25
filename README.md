# panama-canal

- 프록시 설정의 복잡함을 덜어주는, 프론트엔드 개발자를 위한 간편 프록시 및 어드민 환경 서비스


## Projects

아래는 각 컴포넌트별로 기술 스택과 역할을 정리한 내용입니다.

### 1. **Keycloak (IDP)**
   - **기술 스택**: 
     - **Container**: Docker
     - **Identity Provider (IDP)**: Keycloak
   - **역할**:
     - 사용자 인증 및 권한 관리 기능을 제공하는 IDP(Identity Provider) 역할.
     - OAuth2, OpenID Connect, SAML 등 다양한 인증 프로토콜을 지원.
     - 사용자의 로그인, 로그아웃, 세션 관리, 그리고 역할 기반 접근 제어를 관리.
     - 백엔드 및 프론트엔드와의 통합을 통해 인증 및 권한 부여를 중앙에서 관리.

### 2. **Backend (Admin API Server)**
   - **기술 스택**:
     - **Language**: Kotlin
     - **Framework**: Spring Boot
     - **Database**: 선택에 따라 SQL (MySQL, PostgreSQL) 또는 NoSQL (MongoDB)
     - **Security**: Spring Security OAuth2 Resource Server (Keycloak 연동)
   - **역할**:
     - 어드민 기능을 위한 API를 제공하는 서버.
     - 사용자 관리, 프록시 설정 등록 등 다양한 어드민 기능을 위한 비즈니스 로직을 처리.
     - Keycloak과 연동하여 인증 및 권한 검증을 수행.
     - 프론트엔드에서 요청된 데이터를 처리하고 응답.

### 3. **Gateway (Proxy Gateway Server)**
   - **기술 스택**:
     - **Language**: Java/Kotlin
     - **Framework**: Spring Cloud Gateway
    
   - **역할**:
     - 등록된 API path들과 시크릿 혹은 별도 헤더들로 프록시를 동적으로 설정
     - 요청 라우팅, 부하 분산, 요청 필터링 및 보안 정책 적용.
     - API 게이트웨이 패턴을 구현.

### 4. **Frontend (Admin UI)**
   - **기술 스택**:
     - **Language**: JavaScript
     - **Framework**: Vue.js
     - **UI Library**: Admin One UI
     - **State Management**: Vuex
     - **Build Tool**: Webpack, Vite
   - **역할**:
     - 어드민 사용자들을 위한 인터페이스를 제공.
     - 백엔드에서 제공하는 API를 사용하여 사용자 관리, 프록시 및 카테고리 설정 등록
     - Keycloak과 연동하여 사용자 인증 및 세션 관리.

## Architecture Overview
![image](https://github.com/user-attachments/assets/398e846f-24aa-413f-9488-6d73f252bea6)


## Key Features

### 1. 카테고리 등록
- 사용하는 OPEN API 종류별로 카테고리를 등록해 관리할 수 있습니다.
- 항상 API 제공자 사이트에 접속할 필요없이 어떤 API들을 내가 사용중인지 알 수 있습니다.

### 2. 프록시 등록
- 프록시서버 구축에 익숙하지 않더라도 UI 를 기반으로 손쉽게 프록시 uri path와 목적지 도메인을 등록해 프록시를 설정할 수 있습니다.

### 3. 시크릿 키 관리
- OPEN API 사용에 필요한 시크릿 키들을 대칭형 암호화를 통해 안전하게 데이터베이스에서 관리할 수 있습니다.

### 4. 프록시를 통한 API 인증
- HEADER, PARAMETER 등 프록시에서 API 인증을 대신 수행해, 매번 client 측에서 secret을 관리할 필요가 없습니다.
