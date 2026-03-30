# AI/SW 개발 워크스테이션 구축

## 1. 프로젝트 개요
이 프로젝트는 개발자로서 필수적인 세 가지 핵심 도구인
**터미널(CLI), Docker(컨테이너), Git/GitHub(버전 관리)** 를
직접 설치하고 운영하는 경험을 통해
재현 가능한 개발 워크스테이션 환경을 구축하는 것을 목표로 합니다.

## 2. 실행 환경
- OS: 
- Shell: 
- Docker: 28.5.2
- Git: 

## 3. 수행 체크리스트
- [ ] 터미널 기본 조작
- [ ] 파일 권한 실습
- [ ] Docker 설치/점검
- [ ] hello-world 실행
- [ ] Dockerfile 빌드/실행
- [ ] 포트 매핑 접속
- [ ] 바인드 마운트
- [ ] 볼륨 영속성
- [ ] Git 설정 + GitHub 연동

## 4. 터미널 조작 로그
(작업하면서 채워나가기)

## 5. 권한 실습

## 6. Docker 설치/점검

## 7. Dockerfile 및 웹서버

## 8. 포트 매핑

## 9. 볼륨 영속성

## 10. 트러블슈팅
### 문제 1: Git 인증 실패 → SSH 방식으로 전환

[문제]
bash
git push origin master
# Username for 'https://github.com': hyjoo1226
# Password for 'https://hyjoo1226@github.com':
# remote: Invalid username or token.
# fatal: Authentication failed

git push 시도 시 HTTPS 인증 실패

[원인 가설]

권한이 주어지지 않아 push에 실패
GitHub는 2021년부터 HTTPS 비밀번호 인증을 폐지

→ 대안 2가지 검토

방식	설명	환경 적합 여부
Personal Access Token	HTTPS 유지, 토큰으로 인증	 매 세션마다 토큰 관리 번거로움
SSH 키 인증	키 한 번 등록 후 자동 인증	 같은 계정/홈폴더 유지되므로 영구 사용 가능

→ 현재 작업 환경에서 로그아웃 했을 때 기록이 사라지는지 여부를 파악해야 방법을 선택할 수 있을 것

bash
# 1. 현재 내 홈 디렉토리 위치
echo $HOME

/Users/sparrow95769576

# 2. 현재 작업 중인 저장소 위치
pwd

/Users/sparrow95769576/cdsy-E1-1

# 3. 현재 로그인된 사용자
whoami

sparrow95769576


→ 같은 맥 계정을 계속 사용하는 환경이므로 SSH 방식 채택(SSH 키 한번 설정 시 영구적으로 유지)

[확인]
1. SSH 키 생성 및 GitHub 등록

bash
# 키 생성
ssh-keygen -t ed25519 -C "hyjoo1226@gmail.com"

# 공개키 클립보드 복사 → GitHub Settings에 등록
pbcopy < ~/.ssh/id_ed25519.pub
⚠️ 주의: SHA256:xxxx 형태의 fingerprint는 키가 아님
→ ssh-ed25519 AAAA... 로 시작하는 한 줄 전체가 공개키

2. SSH 연결 테스트

bash
ssh -T git@github.com
# Hi hyjoo1226! You've successfully authenticated.

3. 저장소 원격 주소 확인

bash
sparrow95769576@c4r7s5 cdsy-E1-1 % git push origin master
Username for 'https://github.com': hyjoo1226
Password for 'https://hyjoo1226@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/hyjoo1226/cdsy-E1-1.git/'

→ SSH 연결을 했음에도 여전히 권한 문제 발생

bash
git remote -v
# origin  https://github.com/hyjoo1226/cdsy-E1-1.git  ← ⚠️ 아직 HTTP
S
→ SSH 키 등록은 됐지만 저장소 주소가 여전히 HTTPS였던 것이 근본 원인

[해결]

bash
# 원격 주소를 SSH 방식으로 변경
git remote set-url origin git@github.com:hyjoo1226/cdsy-E1-1.git

# 변경 확인
git remote -v
# origin  git@github.com:hyjoo1226/cdsy-E1-1.git (fetch)
# origin  git@github.com:hyjoo1226/cdsy-E1-1.git (push)

# 푸시 성공
git push origin master

SSH 키 등록만으로는 부족
→ 저장소 주소도 반드시 SSH 형식으로 변경해야 함

HTTPS 형식: https://github.com/계정명/저장소.git
SSH  형식:  git@github.com:계정명/저장소.git

### 문제 2:
