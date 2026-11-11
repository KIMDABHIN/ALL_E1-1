# E1-1. 개발 워크스테이션 구축 및 Docker 실습

> Windows 환경에서 WSL2와 Ubuntu를 활용한 Linux 개발 환경을 구축하고, Docker를 이용해 웹 서버를 실행하며 컨테이너와 데이터 저장 방식을 실습한 프로젝트입니다.

---

## 1. 프로젝트 개요

### 프로젝트 목표

개발에 필요한 기본적인 워크스테이션 환경을 구축하고 Linux 명령어와 Docker의 핵심 기능을 직접 실습하는 것을 목표로 합니다.

### 주요 학습 내용

- WSL2를 활용한 Windows 내 Linux 환경 구축
- Ubuntu 터미널을 이용한 Linux 기본 명령어 실습
- Linux 파일 및 디렉터리 관리
- 파일 권한과 접근 권한 이해
- Docker 설치 및 기본 명령어 실습
- Docker 이미지와 컨테이너의 차이 이해
- Nginx 웹 서버 실행
- Dockerfile을 이용한 사용자 정의 이미지 제작
- Bind Mount를 이용한 파일 공유
- Docker Volume을 이용한 데이터 영속성 확인
- Git과 GitHub를 이용한 프로젝트 관리

---

## 2. 개발 환경

| 구분 | 사용 환경 |
|---|---|
| 운영체제 | Windows |
| Linux 환경 | Ubuntu (WSL2) |
| 컨테이너 플랫폼 | Docker Desktop |
| Linux 배포판 | Ubuntu |
| 웹 서버 | Nginx |
| 버전 관리 | Git |
| 원격 저장소 | GitHub |
| 편집 및 실행 | VS Code / Ubuntu Terminal |

### 주요 버전 확인

```bash
wsl --status
wsl --list --verbose
docker --version
git --version
```

Docker 버전 확인 결과:

```text
Docker version 29.9.2
```

Git 버전 확인 결과:

```text
git version 2.53.0
```

---

# 3. 미션별 수행 내용

## Mission 1. WSL2 및 Ubuntu 개발 환경 구축

### 1-1. 미션 목표

Windows 환경에서 Linux를 사용할 수 있도록 WSL2와 Ubuntu를 설치하고 기본적인 Linux 실행 환경을 구축합니다.

### 1-2. 수행 내용

1. Windows에서 WSL 설치 여부 확인
2. WSL2 기본 버전 확인
3. Ubuntu 배포판 설치
4. Ubuntu 사용자 계정 생성
5. Windows 드라이브와 Ubuntu의 연결 구조 확인

### 1-3. 수행 명령어

**WSL 상태 확인**

```powershell
wsl --status
```

**설치된 Linux 배포판 확인**

```powershell
wsl --list --verbose
```

**Ubuntu 설치**

```powershell
wsl --install -d Ubuntu
```

**Ubuntu 실행**

```powershell
wsl
```

### 1-4. Windows와 Linux의 파일 경로 연결

Windows의 D 드라이브는 Ubuntu에서 `/mnt/d` 경로로 접근할 수 있습니다.

예를 들어 Windows의 다음 경로는

```text
D:\E1-1
```

Ubuntu에서는 다음과 같이 표현됩니다.

```text
/mnt/d/E1-1
```

실습 중 확인한 경로:

```bash
pwd
```

출력 예시:

```text
/mnt/d/E1-1
```

### 1-5. 학습 결과

- WSL2를 통해 Windows에서 Linux 환경을 실행할 수 있음을 확인했습니다.
- Ubuntu가 Linux 배포판이라는 점을 이해했습니다.
- Windows 드라이브와 Linux 경로의 연결 구조를 학습했습니다.
- Linux 터미널을 이용해 파일과 디렉터리를 관리할 수 있는 기반을 마련했습니다.

---

## Mission 2. Linux 기본 명령어 및 파일 시스템 실습

### 2-1. 미션 목표

