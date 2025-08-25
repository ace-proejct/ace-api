# 영어 학습 앱 개발 스타일 가이드

## 프로젝트 개요
- **목표**: OPIC 영어 학습을 위한 웹/앱 플랫폼
- **기술 스택**: Spring Boot + React/Next.js + PostgreSQL(pgvector) + Flutter
- **주요 기능**: STT/TTS, Gemini API 연동, 대화 기록 관리

## 코드 리뷰 중점 사항

### 1. 보안 (최우선)
- **API 키 관리**: 환경변수 사용, 하드코딩 금지
- **사용자 토큰**: JWT 만료시간 설정, 안전한 저장
- **입력 검증**: 모든 사용자 입력 sanitization
- **CORS 설정**: 개발/운영 환경 분리

### 2. 성능 최적화
- **데이터베이스**:
  - N+1 쿼리 방지
  - 인덱스 활용
  - pgvector 쿼리 최적화
- **API 호출**:
  - Gemini API 레이트 리미팅 준수
  - 실패시 재시도 로직
  - 응답 캐싱 활용
- **파일 처리**:
  - 음성 파일 크기 제한
  - 스트리밍 처리

### 3. 에러 핸들링
- **네트워크 오류**: 타임아웃 설정, 사용자 친화적 메시지
- **API 장애**: 폴백 메커니즘
- **파일 업로드**: 형식/크기 검증
- **음성 인식 실패**: 재시도 옵션 제공

### 4. 코드 품질
- **Spring Boot**:
  - `@Service`, `@Repository` 레이어 분리
  - `@Transactional` 적절한 사용
  - Exception 커스텀 클래스 활용
- **React/TypeScript**:
  - Props 타입 정의
  - Custom Hook 활용
  - 컴포넌트 재사용성
  - 메모리 누수 방지 (useEffect cleanup)

### 5. 접근성 (a11y)
- **음성 UI**: 시각 장애인을 위한 텍스트 대체
- **키보드 네비게이션**: 모든 기능 접근 가능
- **ARIA 라벨**: 스크린 리더 지원
- **색상 대비**: WCAG 가이드라인 준수

## 명명 규칙
- **Java**: camelCase, 클래스는 PascalCase
- **Database**: snake_case (user_conversation, audio_file)
- **API 엔드포인트**: kebab-case (/api/voice-analysis)
- **React**: PascalCase (VoiceRecorder.tsx)

## 금지 사항
- `console.log()` 프로덕션 코드에 남겨두기
- 하드코딩된 API 키나 비밀번호
- `any` 타입 남발 (TypeScript)
- 에러 무시 (`catch` 블록 비우기)
- 긴 메서드 (20줄 초과시 분할 권장)

## 권장 사항
- 단위 테스트 작성 (특히 API 연동 부분)
- 로깅 레벨 적절히 설정
- Docker 환경 설정 문서화
- README에 개발 환경 셋업 가이드 포함
- 커밋 메시지 컨벤션 준수

## 리뷰 톤
- 건설적이고 친근한 피드백
- 구체적인 개선 방안 제시
- 학습 도움이 되는 참고 자료 링크
- 긍정적인 부분도 언급