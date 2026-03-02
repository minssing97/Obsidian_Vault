---
aliases:
  - openclaw 설치
---
## gog 설치 #gog설치


## 설치(docket 버전) - 다음날 재설치 해야 됨: 설치(new) 참조
#1. 최신 버전의 다운로드 주소를 자동으로 가져와서 다운로드 LATEST_URL=$(curl -s https://api.github.com/repos/steipete/gogcli/releases/latest | grep "browser_download_url.*linux_amd64.tar.gz" | cut -d '"' -f 4) && docker exec -it openclaw-hcjn-openclaw-1 curl -L -o /tmp/gog.tar.gz "$LATEST_URL"

#2. 압축 풀기 (이번에는 파일 크기가 커서 성공할 것입니다) 
docker exec -it openclaw-hcjn-openclaw-1 tar -xzf /tmp/gog.tar.gz -C /tmp

docker exec -it openclaw-hcjn-openclaw-1 ls -F /tmp

#1. 파일을 시스템 실행 경로로 이동 
docker exec -it openclaw-hcjn-openclaw-1 mv /tmp/gog /usr/local/bin/gog 
#2. 실행 권한을 한 번 더 확실히 부여 
docker exec -it openclaw-hcjn-openclaw-1 chmod +x <font color="#ff0000">/usr/local/bin/gog</font> 
#3. 드디어 버전 확인 (이제 숫자가 출력될 것입니다!) 
docker exec -it openclaw-hcjn-openclaw-1 gog --version

## 설치(new)
[[Hostinger  채팅내용]]

지금 상황 정리하면: 어제처럼 **컨테이너 내부**(`/usr/local/bin`)에 `gog`를 넣는 방식은, 컨테이너가 재생성되면(업데이트/재시작/재배포) **그냥 사라져서** 다시 `gog: not found`가 납니다. 그래서 **호스트(VPS)에 설치 → 컨테이너로 마운트**가 정답입니다.

다만 제가 여기서 바로 다운로드/설치를 실행하려고 했는데, 현재 환경 정책상 `curl -L -o ... https://...` 형태의 다운로드 명령 실행이 차단되어 자동으로 내려받아 설치를 못 하고 있어요. 아래 명령은 사용자 쪽에서 VPS에서 그대로 실행해 주세요(호스트에 설치):

```bash
cd /tmp
curl -L -o gogcli.tar.gz https://github.com/steipete/gogcli/releases/download/v0.11.0/gogcli_0.11.0_linux_amd64.tar.gz
tar -xzf gogcli.tar.gz
install -m 0755 gog /usr/local/bin/gog
/usr/local/bin/gog --version
```

설치가 끝나면, OpenClaw 컨테이너가 `gog`를 항상 보게 이렇게 실행만 해주면 됩니다:

```bash
docker exec -it openclaw-hcjn-openclaw-1 sh -lc 'ln -sf /hostbin/gog /usr/local/bin/gog && gog --version'
```

마지막으로 **compose에 마운트 1줄만 추가**하면 영구화됩니다(추가할 항목): 호스트 `/usr/local/bin/gog` → 컨테이너 `/hostbin/gog` (read-only). 지금 Docker Manager에서 `openclaw-hcjn` 편집 화면을 보고 계시니, compose 내용 붙여주시면 제가 정확히 어디에 어떤 줄을 넣을지 딱 맞춰서 작성해드릴게요.
## google 권한 설정 등 참조
[https://gemini.google.com/app/88e1b1faa4d32eff?hl=ko ]

docker exec -it openclaw-hcjn-openclaw-1 gog auth add jamok45@gmail.com --services gmail,calendar,drive,contacts,sheets,docs --remote --step 1

docker exec -it openclaw-hcjn-openclaw-1 gog auth add jamok45@gmail.com --services gmail,calendar,drive,contacts,sheets,docs --remote --step 2 --auth-url '여기에_복사한_주소_붙여넣기'

## 마무리
### docker exec -it openclaw-hcjn-openclaw-1 gog auth list

`Device or resource busy`라는 메시지는 쉽게 말해, **"이 파일은 현재 외부(호스트 VPS)와 단단히 연결되어 있어서, 컨테이너 내부에서 이름을 바꾸거나 옮길 수 없다"**는 뜻입니다.

아까 `docker-compose.yml` 파일의 `volumes:` 섹션에 아래 줄을 추가하셨던 것 기억하시나요?

> `- /usr/local/bin/gog:/usr/local/bin/gog:ro`

#1. 방금 설치한 진짜 파일을 gog.bin으로 이름 변경
docker exec -it openclaw-hcjn-openclaw-1 mv /usr/local/bin/gog /usr/local/bin/gog.bin

1. 비밀번호 '1234'를 품은 새로운 gog 스크립트 만들기
docker exec -it openclaw-hcjn-openclaw-1 sh -c 'printf "#!/bin/bash\nexport GOG_KEYRING_BACKEND=file\nexport GOG_KEYRING_PASSWORD=\"1234\"\n/usr/local/bin/gog.bin \"\$@\"" > /usr/local/bin/gog'

2. 이 스크립트가 실행될 수 있게 권한 주기
docker exec -it openclaw-hcjn-openclaw-1 chmod +x /usr/local/bin/gog