Linux 터미널에서 기본 명령어를 사용하여 디렉터리 생성, 파일 생성, 내용 작성, 복사, 이동, 이름 변경 및 삭제 작업을 수행합니다.

### 2-2. 디렉터리 및 파일 확인

| 명령어 | 기능 |
|---|---|
| `pwd` | 현재 작업 위치 확인 |
| `ls` | 파일 및 디렉터리 목록 확인 |
| `ls -a` | 숨김 파일을 포함한 전체 목록 확인 |
| `cd` | 디렉터리 이동 |

수행 명령어:

```bash
pwd
ls
ls -a
cd practice
```

### 2-3. 디렉터리 생성 및 파일 생성

수행 명령어:

```bash
mkdir practice
cd practice
touch memo.txt
```

- `mkdir`: 새로운 디렉터리 생성
- `touch`: 새로운 파일 생성

### 2-4. 파일 내용 작성 및 확인

수행 명령어:

```bash
echo "Hello, Linux!" > memo.txt
cat memo.txt
```

실행 결과:

```text
Hello, Linux!
```

`echo`로 파일에 내용을 입력하고 `cat`으로 작성된 내용을 확인했습니다.

### 2-5. 파일 복사 및 이름 변경

수행 명령어:

```bash
cp memo.txt memo_backup.txt
mv memo_backup.txt memo_copy.txt
```

- `cp`: 파일 복사
- `mv`: 파일 이동 또는 이름 변경

### 2-6. 파일 및 디렉터리 이동과 삭제

수행 명령어:

```bash
mkdir backup
mv memo_copy.txt backup/
ls backup
rm backup/memo_copy.txt
rmdir backup
```

- `rm`: 파일 삭제
- `rmdir`: 비어 있는 디렉터리 삭제

### 2-7. 숨김 파일 확인

Linux에서는 파일명 앞에 `.`을 붙이면 숨김 파일로 취급됩니다.

수행 명령어:

```bash
touch .secret.txt
ls
ls -a
rm .secret.txt
```

`ls`에서는 보이지 않지만 `ls -a`에서는 숨김 파일이 표시되는 것을 확인했습니다.

### 2-8. 학습 결과

- Linux의 기본 파일 및 디렉터리 관리 명령어를 익혔습니다.
- 상대 경로와 현재 작업 위치의 중요성을 이해했습니다.
- 파일 복사, 이동, 이름 변경 및 삭제를 직접 수행했습니다.
- 숨김 파일의 개념과 확인 방법을 학습했습니다.

---

## Mission 3. Linux 파일 권한 실습

### 3-1. 미션 목표

Linux에서 파일 접근 권한의 개념을 이해하고 `chmod` 명령어를 사용하여 권한을 변경합니다.

### 3-2. 파일 권한 확인

수행 명령어:

```bash
touch permission.txt
ls -l permission.txt
```

Linux 파일 권한은 다음과 같은 세 가지 사용자 구분을 기준으로 관리됩니다.

- User: 파일 소유자
- Group: 파일 소유 그룹
- Other: 그 외 사용자

### 3-3. 권한 변경

Ubuntu 홈 디렉터리에서 다음 명령어를 실행했습니다.

**644 권한 설정**

```bash
chmod 644 permission.txt
ls -l permission.txt
```

결과:

```text
-rw-r--r--
```

**755 권한 설정**

```bash
chmod 755 permission.txt
ls -l permission.txt
```

결과:

```text
-rwxr-xr-x
```

### 3-4. 권한 숫자의 의미

| 숫자 | 권한 | 의미 |
|---|---|---|
| 4 | r | 읽기 |
| 2 | w | 쓰기 |
| 1 | x | 실행 |
| 0 | - | 권한 없음 |

권한은 각 사용자 그룹에 부여된 숫자의 합으로 표현합니다.

- 644: 소유자는 읽기와 쓰기, 나머지는 읽기만 가능
- 755: 소유자는 읽기·쓰기·실행, 나머지는 읽기·실행 가능

### 3-5. 실습 중 확인한 사항

