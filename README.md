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
- [v] 터미널 기본 조작
- [v] 파일 권한 실습
- [v] Docker 설치/점검
- [v] hello-world 실행
- [v] Dockerfile 빌드/실행
- [v] 포트 매핑 접속
- [ ] 바인드 마운트
- [v] 볼륨 영속성
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

```
sparrow95769576@c4r7s7 cdsy-E1-1 % docker --version

Docker version 28.5.2, build ecc6942
```

```
sparrow95769576@c4r7s7 cdsy-E1-1 % docker info

Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/sparrow95769576/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/sparrow95769576/.docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 9bc6c2ab-7a11-4a67-aa18-8841c98643bc
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set
```
warning은 Docker가 네트워크 방화벽 규칙 일부를 사용하지 않았다는 의미
-> 현재 OrbStack이 자체 네트워크 방식을 쓰기 때문에 생긴 것으로, 정상 동작에 영향 없음


## 7. Docker 기본 운영 명령

```
// hello-world 명령 실행
sparrow95769576@c4r7s7 cdsy-E1-1 % docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
hello-world 명령어:  이미지 다운로드(없으면) -> 컨테이너 생성 -> 프로그램  실행 -> 종료

```
// 이미지 목록 확인
sparrow95769576@c4r7s7 cdsy-E1-1 % docker images

REPOSITORY    TAG       IMAGE ID       CREATED      SIZE
hello-world   latest    e2ac70e7319a   7 days ago   10.1kB
```
컨테이너를 만들려면 이미지가 필요
- 이미지: 컨테이너를 만들기 위한 템플릿(규격화된 파일 시스템 + 실행 환경 + 앱/프로그램 포함)
- 컨테이너: 이미지 기반으로 실제 실행되는 독립적인 프로세스

어떤 이미지가 있는지 확인하는 것을 통해 새 이미지 다운로드 여부 판단, 오래되거나 사용하지 않는 이미지 판단 가능


```
// 컨테이너 목록 확인(실행 중)
sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

// 컨테이너 목록 확인(종료된 것 포함 전체)
sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
3a4e3890a7c8   hello-world   "/hello"   17 seconds ago   Exited (0) 17 seconds ago             exciting_margulis
```
hello-world 명령어를 사용했으므로 ps -a 명령어를 입력했을 때만 나타나는 모습

```
// 로그 확인
sparrow95769576@c4r7s7 cdsy-E1-1 % docker logs 3a4e3890a7c8

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```


```
// stats(컨테이너별 리소스 사용량) 확인
sparrow95769576@c4r7s7 cdsy-E1-1 % docker stats 3a4e3890a7c8

Hello from Docker!
This message shows that your installation appears to be working correctly.

CONTAINER ID   NAME                CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS 
3a4e3890a7c8   exciting_margulis   0.00%     0B / 0B             0.00%     0B / 0B   0B / 0B     0 
```
현재는 실행된 컨테이너가 없는 모습

## 8. 컨테이너 실행 실습

```
// ubuntu 컨테이너 실행
// docker run -it -- name [ 이름 지정] [사용할 이미지] [진입 후 실행할 명령]
// -it: 터미널 상호작용 옵션
sparrow95769576@c4r7s7 cdsy-E1-1 % docker run -it --name ubuntu-practice ubuntu bash

Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
817807f3c64e: Pull complete 
Digest: sha256:186072bba1b2f436cbb91ef2567abca677337cfc786c86e107d25b7072feef0c
Status: Downloaded newer image for ubuntu:latest

root@130521e01b1c:/# pwd
/

root@130521e01b1c:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

root@130521e01b1c:/# echo "Hello"
Hellols!

root@1e831827e2c5:/# exit
exit
```

```
// -d(백그라운드 실행) 옵션으로 컨테이너 실행
sparrow95769576@c4r7s7 cdsy-E1-1 % docker run -it -d --name ubuntu-bg ubuntu bash
bd9deb02a8a3b08430d68c48df165c05195a538c4a55a66b1bc56232bed7ad44

sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS          PORTS     NAMES
bd9deb02a8a3   ubuntu    "bash"    36 seconds ago   Up 36 seconds             ubuntu-bg

sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED             STATUS                          PORTS     NAMES
bd9deb02a8a3   ubuntu        "bash"     51 seconds ago      Up 51 seconds                             ubuntu-bg
1e831827e2c5   ubuntu        "bash"     6 minutes ago       Exited (0) About a minute ago             ubuntu-practice
3a4e3890a7c8   hello-world   "/hello"   About an hour ago   Exited (0) About an hour ago              exciting_margulis
```
-> 기존 실행 방법은 컨테이너가 터미널과 붙어있을 때만 살아있고 exit하면 종료
-> -d 옵션을 사용하면 터미널과 분리해 백그라운드로 실행되므로, 터미널을 종료하더라도 컨테이너가 살아있음

```
// attach: 이미 실행 중인 컨테이너의 메인 프로세스에 연결
sparrow95769576@c4r7s7 cdsy-E1-1 % docker attach ubuntu-bg

root@bd9deb02a8a3:/# exit
exit

sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps              
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
-> 분리된 컨테이너를 다시 붙인 상태이므로 exit를 하면 컨테이너가 종료됨

```
sparrow95769576@c4r7s7 cdsy-E1-1 % docker run -it -d --name ubuntu-exec ubuntu bash
5b23e90b56bb0f400e397d2d06dc8aa8c355ae81524aa65ae27992d2d3427c85

sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED         STATUS         PORTS     NAMES
5b23e90b56bb   ubuntu    "bash"    5 seconds ago   Up 5 seconds             ubuntu-exec

// exec: 실행 중인 컨테이너에 새로운 프로세스 실행
sparrow95769576@c4r7s7 cdsy-E1-1 % docker exec -it ubuntu-exec bash

root@5b23e90b56bb:/# exit   
exit

sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS          PORTS     NAMES
5b23e90b56bb   ubuntu    "bash"    54 seconds ago   Up 54 seconds             ubuntu-exec
```
-> 컨테이너에서 새로 실행한 상태이므로 exit하더라도 컨테이너가 살아있음


## 8. 포트 매핑

## 9. 볼륨 영속성

```
// 볼륨 생성
sparrow95769576@c4r7s7 cdsy-E1-1 % docker volume create my-db-storage
my-db-storage

// 볼륨 목록 확인
sparrow95769576@c4r7s7 cdsy-E1-1 % docker volume ls
DRIVER    VOLUME NAME
local     my-db-storage

// 볼륨의 상세 정보 확인
sparrow95769576@c4r7s7 cdsy-E1-1 % docker volume inspect my-db-storage
[
    {
        "CreatedAt": "2026-03-31T15:52:25+09:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/my-db-storage/_data",
        "Name": "my-db-storage",
        "Options": null,
        "Scope": "local"
    }
]
```

```
// 볼륨을 /app/data 경로에 마운트하여 컨테이너 실행
// sleep infinity 옵션: 컨테이너가 종료되지 않도록 유지시켜주는 옵션
sparrow95769576@c4r7s7 cdsy-E1-1 % docker run -d --name worker-v1 -v my-db-storage:/app/data ubuntu sleep infinity
08a173b533096d8ff159d9e7d703383c954b68b26297baf5154231639010634b

// 컨테이너 내부에 데이터 파일 생성
sparrow95769576@c4r7s7 cdsy-E1-1 % docker exec -it worker-v1 bash -c "echo 'Persistence Test: Success' > /app/data/result.txt"

// 생성된 파일 내용 확인
sparrow95769576@c4r7s7 cdsy-E1-1 % docker exec -it worker-v1 cat /app/data/result.txt
Persistence Test: Success

// 컨테이너 삭제
sparrow95769576@c4r7s7 cdsy-E1-1 % docker rm -f worker-v1
worker-v1

sparrow95769576@c4r7s7 cdsy-E1-1 % docker ps -a | grep worker-v1

// 동일한 볼륨을 새 컨테이너에 연결
sparrow95769576@c4r7s7 cdsy-E1-1 % docker run -d --name worker-v2 -v my-db-storage:/app/data ubuntu sleep infinity
02f08b585b24b7cc589edb1d27213f85933b895c5462d27a231e5688eeffa0c1

// 이전 컨테이너에 생성했던 파일이 존재하는지 확인
sparrow95769576@c4r7s7 cdsy-E1-1 % docker exec -it worker-v2 cat /app/data/result.txt
Persistence Test: Success
```


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
