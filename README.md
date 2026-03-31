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

터미널 조작 명령어
- pwd: 현재 경로 출력
- ls: 디렉토리 목록 보기
- ls -la: 숨김 파일을 포함해 디렉토리 목록 보기
- cd: 디렉토리 이동
- touch: 새로운 파일 생성
- cat: 파일 내용 출력
- echo: 터미널에 입력 내용 출력, 입력 내용 파일에 저장
- mkdir: 새로운 디렉토리 생성
- cp: 파일 복사
- mv: 파일 이동, 파일 이름 변경
- rm: 파일 삭제
cp, rm의 경우 폴더 단위로 할 경우 -r 옵션 필요

```
// 현재 위치 확인
sparrow95769576@c4r7s5 cdsy-E1-1 % pwd
/Users/sparrow95769576/cdsy-E1-1
```

```
// 목록 확인(숨김 파일 포함)
sparrow95769576@c4r7s5 cdsy-E1-1 % ls -la
total 8
drwxr-xr-x   4 sparrow95769576  sparrow95769576   128  3 30 17:54 .
drwxr-x---+ 21 sparrow95769576  sparrow95769576   672  3 30 17:54 ..
drwxr-xr-x  13 sparrow95769576  sparrow95769576   416  3 30 17:54 .git
-rw-r--r--   1 sparrow95769576  sparrow95769576  3718  3 30 17:54 README.md
```

```
// 폴더 생성
sparrow95769576@c4r7s5 cdsy-E1-1 % mkdir terminal-practice
```

```
// 이동
sparrow95769576@c4r7s5 cdsy-E1-1 % cd terminal-practice

// 이동 확인
sparrow95769576@c4r7s5 terminal-practice % pwd
/Users/sparrow95769576/cdsy-E1-1/terminal-practice
```

```
// 빈 파일 생성
sparrow95769576@c4r7s5 terminal-practice % touch hello.txt
sparrow95769576@c4r7s5 terminal-practice % touch bye.txt

// 파일 생성 확인
sparrow95769576@c4r7s5 terminal-practice % ls -la
total 0
drwxr-xr-x  4 sparrow95769576  sparrow95769576  128  3 30 18:02 .
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:01 ..
-rw-r--r--  1 sparrow95769576  sparrow95769576    0  3 30 18:02 bye.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576    0  3 30 18:01 hello.txt
```

```
// 파일 내용 변경
sparrow95769576@c4r7s5 terminal-practice % echo "Hello Codyssey" > hello.txt                    


// 파일 내용 확인
sparrow95769576@c4r7s5 terminal-practice % cat hello.txt 
Hello Codyssey
```

```
// 복사
sparrow95769576@c4r7s5 terminal-practice % cp hello.txt hello-copy.txt
```

```
// 이름 변경 전
sparrow95769576@c4r7s5 terminal-practice % ls -la
total 16
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:05 .
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:01 ..
-rw-r--r--  1 sparrow95769576  sparrow95769576    0  3 30 18:02 bye.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello-copy.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello.txt

// 이름 변경
sparrow95769576@c4r7s5 terminal-practice % mv bye.txt byebye.txt

// 이름 변경 후
sparrow95769576@c4r7s5 terminal-practice % ls -la
total 16
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:05 .
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:01 ..
-rw-r--r--  1 sparrow95769576  sparrow95769576    0  3 30 18:02 byebye.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello-copy.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello.txt
```

```
// 폴더 생성
sparrow95769576@c4r7s5 terminal-practice % mkdir new_folder

// 이동 전
sparrow95769576@c4r7s5 terminal-practice % ls -la
total 16
drwxr-xr-x  6 sparrow95769576  sparrow95769576  192  3 30 18:07 .
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:01 ..
-rw-r--r--  1 sparrow95769576  sparrow95769576    0  3 30 18:02 byebye.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello-copy.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello.txt
drwxr-xr-x  2 sparrow95769576  sparrow95769576   64  3 30 18:07 new_folder

// 이동
sparrow95769576@c4r7s5 terminal-practice % mv hello-copy.txt new_folder 

// 이동 후
sparrow95769576@c4r7s5 terminal-practice % ls -la
total 8
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:07 .
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:01 ..
-rw-r--r--  1 sparrow95769576  sparrow95769576    0  3 30 18:02 byebye.txt
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello.txt
drwxr-xr-x  3 sparrow95769576  sparrow95769576   96  3 30 18:07 new_folder

sparrow95769576@c4r7s5 terminal-practice % cd new_folder 


sparrow95769576@c4r7s5 new_folder % ls -la
total 8
drwxr-xr-x  3 sparrow95769576  sparrow95769576   96  3 30 18:07 .
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:07 ..
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello-copy.txt
```