Windows 드라이브가 연결된 `/mnt/d` 경로에서는 Linux 파일 시스템과 권한 처리 방식이 다르기 때문에 `chmod` 변경 결과가 제한적으로 반영될 수 있음을 확인했습니다.

따라서 권한 변경 실습은 Ubuntu 홈 디렉터리에서 진행했습니다.

### 3-6. 학습 결과

- Linux 파일 권한의 기본 구조를 이해했습니다.
- 읽기, 쓰기, 실행 권한의 의미를 학습했습니다.
- `chmod` 명령어를 이용해 파일 권한을 변경했습니다.
- Windows 마운트 경로와 Linux 자체 파일 시스템의 차이를 확인했습니다.

---

## Mission 4. Docker 설치 및 기본 기능 실습

### 4-1. 미션 목표

Docker의 개념을 이해하고 컨테이너를 실행, 확인, 종료 및 재시작하는 기본적인 관리 작업을 수행합니다.

### 4-2. Docker 실행 환경 구축

Docker Desktop을 설치하고 WSL Integration을 활성화하여 Ubuntu에서 Docker를 사용할 수 있도록 설정했습니다.

버전 확인:

```bash
docker --version
```

Docker 정보 확인:

```bash
sudo docker info
```

실습 환경에서는 Docker 명령어 실행 시 권한 문제가 발생하여 `sudo`를 사용했습니다.

### 4-3. Docker 정상 작동 확인

수행 명령어:

```bash
sudo docker run hello-world
```

Docker가 정상적으로 이미지를 다운로드하고 컨테이너를 실행하는 것을 확인했습니다.

### 4-4. Docker 이미지 확인

```bash
sudo docker images
```

현재 시스템에 저장된 Docker 이미지 목록을 확인했습니다.

### 4-5. 컨테이너 확인

```bash
sudo docker ps
```

현재 실행 중인 컨테이너를 확인했습니다.

```bash
sudo docker ps -a
```

종료된 컨테이너까지 포함한 전체 목록을 확인했습니다.

### 4-6. 컨테이너 로그 확인

```bash
sudo docker logs ecstatic_newton
```

컨테이너에서 발생한 로그를 확인했습니다.

### 4-7. 컨테이너 실행 및 종료

```bash
sudo docker start ecstatic_newton
sudo docker stop ecstatic_newton
```

기존에 생성한 컨테이너를 다시 시작하고 종료하는 작업을 수행했습니다.

### 4-8. 컨테이너 리소스 확인

```bash
sudo docker stats --no-stream
```

컨테이너의 CPU 및 메모리 사용량 등의 상태를 확인했습니다.

### 4-9. 컨테이너 내부 데이터 유지 확인

Ubuntu 컨테이너를 실행한 후 내부에서 파일을 생성했습니다.

컨테이너 내부 명령어:

```bash
echo "Docker Test" > docker_test.txt
cat docker_test.txt
```

이후 컨테이너를 종료하고 다시 시작하여 파일이 유지되는지 확인했습니다.

### 4-10. 학습 결과

- Docker 이미지와 컨테이너의 기본 개념을 이해했습니다.
- Docker Hub에서 이미지를 다운로드하고 컨테이너를 실행하는 과정을 경험했습니다.
- 컨테이너의 실행, 종료, 재시작 및 로그 확인을 수행했습니다.
- 컨테이너 내부 파일의 데이터 유지 여부를 확인했습니다.

---

## Mission 5. Dockerfile을 이용한 Nginx 웹 서버 구축

### 5-1. 미션 목표

Dockerfile을 직접 작성하여 사용자 정의 Docker 이미지를 만들고, Nginx 웹 서버를 실행하여 브라우저에서 직접 확인합니다.

### 5-2. 프로젝트 디렉터리 구성

```text
E1-1/
└── E1-1-nginx/
    ├── Dockerfile
    └── index.html
```

### 5-3. HTML 파일 작성

`index.html`

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>나의 Docker 웹페이지</title>
</head>
<body>
    <h1>Hello, Bind Mount!</h1>
    <p>파일 수정 내용이 Docker 컨테이너에 반영됩니다.</p>
