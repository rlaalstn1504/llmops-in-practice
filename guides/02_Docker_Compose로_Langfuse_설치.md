# Docker Compose로 Langfuse 내 컴퓨터(서버)에 설치하기

Langfuse는 클라우드(https://cloud.langfuse.com)로 쓸 수도 있지만, 오픈소스라서 내 컴퓨터나 회사 서버에 직접 설치해 쓸 수도 있습니다. 공식 저장소에 들어 있는 `docker-compose.yml` 하나로 필요한 서비스(웹, 데이터베이스 등)가 한꺼번에 실행됩니다.

## 준비

- Docker Desktop(Windows·macOS) 또는 Docker Engine + Compose 플러그인(Linux)
- Git

## 설치와 실행

```bash
git clone https://github.com/langfuse/langfuse.git
cd langfuse
docker compose up -d
```

- 처음 실행할 때는 여러 컨테이너 이미지를 내려받아 수 분에서 수십 분이 걸립니다.
- 모든 컨테이너가 뜨면 브라우저에서 http://localhost:3000 으로 접속해 회원가입하고 프로젝트를 만듭니다.
- 프로젝트 설정에서 API 키를 발급받아 `.env`에 넣고, `LANGFUSE_HOST=http://localhost:3000`으로 바꾸면 노트북 실습을 내 Langfuse로 그대로 할 수 있습니다.

## 자주 쓰는 명령

```bash
docker compose ps        # 실행 상태 확인
docker compose logs -f   # 로그 보기
docker compose down      # 중지 (데이터는 유지)
```

공식 문서: https://langfuse.com/self-hosting
