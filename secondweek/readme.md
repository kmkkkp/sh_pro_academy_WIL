# 🛡️ 클라우드 보안 및 네트워크 구성 정리

## ✅ 1. 정보보호센터 특강 - 클라우드 보안 인프라

### 🔷 보안 인프라 구축
- **방화벽**: 외부에서 내부로의 파일 유입 시 망연계 제어  
- **DRM**: 데이터 보안 및 유출 방지  
- **Cloud-native**: DevOps 기반 무중단 서비스 구축  

### 🔷 클라우드 보안 솔루션

1. **NGFW (Next-Gen Firewall):**
   - L7 레이어에서 HTTP, HTTPS 트래픽까지 검사  
   - TCP 외에 전체 패킷을 분석  

2. **CSPM (Cloud Security Posture Management):**
   - 클라우드 설정 오류 및 취약점 탐지  
   - 보안 컴플라이언스 준수 점검  

3. **CWPP (Cloud Workload Protection Platform):**
   - 컨테이너 보안, 파드/오토스케일링 보호  

4. **CNAPP (Cloud Native Application Protection Platform):**
   - CSPM + CWPP 통합 보안 솔루션  
   - DevSecOps 환경에 최적화  

---

## ✅ 2. VPC와 네트워크 서브넷

### 🔷 VPC (Virtual Private Cloud)
- AWS에서 제공하는 네트워크 환경, 서브넷 단위로 분리 가능  
- **프라이빗 IP**: 내부 네트워크에서만 사용  
- **공인 IP**: 외부 접근 가능 (Public Subnet)  
- RFC 1918 규약 준수 중요 (`172.31.0.0/16` 사용)

### 🔷 서브넷 구성
- **서브넷 마스크:** `/24` (256개 IP 가능)  
- **AZ (Availability Zone)**: 서브넷은 서로 다른 AZ에 분산 배치하여 무중단 운영  
- **라우팅 테이블:** 인터넷 게이트웨이를 통해 트래픽 제어  
- **네트워크 ACL:** 서브넷 단위 보안 정책  

---

## ✅ 3. EC2, RDS, ElastiCache 실습

### 🔷 EC2와 SSH 터널링
- EC2에 Jupyter Notebook 서버 설치 및 보안 설정  
- SSH 터널링을 통해 private RDS 및 ElastiCache에 연결  

**SSH 터널링 명령어:**  
```bash
ssh -N -i {키파일경로} -L {로컬포트}:{엔드포인트}:{포트} {사용자}@{호스트IP}
```

**예제:**  
```bash
ssh -N -i ~/mykey.pem -L 8888:redis-endpoint:6379 ec2-user@public-ip
```

---

### 🔷 Jupyter Notebook 설치 및 구성

**가상 환경 생성:**  
```bash
conda create -n jupyter python=3.11
conda activate jupyter
pip install jupyterlab
```

**암호화된 비밀번호 생성:**  
```python
from jupyter_server.auth import passwd
passwd()
```

**Jupyter 설정파일 생성:**  
```bash
jupyter notebook --generate-config
vi /home/ubuntu/.jupyter/jupyter_notebook_config.py
```

**설정파일 내용 예시:**  
```python
c.NotebookApp.password = u'argon2:hashed_password'
c.NotebookApp.ip = "EC2 Private IP"
c.NotebookApp.notebook_dir = '/'
```

**포트 개방 설정:**  
- 보안 그룹에서 `8888` 포트를 인바운드로 허용  

---

### 🔷 성능 평가
- 네트워크 I/O: `ping` 테스트  
- CPU 사용률: `htop` 또는 `top`  
- 디스크 속도: `dd` 또는 `fio`  

---

### ✅ 참고 링크
- SSH Tunneling 유튜브 강의: [YouTube - SSH Tunneling](https://www.youtube.com/watch?v=rFWpEIATZNw)