</body>
</html>
```

직접 HTML 파일을 작성하여 Nginx가 제공할 웹페이지를 구성했습니다.

### 5-4. Dockerfile 작성

`Dockerfile`

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

각 명령어의 역할:

- `FROM nginx:alpine`: 경량화된 Nginx 이미지를 기반 이미지로 사용합니다.
- `COPY`: 작성한 HTML 파일을 Nginx의 기본 웹 문서 경로로 복사합니다.

### 5-5. Docker 이미지 빌드

프로젝트 디렉터리에서 실행:

```bash
sudo docker build -t my-nginx .
```

- `docker build`: Docker 이미지 생성
- `-t my-nginx`: 이미지 이름 지정
- `.`: 현재 디렉터리를 빌드에 사용할 경로로 지정

### 5-6. Nginx 컨테이너 실행

```bash
sudo docker run -d --name my-nginx-container -p 8080:80 my-nginx
```

명령어 구성:

| 옵션 | 의미 |
|---|---|
| `-d` | 백그라운드 실행 |
| `--name` | 컨테이너 이름 지정 |
| `-p 8080:80` | 호스트 8080 포트와 컨테이너 80 포트 연결 |
| `my-nginx` | 실행할 Docker 이미지 |

### 5-7. 웹페이지 접속 확인

Windows 브라우저에서 다음 주소로 접속했습니다.

```text
http://localhost:8080
```

직접 작성한 HTML 페이지가 정상적으로 표시되는 것을 확인했습니다.

### 5-8. 학습 결과

- Dockerfile의 기본 구조를 이해했습니다.
- 사용자 정의 Docker 이미지를 직접 생성했습니다.
- Nginx 웹 서버를 컨테이너 형태로 실행했습니다.
- 포트 포워딩을 통해 브라우저에서 컨테이너의 웹페이지에 접속했습니다.

---

## Mission 6. Bind Mount를 이용한 파일 공유

### 6-1. 미션 목표

호스트 컴퓨터의 파일과 Docker 컨테이너 내부의 디렉터리를 연결하여 파일 수정 내용이 실시간으로 반영되는지 확인합니다.

### 6-2. Bind Mount 컨테이너 실행

프로젝트 디렉터리에서 다음 명령어를 실행했습니다.

```bash
sudo docker run -d --name my-nginx-bind -p 8081:80 -v "$PWD":/usr/share/nginx/html:ro my-nginx
```

명령어 구성:

| 옵션 | 의미 |
|---|---|
| `-d` | 백그라운드 실행 |
| `--name my-nginx-bind` | 컨테이너 이름 지정 |
| `-p 8081:80` | 호스트 8081 포트와 컨테이너 80 포트 연결 |
| `-v` | 호스트와 컨테이너 디렉터리 연결 |
| `$PWD` | 현재 작업 디렉터리 |
| `:ro` | 읽기 전용으로 마운트 |

### 6-3. 웹페이지 접속

브라우저에서 다음 주소로 접속했습니다.

```text
http://localhost:8081
```

Bind Mount로 연결한 HTML 페이지가 정상적으로 표시되는 것을 확인했습니다.

### 6-4. 파일 수정 테스트

기존 HTML 내용을 다음과 같이 변경했습니다.

```html
<h1>Hello, Bind Mount!</h1>
<p>파일 수정 내용이 Docker 컨테이너에 반영됩니다.</p>
```

파일 수정 후 브라우저를 새로고침했습니다.

별도의 이미지 재빌드나 컨테이너 재생성 없이 수정 내용이 반영되는 것을 확인했습니다.

### 6-5. 학습 결과

- Bind Mount의 개념과 사용 방법을 이해했습니다.
- 호스트 컴퓨터의 디렉터리를 컨테이너 내부에 연결했습니다.
- 파일 수정 내용이 컨테이너에 반영되는 과정을 확인했습니다.
- 개발 과정에서 Bind Mount를 활용하면 코드 수정 및 테스트가 편리해진다는 점을 학습했습니다.

---

## Mission 7. Docker Volume을 이용한 데이터 영속성 실습

### 7-1. 미션 목표

컨테이너가 삭제되더라도 데이터를 유지할 수 있도록 Docker Volume을 생성하고 데이터 영속성을 확인합니다.

### 7-2. Docker Volume 생성

```bash
sudo docker volume create nginx-data
```

생성된 Volume 확인:

```bash
sudo docker volume ls
```

### 7-3. Volume을 컨테이너에 연결

```bash
sudo docker run -it --name volume-test -v nginx-data:/data ubuntu bash
```

명령어 구성:

| 옵션 | 의미 |
|---|---|
| `-it` | 대화형 터미널 실행 |
| `--name` | 컨테이너 이름 지정 |
| `-v nginx-data:/data` | Docker Volume을 컨테이너의 `/data`에 연결 |
| `ubuntu` | 사용할 이미지 |
| `bash` | 컨테이너 내부 Bash 실행 |

### 7-4. Volume에 데이터 저장

컨테이너 내부에서 실행:

```bash
echo "Docker Volume 데이터 보존 테스트!" > /data/test.txt
cat /data/test.txt
```

실행 결과:

```text
Docker Volume 데이터 보존 테스트!
```

### 7-5. 다른 컨테이너에서 데이터 확인

새로운 Ubuntu 컨테이너를 실행하면서 기존 Volume을 다시 연결했습니다.

```bash
sudo docker run --rm -it -v nginx-data:/data ubuntu bash
```

컨테이너 내부에서 실행:

```bash
cat /data/test.txt
```

실행 결과:

```text
Docker Volume 데이터 보존 테스트!
```

새로운 컨테이너에서도 기존 데이터가 정상적으로 출력되는 것을 확인했습니다.

### 7-6. 학습 결과

- Docker Volume의 개념을 이해했습니다.
- Volume을 생성하고 컨테이너에 연결하는 방법을 학습했습니다.
- 컨테이너가 달라져도 Volume에 저장된 데이터는 유지될 수 있음을 확인했습니다.
- 컨테이너와 데이터 저장 공간을 분리하는 이유를 이해했습니다.

---

# 4. 주요 명령어 정리

## Linux 명령어

| 명령어 | 기능 |
|---|---|
| `pwd` | 현재 경로 확인 |
| `ls` | 파일 목록 확인 |
| `ls -a` | 숨김 파일 포함 목록 확인 |
| `cd` | 디렉터리 이동 |
| `mkdir` | 디렉터리 생성 |
| `touch` | 파일 생성 |
| `echo` | 문자열 출력 및 파일 작성 |
| `cat` | 파일 내용 확인 |
| `cp` | 파일 복사 |
| `mv` | 파일 이동 및 이름 변경 |
| `rm` | 파일 삭제 |
| `rmdir` | 빈 디렉터리 삭제 |
| `chmod` | 파일 권한 변경 |

## Docker 명령어

| 명령어 | 기능 |
|---|---|
| `docker --version` | Docker 버전 확인 |
| `docker info` | Docker 환경 정보 확인 |
| `docker run` | 컨테이너 생성 및 실행 |
| `docker images` | 이미지 목록 확인 |
| `docker ps` | 실행 중인 컨테이너 확인 |
| `docker ps -a` | 전체 컨테이너 확인 |
| `docker logs` | 컨테이너 로그 확인 |
| `docker start` | 컨테이너 시작 |
| `docker stop` | 컨테이너 종료 |
| `docker stats` | 컨테이너 리소스 사용량 확인 |
| `docker build` | Docker 이미지 빌드 |
| `docker volume create` | Volume 생성 |
| `docker volume ls` | Volume 목록 확인 |

## Git 명령어

| 명령어 | 기능 |
|---|---|
| `git init` | Git 저장소 초기화 |
| `git status` | 변경 사항 확인 |
| `git add` | 파일을 커밋 대상으로 등록 |
| `git commit` | 변경 사항 기록 |
| `git branch -M main` | 브랜치 이름 변경 |
| `git remote add origin` | 원격 저장소 연결 |
| `git pull --rebase` | 원격 변경 사항을 가져와 로컬 작업과 재적용 |
| `git push -u origin main` | 원격 저장소에 업로드 및 추적 브랜치 설정 |

---

# 5. 최종 프로젝트 디렉터리 구조

```text
E1-1/
│
├── E1-1-nginx/
│   ├── Dockerfile
│   └── index.html
│
└── practice/
    └── memo.txt