```
sparrow95769576@c4r7s5 new_folder % cd ..

// 파일 삭제
sparrow95769576@c4r7s5 terminal-practice % rm byebye.txt 

// 폴더 삭제
sparrow95769576@c4r7s5 terminal-practice % rm -r new_folder 

// 삭제 확인
sparrow95769576@c4r7s5 terminal-practice % ls -la
total 8
drwxr-xr-x  3 sparrow95769576  sparrow95769576   96  3 30 18:08 .
drwxr-xr-x  5 sparrow95769576  sparrow95769576  160  3 30 18:01 ..
-rw-r--r--  1 sparrow95769576  sparrow95769576   15  3 30 18:05 hello.txt
```

## 5. 권한 실습

```
-  rwx  r--  r--
│   │    │    └── others (다른 사용자)
│   │    └─────── group (그룹)
│   └──────────── user (소유자)
└──────────────── 파일 종류 (- 파일 / d 폴더)
```

권한 종류
- r(read): 파일 읽기 / 폴더 내 파일 목록 보기
- w(write): 파일 쓰기 / 폴더 내 파일 생성/삭제/이름 변경
- x(execute): 파일 실행 / 폴더 들어가기

숫자 표기법
- 7: rwx(4+2+1)
- 6: rw-(4+2)
- 5: r-x(4+1)
- 4: r--(4)
- 3: -wx(2+1)
- 2: -w-(2)
- 1: --x(1)
- 0: ---

ex) chmod 755 = 소유자(rwx) 그룹(r-x) 다른 사용자(r-x)


파일 권한
```
// 스크립트는 없지만 권한 중 실행이 있으므로 .sh 파일로 생성
sparrow95769576@c4r7s7 permission-practice % touch test.sh
sparrow95769576@c4r7s7 permission-practice % ls -la test.sh 
-rw-r--r--  1 sparrow95769576  sparrow95769576  0  3 31 12:03 test.sh

// 권한 추가(사용자에게 실행 권한)
sparrow95769576@c4r7s7 permission-practice % chmod u+x test.sh 
sparrow95769576@c4r7s7 permission-practice % ls -la test.sh 
-rwxr--r--  1 sparrow95769576  sparrow95769576  0  3 31 12:03 test.sh

// 숫자로 권한 변경
sparrow95769576@c4r7s7 permission-practice % chmod 755 test.sh 
sparrow95769576@c4r7s7 permission-practice % ls -la         
total 0
drwxr-xr-x  3 sparrow95769576  sparrow95769576   96  3 31 12:03 .
drwxr-xr-x  6 sparrow95769576  sparrow95769576  192  3 31 11:59 ..
-rwxr-xr-x  1 sparrow95769576  sparrow95769576    0  3 31 12:03 test.sh

// 000으로 변경(권한 완전 제거)
sparrow95769576@c4r7s7 permission-practice % chmod 000 test.sh 
sparrow95769576@c4r7s7 permission-practice % ls -la
total 0
drwxr-xr-x  3 sparrow95769576  sparrow95769576   96  3 31 12:03 .
drwxr-xr-x  6 sparrow95769576  sparrow95769576  192  3 31 11:59 ..
----------  1 sparrow95769576  sparrow95769576    0  3 31 12:03 test.sh

// 권한이 없어 읽기 실패
sparrow95769576@c4r7s7 permission-practice % cat test.sh 
cat: test.sh: Permission denied

// 700으로 변경(사용자에게 모든 권한)
sparrow95769576@c4r7s7 permission-practice % chmod 700 test.sh 
sparrow95769576@c4r7s7 permission-practice % ls -la
total 0
drwxr-xr-x  3 sparrow95769576  sparrow95769576   96  3 31 12:03 .
drwxr-xr-x  6 sparrow95769576  sparrow95769576  192  3 31 11:59 ..
-rwx------  1 sparrow95769576  sparrow95769576    0  3 31 12:03 test.sh

// 읽기 성공
sparrow95769576@c4r7s7 permission-practice % cat test.sh 
```

