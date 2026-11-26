# GCP VM 인스턴스 만들고 SSH로 원격 접속하기

클라우드 서버(GCP Compute Engine)에 VM을 만들고, 내 PC에서 SSH 키로 접속한 뒤 VS Code로 원격 개발하는 방법입니다.

## 1. VM 인스턴스 만들기

1. https://console.cloud.google.com 에서 프로젝트를 선택하고 **Compute Engine > VM 인스턴스 > 인스턴스 만들기**로 이동합니다.
2. 리전과 머신 유형을 고릅니다.
   - GPU가 필요하면 **GPU 머신**(예: NVIDIA L4 + `g2-standard` 계열)을 선택합니다. 비용이 크므로 실습이 끝나면 바로 중지하거나 삭제하세요.
   - 실습용 서버라면 GPU 없는 일반 머신으로도 충분합니다.
3. 부팅 디스크는 **Ubuntu**를 선택하고 만들기를 누릅니다.
4. 생성이 끝나면 목록에서 **외부 IP**를 확인합니다.

> VM은 켜져 있는 시간만큼 비용이 나갑니다. 쓰지 않을 때는 **중지**, 더 이상 필요 없으면 **삭제**하세요.

## 2. SSH 키 만들기 (내 PC)

GCP는 보안 때문에 아이디와 IP만으로는 접속을 허용하지 않습니다. 내 PC에서 키 쌍(개인 키 + 공개 키)을 만들고, 공개 키를 GCP에 등록해야 접속할 수 있습니다.

```bash
ssh-keygen -t ed25519 -C "<GCP에서 쓸 사용자 이름>" -f ~/.ssh/gcp_key
```

- `~/.ssh/gcp_key`: 개인 키. 절대 공유하지 않습니다.
- `~/.ssh/gcp_key.pub`: 공개 키. GCP에 등록합니다.
- `-C` 뒤에 적은 이름이 VM의 **사용자 계정 이름**이 됩니다. 접속할 때 같은 이름을 써야 합니다.

## 3. 공개 키를 VM에 등록하기

1. VM 인스턴스 상세 화면에서 **수정**을 누릅니다.
2. **보안 및 액세스 > SSH 키 > 항목 추가**에 `gcp_key.pub` 파일 내용을 통째로 붙여 넣고 저장합니다.
3. 팀원이 함께 쓰는 서버라면 팀원 각자의 공개 키를 모두 등록합니다.

## 4. 터미널로 접속하기

```bash
ssh -i ~/.ssh/gcp_key <사용자 이름>@<외부 IP>
```

처음 접속할 때 나오는 확인 질문에는 `yes`를 입력합니다.

## 5. VS Code Remote-SSH로 접속하기

1. VS Code 확장 **Remote - SSH**를 설치합니다.
2. `F1` > **Remote-SSH: Open SSH Configuration File**에서 설정 파일을 열고 아래처럼 저장합니다.

```
Host gcp
    HostName <외부 IP>
    User <사용자 이름>
    IdentityFile ~/.ssh/gcp_key
    Port 22
```

3. `F1` > **Remote-SSH: Connect to Host** > `gcp`를 선택하면 새 창에서 서버에 접속됩니다. 첫 접속에는 서버에 VS Code 서버를 설치하느라 시간이 조금 걸립니다.
4. 이후에는 로컬에서 코딩하듯이 서버의 파일을 열고 터미널을 쓰면 됩니다.