```

### 파일별 역할

- `E1-1-nginx/`: Docker 및 Nginx 웹 서버 실습 프로젝트
- `Dockerfile`: Nginx 기반 Docker 이미지 생성 설정
- `index.html`: 직접 작성한 웹페이지
- `practice/`: Linux 파일 관리 실습 공간
- `memo.txt`: Linux 파일 생성 및 내용 작성 실습 파일

---

# 6. GitHub 저장소 관리

### GitHub 저장소

https://github.com/KIMDABHIN/ALL_E1-1

### Git 저장소 설정

```bash
git config --global user.name "KIMDABHIN"
git config --global user.email "hansa302@daum.net"
```

### 프로젝트 업로드 과정

```bash
git init
git add E1-1-nginx practice
git commit -m "Initial commit: E1-1 Docker and Linux practice"
git branch -M main
git remote add origin https://github.com/KIMDABHIN/ALL_E1-1.git
git pull --rebase origin main
git push -u origin main
```

처음 업로드할 때 원격 저장소에 이미 존재하던 커밋으로 인해 Push가 거절되는 상황이 발생했습니다.

`git pull --rebase origin main` 명령어로 원격 저장소의 내용을 먼저 반영한 후 다시 Push하여 정상적으로 업로드했습니다.

최종 업로드 결과:

```text
2b3bd80..972356a  main -> main
branch 'main' set up to track 'origin/main'.
```

이를 통해 로컬 프로젝트와 GitHub 원격 저장소의 연결 및 업로드가 완료되었습니다.

---

# 7. 최종 수행 결과

| 미션 | 수행 내용 | 결과 |
|---|---|---|
| Mission 1 | WSL2 및 Ubuntu 환경 구축 | 완료 |
| Mission 2 | Linux 기본 명령어 및 파일 관리 | 완료 |
| Mission 3 | Linux 파일 권한 관리 | 완료 |
| Mission 4 | Docker 설치 및 컨테이너 관리 | 완료 |
| Mission 5 | Dockerfile 및 Nginx 웹 서버 구축 | 완료 |
| Mission 6 | Bind Mount 실습 | 완료 |
| Mission 7 | Docker Volume 및 데이터 영속성 확인 | 완료 |
| GitHub | 프로젝트 원격 저장소 업로드 | 완료 |

---

# 8. 프로젝트를 통해 배운 점

이번 실습을 통해 개발 환경을 구축하는 과정부터 Linux 명령어를 활용한 파일 관리, Docker를 이용한 컨테이너 실행까지 개발 워크스테이션의 기본적인 구조를 경험했습니다.

특히 Dockerfile을 직접 작성하고 Nginx 웹 서버를 실행하면서 컨테이너가 단순히 프로그램을 실행하는 공간이 아니라, 애플리케이션을 독립적인 환경에서 실행하고 관리할 수 있도록 도와주는 기술이라는 점을 이해했습니다.

또한 Bind Mount와 Docker Volume을 각각 실습하면서 호스트의 파일을 컨테이너와 공유하는 방식과 컨테이너가 달라져도 데이터를 유지하는 방식의 차이를 확인했습니다.

마지막으로 Git과 GitHub를 이용해 실습 결과물을 원격 저장소에 업로드하면서 개발 과정에서 버전 관리와 작업 기록을 남기는 것이 중요하다는 점도 배웠습니다.

이번 프로젝트는 Linux와 Docker의 기초를 직접 실행하고 확인하면서 개발 환경에 대한 이해도를 높이는 실습이었습니다.

---

