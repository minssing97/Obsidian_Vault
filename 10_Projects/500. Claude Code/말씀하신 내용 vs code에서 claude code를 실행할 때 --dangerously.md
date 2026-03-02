---
title: "말씀하신 내용 vs code에서 claude code를 실행할 때 --dangerously..."
source: "https://gemini.google.com/app/f04206a24ecb06c1?is_sa=1&is_sa=1&android-min-version=301356232&ios-min-version=322.0&campaign_id=bkws&utm_source=sem&utm_medium=paid-media&utm_campaign=bkws&pt=9008&mt=8&ct=p-growth-sem-bkws&gclsrc=aw.ds&gad_source=1&gad_campaignid=20437330476&gbraid=0AAAAApk5BhkH8EKSyk9w5lo13pAcjs6GD&gclid=Cj0KCQiAtfXMBhDzARIsAJ0jp3CYOaGHS9W8gSgyxZ8FyTQnTiqabFQbib8N6Hg3KOZDITSNCCAqotgaAjRHEALw_wcB"
author:
  - "[[Gemini]]"
published:
created: 2026-02-25
description: "Google의 AI 어시스턴트인 Gemini를 만나 보세요. 글을 쓰고, 계획하고, 브레인스토밍하는 등 다양한 상황에서 도움을 받을 수 있습니다. 생성형 AI의 강력한 기능을 경험해 보세요."
tags:
  - "clippings"
---
vs code에서 claude code를 실행할 때 --dangerously-skip-permissions 같은 옵션은 어떻게 주면 되?

---

VS Code 터미널에서 `claude-code` 를 실행할 때 옵션을 추가하는 방법은 아주 간단합니다. 일반적인 CLI(커맨드 라인 인터페이스) 도구들과 마찬가지로, 실행 명령어 뒤에 공백을 두고 옵션을 붙여주시면 됩니다.

## 🛠️ 실행 방법

터미널(Terminal) 창을 열고 아래와 같이 입력하세요:

Bash

```
claude --dangerously-skip-permissions
```

이 옵션을 사용하면 Claude가 파일을 읽거나 수정할 때 매번 사용자에게 허가를 구하지 않고 **즉시 작업을 수행** 합니다.

---

### ⚠️ 주의사항 (꼭 읽어주세요!)

이름부터 \*\*"Dangerously"\*\*가 들어가는 만큼, 이 옵션을 사용할 때는 몇 가지 리스크를 인지하셔야 합니다:

- **자동 승인:** Claude가 코드를 대량으로 삭제하거나 중요한 설정 파일을 수정해도 묻지 않고 진행합니다.
- **권장 환경:** 반드시 **Git 같은 버전 관리 시스템** 이 적용된 프로젝트에서 사용하세요. 잘못된 수정이 발생했을 때 바로 `git restore` 로 되돌릴 수 있어야 안전합니다.
- **보안:** 신뢰할 수 없는 프롬프트나 외부 스크립트를 Claude에게 분석시킬 때는 이 옵션을 끄는 것이 좋습니다.

### 💡 팁: 다른 유용한 옵션들

자주 함께 쓰이는 옵션들도 참고해 보세요:

| 옵션 | 설명 |
| --- | --- |
| `--model <model_name>` | 사용할 특정 모델을 지정합니다. |
| `--print` | 대화형 모드 대신 결과를 한 번 출력하고 종료합니다. |
| `--help` | 사용 가능한 모든 옵션 목록을 확인합니다. |

---

**혹시 특정 작업을 자동화하기 위해 이 옵션을 찾으시는 건가요?** 원하신다면 Claude Code를 특정 파일 범위 내에서만 작동하도록 제한하는 설정법도 알려드릴 수 있습니다.

---

알려줘

---

Claude Code가 프로젝트 전체를 헤집어 놓는 게 걱정된다면, **파일 범위를 제한하거나 특정 파일에 접근하지 못하도록** 설정하는 것이 가장 깔끔합니다.

`--dangerously-skip-permissions` 옵션을 쓰더라도 아래 방법들을 병행하면 훨씬 안전하게 자동화를 맡길 수 있습니다.

---

### 1..claudeignore 파일 활용 (가장 추천)

`.gitignore` 와 똑같은 방식입니다. Claude가 건드리지 말아야 할 폴더나 파일을 이 파일에 적어두면, 아예 **인식조차 못 하게** 격리할 수 있습니다.

- 프로젝트 루트에 `.claudeignore` 파일을 만듭니다.
- 제외할 항목을 입력합니다:
	Plaintext
	```
	# 중요 설정 파일 제외
	.env
	config/secrets.json
	# 대용량 로그 및 빌드 파일 제외
	logs/
	dist/
	# 특정 문서 제외
	private_notes.md
	```

### 2\. 실행 시 파일 경로 직접 지정

명령어를 실행할 때 특정 파일이나 디렉토리만 인자로 넘겨주면, Claude는 해당 범위 내의 컨텍스트에 집중합니다.

Bash

```
# 특정 폴더만 대상으로 실행
claude src/components/ --dangerously-skip-permissions

# 특정 파일들만 지정해서 실행
claude main.py utils.py --dangerously-skip-permissions
```

### 3\. Read-Only 모드로 먼저 확인하기

삭제나 수정 권한을 주기 전에 내용만 읽게 하고 싶다면 `--read-only` 옵션을 섞어보세요.

Bash

```
claude --read-only
```

이 상태로 먼저 대화하며 계획을 짠 뒤, 확신이 생겼을 때 `exit` 후 `--dangerously-skip-permissions` 를 붙여서 다시 실행하는 방식이 실무에서 가장 안전합니다.

---

### 💡 한 걸음 더 나아가기

매번 긴 옵션을 치기 귀찮다면, VS Code가 설정된 터미널(zsh, bash 등)의 설정 파일에 \*\*별칭(Alias)\*\*을 등록해 두는 것도 방법입니다.

- **설정 예시 (alias):**`alias cld='claude --dangerously-skip-permissions'` *(이제 터미널에 `cld` 만 쳐도 옵션이 자동 적용되어 실행됩니다.)*

혹시 \*\*특정 파일 형식(예:.js 파일만 수정)\*\*만 골라서 작업을 시키고 싶은 구체적인 시나리오가 있으신가요? 상황에 맞는 필터링 방법을 더 자세히 알려드릴 수 있습니다.