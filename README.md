# ☁️ Aira-3: IaaS 클라우드 운영 자동화

> 기간: 2025.02.20 ~ 2025.03.24  
> EKS 기반 인프라 코드화(IaC)와 운영 자동화로 **클라우드 운영 효율성 및 안정성 향상**을 목표로 한 프로젝트

<img width="12620" height="7220" alt="image" src="https://github.com/user-attachments/assets/363e3853-f2b2-4d0e-a774-bef2caa0d568" />
<img width="12200" height="8060" alt="image" src="https://github.com/user-attachments/assets/6427badf-9e7f-4a2c-a554-beadec8fcd4b" />
<img width="1871" height="1071" alt="image" src="https://github.com/user-attachments/assets/4cac08cf-1c64-4c78-9064-daea250e2fd0" />


---

## 🔧 프로젝트 개요

Aira-3는 OpenAI 기반 챗봇 서비스 **Aira**의 세 번째 고도화 프로젝트로,  
**반복적인 클라우드 운영 작업을 자동화**하고 **트래픽 탄력성 확보**, **비용 최적화**, **백업/복원 자동화**까지 포함하는 **운영 자동화 체계 구축**에 중점을 두었습니다.

---

## 🛠️ 주요 기술 스택 및 도구

| 항목 | 사용 기술 |
|------|-----------|
| IaC 구성 | Terraform, Ansible |
| 클러스터 환경 | AWS EKS, Kubernetes |
| CI/CD 자동화 | GitHub Actions, ArgoCD |
| 모니터링 | Prometheus, Grafana, CloudWatch, Cost Explorer |
| 트래픽 자동 확장 | Horizontal Pod Autoscaler (HPA) |
| 백업/복원 자동화 | Kubernetes CronJob |
| 도메인 관리 | Route53 (예: kopmorning.com) |

---

## 🗂️ 인프라 구성 요약

- **Terraform 기반 IaC 구성**
  - EKS 클러스터, VPC, 노드 그룹 등 인프라 코드화
- **Ansible로 Kubernetes 설정 자동화**
  - ArgoCD, Monitoring, DB 네임스페이스 구성 자동화
- **ArgoCD + GitOps 기반 자동 배포 시스템**
  - GitHub Actions → ArgoCD → K8s 앱 실시간 배포 동기화
- **운영 자동화 및 모니터링**
  - Prometheus + Grafana 리소스 시각화
  - CloudWatch + Cost Explorer로 예산 초과 알림
- **트래픽 탄력 대응**
  - HPA로 CPU 사용률에 따라 Pod 수 자동 확장
- **DB 백업 및 복원 자동화**
  - CronJob으로 주기적 DB 백업 및 복구 프로세스 구현

---

## ✅ 성과

- **완전 자동화된 GitOps 운영 체계** 구축 (ArgoCD + GitHub Actions)
- **운영비용 시각화 및 예산 초과 탐지 자동화**
- **트래픽 자동 확장 설정**으로 부하 대응 능력 향상
- **주기적 DB 백업 자동화 및 복구 시나리오 문서화**
- **Infra as Code 기반 유지보수 가능 구조 완성**

---

## 📂 주요 역할 및 기여

| 구분 | 상세 내용 |
|------|-----------|
| Ansible 자동화 구성 | ArgoCD, DB, Monitoring 네임스페이스 및 설정파일 코드화 및 운영 반영 |
| ArgoCD 운영 구성 | Git 연동, 앱 배포 자동 동기화 및 실시간 UI 설정 |
| 모니터링 및 비용 최적화 | Prometheus + Grafana로 대시보드 구축, CloudWatch & Cost Explorer로 자원 예산 관리 |
| CI/CD 파이프라인 설계 | GitHub Actions를 활용한 자동 빌드, 테스트, 배포 파이프라인 구축 |
| DB 자동 백업 문서화 | CronJob 기반 주기 백업 및 복구 시나리오 설계 및 문서 정리 |

---

## 🔗 관련 링크

- [📎 발표 자료 (Google Drive)](https://drive.google.com/file/d/1bYXmLwZJiuwLVtq1yluauUZVwtgd4ewX/view?usp=drive_link)

---

## 📌 향후 개선 방향

- ArgoCD Notifications로 슬랙 알림 설정
- S3를 활용한 백업 파일 버전 관리 및 장기 보관 전략 도입
- Pod 단위 리소스 자동 최적화 추천 시스템 도입 검토

---

> Aira-3는 운영 자동화를 실전에서 구현하며, IaC와 GitOps, 모니터링, 예산 관리까지 포함한 종합적인 클라우드 운영 체계를 구축한 프로젝트입니다.
