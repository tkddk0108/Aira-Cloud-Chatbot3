# Aira: 클라우드 네이티브 챗봇 플랫폼

Aira는 클라우드 환경에서 프론트엔드, 백엔드, GPT 워커, 인프라(IaC/자동화/배포)까지 통합된 AI 기반 챗봇 서비스입니다. 이 README는 전체 구조와 각 구성 요소의 설치·배포·운영 방법을 한 번에 이해할 수 있도록 안내합니다.

---

## 목차
1. 프로젝트 개요  
2. 디렉터리 구조  
3. 공통 요구사항 및 사전 준비  
4. 프론트엔드(Frontend)  
5. 백엔드(Backend)  
6. GPT 워커(GPT Worker)  
7. 인프라 구성(IaC)  
8. CI/CD 및 GitOps 파이프라인  
9. 보안 및 네트워킹  
10. 모니터링 및 로깅  
11. 배포 예시 워크플로우  
12. Docker 이미지 빌드 & 레지스트리  
13. API 문서화  
14. 버전 관리 및 브랜치 전략  
15. 기타 유틸리티 및 스크립트  
16. 기여 방법(Contributing)  
17. 라이선스(License)

---

## 1. 프로젝트 개요
- AI 챗봇 서비스로, 사용자와의 대화 및 동화 생성 등 다양한 기능 제공
- OpenAI API 호출을 별도 GPT 워커로 분리, SQS(FIFO)로 요청 관리
- 주요 아키텍처: 프론트엔드(React 등), 백엔드(FastAPI), GPT 워커, 데이터베이스(MySQL 등), IaC(Terraform/Ansible/GitOps), CI/CD, 모니터링/로깅

---

## 2. 디렉터리 구조
- FE: 프론트엔드
- BE: 백엔드
- GPT: GPT 워커
- Terraform: 인프라 코드
- Ansible: 서버 자동화
- GitOps: GitOps 배포 설정
- CI: CI 파이프라인 예시
- docs: 추가 문서
- scripts: 유틸리티 스크립트

---

## 3. 공통 요구사항 및 사전 준비
- Node.js, Python 3.9+, Docker, Terraform, Ansible, kubectl, AWS CLI, Git 필요
- AWS 계정 및 IAM 권한, S3/ECR/ECS/EKS/RDS/SQS 등 리소스 준비
- 환경 변수는 .env 파일 또는 Secrets Manager 등으로 관리
- 로컬 테스트는 Docker Compose, FE 개발 서버 등 활용
- 네트워킹(CORS, 보안 그룹 등) 및 브랜치 전략 필요

---

## 4. 프론트엔드(Frontend)
- React 기반, 상태 관리, UI 라이브러리, 라우팅, HTTP 클라이언트 등 사용
- 개발: 의존성 설치, 환경 변수 설정, 개발 서버 실행, API 연동 테스트, 빌드
- 배포: Docker 이미지 생성, 레지스트리 푸시, S3/CloudFront 또는 ECS/EKS 배포, CI/CD 연동

---

## 5. 백엔드(Backend)
- Python FastAPI, Uvicorn, MySQL, SQS, JWT 인증, Docker 등 사용
- 주요 기능: 사용자 인증, GPT 연동 엔드포인트, DB 연동, 오류 처리 등
- 환경 변수: FastAPI, DB, SQS, OpenAI, JWT, 로깅 등 설정
- 개발 및 실행: Docker Compose, 로컬 DB, SQS 대체(LocalStack 등) 활용
- 배포: ECS/EKS, 환경 변수/시크릿 관리, GitOps 연동

---

## 6. GPT 워커(GPT Worker)
- SQS 큐에서 메시지 폴링, OpenAI API 호출, 결과 저장/게시, 재시도 로직 등 구현
- 흐름: 클라이언트 요청 → SQS → 워커 → OpenAI → 결과 저장 → 클라이언트 조회
- 환경 변수: AWS, SQS, OpenAI, 재시도/폴링 설정 등
- 로컬 테스트: Docker Compose, LocalStack 등 활용

---

## 7. 인프라 구성(IaC)
- Terraform: AWS 리소스(VPC, ECS/EKS, RDS, SQS, IAM 등) 자동화
- Ansible: 서버 초기 설정, 서비스 등록, 모니터링 에이전트 설치 등
- GitOps(ArgoCD 등): Git 저장소와 클러스터 상태 동기화, AppOfApps 패턴 등

---

## 8. CI/CD 및 GitOps 파이프라인
- GitHub Actions 등으로 빌드, 테스트, 이미지 푸시, 배포 트리거
- 프론트엔드/백엔드/GPT 워커/인프라 각각 워크플로우 구성
- ECS/EKS/Kubernetes, GitOps(ArgoCD) 자동 배포, 롤백, 환경 분리

---

## 9. 보안 및 네트워킹
- VPC, 서브넷, 보안 그룹, NAT, ALB 등 네트워크 구성
- 인증/인가(JWT, OAuth2), 시크릿 관리(Secrets Manager 등)
- CORS, TLS/SSL, IAM 최소 권한, 로깅 민감 정보 필터링 등

---

## 10. 모니터링 및 로깅
- Prometheus, Grafana, CloudWatch 등으로 메트릭/로그 수집 및 대시보드 구성
- 알림(Alarm, Slack, 이메일 등), 트레이싱(OpenTelemetry 등), 로깅 레벨/마스킹

---

## 11. 배포 예시 워크플로우
- 인프라 준비(Terraform)
- CI/CD 설정 및 환경 변수 관리
- FE/BE/GPT 워커 빌드 및 배포
- DNS(Route53), 모니터링, 테스트, 운영 및 보안 점검

---

## 12. Docker 이미지 빌드 & 레지스트리
- ECR 리포지토리 생성, AWS CLI 로그인, 이미지 빌드/태깅/푸시
- 버전 태깅, 멀티스테이지 빌드, 로컬 개발은 Docker Compose 활용

---

## 13. API 문서화
- FastAPI의 /docs, /redoc 엔드포인트 활용
- API 스펙 공유, Postman 컬렉션 등 필요시 추가

---

## 14. 버전 관리 및 브랜치 전략
- main/dev/feature/hotfix 브랜치, 커밋 메시지 규칙, PR 리뷰, 태그 릴리스 등

---

## 15. 기타 유틸리티 및 스크립트
- 배포/테스트/마이그레이션/로컬 시작 스크립트, Lint/Formatter, Pre-commit 훅 등

---

## 16. 기여 방법(Contributing)
- 이슈 작성, 브랜치 생성, 코드 작성/테스트, PR 제출/리뷰/머지, 문서 업데이트 등

---

## 17. 라이선스(License)
- 프로젝트 라이선스(MIT 등) 명시

---

## 부록: 자주 묻는 질문(FAQ)
- SQS 없이 로컬 테스트: LocalStack, 임시 메모리 큐 등 활용
- OpenAI API 호출 실패: 네트워크/인증 오류, 재시도/백오프, 로그 확인
- GPT 워커 동시성: 인스턴스 수, 스레드/비동기 처리 등 조절
- Terraform 권한 오류: IAM, State 파일, S3/DynamoDB 락 점검
- Ansible 연결 에러: SSH 키, 호스트/IP, 방화벽 설정 점검

---

이 README.md를 프로젝트 루트에 두고, 각 하위 디렉터리(FE, BE, GPT, Terraform 등)에도 별도 README를 작성해 주세요. 실제 환경에 맞게 경로, 명령어, 환경 변수 등을 수정해 사용하시면 됩니다.