폴더 권한
```
sparrow95769576@c4r7s7 permission-practice % mkdir test-dir
sparrow95769576@c4r7s7 permission-practice % ls -la
total 0
drwxr-xr-x  4 sparrow95769576  sparrow95769576  128  3 31 12:21 .
drwxr-xr-x  6 sparrow95769576  sparrow95769576  192  3 31 12:21 ..
drwxr-xr-x  2 sparrow95769576  sparrow95769576   64  3 31 12:21 test-dir
-rwx------  1 sparrow95769576  sparrow95769576    0  3 31 12:03 test.sh

// 사용자에게 실행 권한 제거
sparrow95769576@c4r7s7 permission-practice % chmod 644 test-dir 
sparrow95769576@c4r7s7 permission-practice % ls -la
total 0
drwxr-xr-x  4 sparrow95769576  sparrow95769576  128  3 31 12:21 .
drwxr-xr-x  6 sparrow95769576  sparrow95769576  192  3 31 12:21 ..
drw-r--r--  2 sparrow95769576  sparrow95769576   64  3 31 12:21 test-dir
-rwx------  1 sparrow95769576  sparrow95769576    0  3 31 12:03 test.sh

// 실행 권한이 없어 폴더 진입 실패
sparrow95769576@c4r7s7 permission-practice % cd test-dir 
cd: permission denied: test-dir

// 사용자에게 읽기 권한 제거
sparrow95769576@c4r7s7 permission-practice % chmod 300 test-dir 
sparrow95769576@c4r7s7 permission-practice % ls -la
total 0
drwxr-xr-x  4 sparrow95769576  sparrow95769576  128  3 31 12:21 .
drwxr-xr-x  6 sparrow95769576  sparrow95769576  192  3 31 12:21 ..
d-wx------  2 sparrow95769576  sparrow95769576   64  3 31 12:21 test-dir
-rwx------  1 sparrow95769576  sparrow95769576    0  3 31 12:03 test.sh
sparrow95769576@c4r7s7 permission-practice % ls -la | grep test-dir 
d-wx------  2 sparrow95769576  sparrow95769576   64  3 31 12:21 test-dir

// 읽기 실패
sparrow95769576@c4r7s7 permission-practice % ls test-dir 
ls: test-dir: Permission denied

// 사용자에게 모든 권한 부여
sparrow95769576@c4r7s7 permission-practice % chmod 755 test-dir

// 읽기 성공 
sparrow95769576@c4r7s7 permission-practice % ls test-dir 
```



## 6. Docker 설치/점검

## 7. Dockerfile 및 웹서버

## 8. 포트 매핑

## 9. 볼륨 영속성

## 10. 트러블슈팅
### 문제 1: Git 인증 실패

[문제]
```
git push origin master
# Username for 'https://github.com': hyjoo1226
# Password for 'https://hyjoo1226@github.com':
# remote: Invalid username or token.
# fatal: Authentication failed
```
git push 시도 시 HTTPS 인증 실패

[원인 가설]

권한이 주어지지 않아 push에 실패
GitHub는 이제 HTTPS 비밀번호 인증을 지원하지 않아 PAT 또는 SSH 사용 필요

[확인]

코디세이는 공용 컴퓨터 여러 개를 계속 이동하는 환경이므로 PAT 방식 사용
이러한 환경에서는 매번 SSH 키 생성 및 등록이 번거로움

PAT
- Github 비밀번호 대신 사용하는 임시 비밀번호로, HTTPS 방식에서 인증을 대체
- 동작 원리: Github 서버가 토큰을 검증 -> 권한에 따라 접근 허용
- 계정에 종속되므로 따로 저장만 해두면 어디서든 사용하기 편함
- 토큰 유출 위험, 만료 관리 필요

SSH
- 로컬 PC에 있는 개인 키와 Github에 등록된 공개 키를 이용한 인증
- 동작 원리: SSH 키 쌍 생성(비밀키, 공개키) -> 공개키를 Github 계정에 저장 -> Github 서버가 등록된 공개 키로 Challenge(도전 값, 랜덤 메세지) 전달 -> 로컬 PC에서는 비밀 키로 Challenge를 암호화(서명) -> 서명 검증
- SSH는 로컬 환경(~/.ssh)에 키가 저장되기 때문에 환경이 유지되는 개인 PC에서 효율적
- 보안성 높으나 공용 환경에선 부적합


[해결]

1. PAT(Personal Access Token) 생성
- Github Settings -> Developer settings -> Tokens
- 권한: repo 체크

2. git push 시 사용
```
git push origin master

// 입력(기존 비밀번호 자리에 토큰 입력)
Username: hyjoo1226
Password: [PAT 입력]
```


### 문제 2:
