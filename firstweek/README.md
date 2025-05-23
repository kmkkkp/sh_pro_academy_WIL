# 금융 기초 지식과 DevOps, 클라우드란?

## 🏦 1. 금융 기초 지식

### ✅ 증권사의 역할
- 자금의 중개: 매수자-매도자 연결  
- 유동성 공급: 시장 활성화  
- 기업금융: IPO, 유상증자 등  
- 자산관리: 고객 맞춤 포트폴리오  
- 기관투자자 서비스 및 자기자본 운용  

### ✅ 금리란 무엇인가?
- 돈의 가격 (기준금리: 한국은행이 설정)  
- 금리 ↑ → 소비 ↓, 대출 ↓ → 경기 둔화  
- 금리 ↓ → 소비 ↑, 투자 ↑ → 경기 자극  
- **금리와 채권가격은 반비례**

### ✅ 투자 판단 지표

| 지표  | 설명 |
|-------|------|
| EPS   | 주당순이익 (당기순이익 / 주식수) |
| PER   | 주가 / EPS (저PER: 저평가 가능성) |
| PBR   | 주가 / 순자산 (1보다 작으면 저평가 가능성) |
| PSR   | 주가 / 매출액 (적자 기업에 유용) |

### ✅ 서브프라임 모기지 사태 (2008)
- 신용 낮은 사람에 대출 → 부실채권 → 파생상품으로 전이  
- 금융기관 간 신뢰 붕괴  
- 교훈: "과도한 레버리지와 불투명한 구조는 위험하다"


---

## 🧠 2. Git 관련 핵심 개념 정리

### ✅ Git 기본 흐름
```bash
Working Directory → Stage(add) → Commit → Repository
```

### ✅ 주요 명령 및 개념
- `commit`: 스냅샷 저장 (메시지 규칙 중요)  
- `merge`: 브랜치 병합 (3-way merge 충돌 가능)
### ✅ 안 써보던 내용 
> https://learngitbranching.js.org/?locale=ko 연습해보자
- `cherry-pick`: 원하는 commit만 선택 병합  
- `rebase`: 브랜치 이력 정리, 충돌시 ours/theirs 주의  
- `revert`: 특정 commit 취소  
- **3-way merge**: 같은 라인 변경 충돌 시  
- **ours/theirs**:  
  - `ours`: 현재 브랜치 우선  
  - `theirs`: 병합 대상 브랜치 우선  

### ✅ 실무 팁
- 커밋 메시지에서 코드블럭(```) 사용 피하기  
- 커밋 단위는 기능별로 작게! cherry-pick에 유리  


---

## ☁️ 3. 클라우드 & 인프라 구조

### ✅ 클라우드 개념

| 개념 | 설명 |
|------|------|
| 클라우드 컴퓨팅 | 온디맨드 자원 제공, 자동 확장/축소 가능 |
| Region | 여러 데이터 센터(가용 영역)의 묶음 |
| Availability Zone (AZ) | 독립된 전력/네트워크/위치를 가진 데이터센터 |
| VPC | Virtual Private Cloud, 사용자만의 네트워크 공간 |
| IAM | Identity & Access Mgmt. (역할, 최소 권한 설정) |

- **공동책임모델**: AWS는 인프라 책임, 사용자는 설정 보안 책임  
- **MFA 필수**, 루트 계정 최소 사용  
- **자동화**: Auto Scaling, ELB 설정 등  

### ✅ 인스턴스 & 자원

| 요소 | 설명 |
|------|------|
| EC2 | 가상 서버 인스턴스 |
| AMI | Amazon Machine Image (OS, 설정 포함) |
| EBS | Block Storage, 영구 저장소 |
| Instance Store | 휘발성 저장소 |
| S3 | 객체 저장소 (백업, 로그 등) |
| EFS/FSx | 공유 스토리지 (NAS처럼 사용) |

- `온디맨드`: 실시간 과금  
- `예약`: 일정 기간 사용 약정  
- `Spot`: 잉여 자원 저렴하게 사용  

### ✅ DevOps와 MSA
- **DevOps**: 개발과 운영의 통합 → 빠른 배포, 지속적 통합(CI), 테스트 자동화  
- **MSA (Microservices Architecture)**  
  - 느슨하게 결합된 도메인 단위 서비스  
  - bounded context, 빠른 배포, 독립적 유지보수  

### ✅ 데이터 흐름 (정보계 기준)
```
수집(ETL) → 저장(Data Lake) → 분석(Redshift) → 시각화(Kibana)
```
- Kinesis, Glue, Elasticsearch 등 활용
