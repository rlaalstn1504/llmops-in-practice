# llmops-in-practice

내 PC에서 잘 돌아가는 LLM 앱을 실제 서비스로 운영하려면 서버, 배포, 모니터링이 필요합니다. 이 저장소는 클라우드 서버 준비부터 LLM 호출 모니터링까지 LLM 서비스 운영에 필요한 실습 자료를 모았습니다.

유튜브 강의: **LLMOps 실전: AI 서비스 배포·운영·모니터링** 재생목록 (링크 추가 예정)

## 구성

| 파일 | 내용 |
|---|---|
| [01_Langfuse로_RAG_모니터링.ipynb](01_Langfuse로_RAG_모니터링.ipynb) | Langfuse 가입과 API 키 설정, CallbackHandler로 RAG 체인 트레이싱, 비용·지연 시간·검색 결과 분석 |
| [guides/01_GCP_VM과_SSH_원격접속.md](guides/01_GCP_VM%EA%B3%BC_SSH_%EC%9B%90%EA%B2%A9%EC%A0%91%EC%86%8D.md) | GCP VM 인스턴스 생성, SSH 키 등록, VS Code Remote-SSH 접속 |
| [guides/02_Docker_Compose로_Langfuse_설치.md](guides/02_Docker_Compose%EB%A1%9C_Langfuse_%EC%84%A4%EC%B9%98.md) | Docker Compose로 Langfuse를 로컬·서버에 직접 설치 |

## 실행 환경

- Python 3.10에서 테스트했습니다.
- 라이브러리 버전에 따라 결과가 달라질 수 있으니 `requirements.txt`로 설치하는 것을 권장합니다.

```bash
python -m venv .venv            # 또는 conda create -n llmops-in-practice python=3.10
pip install -r requirements.txt
```

- `requirements.txt`의 PyTorch는 CUDA 12.1 버전입니다. GPU가 없거나 다른 CUDA 버전을 쓰면 https://pytorch.org 에서 환경에 맞는 설치 명령을 확인하세요.

## API 키 설정

`.env.example`을 복사해 `.env` 파일을 만들고 값을 채우세요. `.env`는 깃허브에 올라가지 않도록 `.gitignore`에 들어 있습니다.

```bash
cp .env.example .env
```


## 문의

강의 문의: rlaalstn1504@naver.com
