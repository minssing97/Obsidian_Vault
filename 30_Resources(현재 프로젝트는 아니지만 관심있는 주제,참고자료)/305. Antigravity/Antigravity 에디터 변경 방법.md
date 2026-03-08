---
title: "Antigravity 에디터 변경 방법"
source: "https://chatgpt.com/c/69a7ef81-a26c-83a5-ab83-b51b225a41e1"
author:
  - "[[ChatGPT]]"
published:
created: 2026-03-04
description: "ChatGPT는 매일의 일상을 위한 AI 챗봇입니다. 최첨단 AI와 대화하며 다양한 아이디어를 탐색하고, 문제를 해결하고, 더 빨리 학습하세요."
tags:
  - "clippings"
---
antigravity에서 특정 파일 형식의 editor를 변경하는 방법은?

---

Antigravity는 VS Code 계열이라서(설정/프로필/확장 생태계가 유사) \*\*“특정 확장자(파일 형식)를 어떤 ‘에디터(뷰)’로 열지”\*\*를 `workbench.editorAssociations` 로 매핑하는 방식이 가장 정석입니다.

## 1) Antigravity 내부에서 “특정 파일 형식 → 에디터(뷰) 변경”

### A. 설정 UI로 하는 법

1. Antigravity에서 **Settings 열기**
	- 단축키: **Cmd +,** (Mac) / 보통 Windows는 **Ctrl +,**
2. 검색창에 **“editor associations”** 또는 **“workbench.editorAssociations”** 입력
3. **Add Item** (또는 JSON 편집)에서
	- **파일 패턴(예: `*.md`, `*.csv`)**
	- **연결할 에디터 ID(예: 기본 Text Editor, Markdown Preview 등)**  
		를 지정합니다.

### B. settings.json으로 바로 설정(추천)

1. Command Palette 열기: **F1** (또는 Cmd/Ctrl+Shift+P)
2. **“Open User Settings (JSON)”** 선택
3. 아래처럼 추가/수정:
- `*.md` 를 **Markdown Preview(미리보기 에디터)** 로 강제하는 예시입니다.
- `"default"` 는 일반 텍스트 에디터(기본 편집기) 쪽으로 두는 의미로 쓰입니다.
- 에디터 ID는 설치된 확장/기능에 따라 달라질 수 있어서, 설정 UI에서 선택 목록이 뜨면 그걸 고르는 게 가장 안전합니다.

## 2) “에디터”가 아니라 “언어 모드(하이라이트)”만 바꾸고 싶은 경우

예: `.h` 를 C가 아니라 C++로 인식하게 하고 싶다  
→ 이건 `files.associations` 를 씁니다.

## 3) (참고) OS에서 더블클릭 시 “기본 앱을 Antigravity로” 바꾸는 것이라면

이건 Antigravity 내부 설정이 아니라 **Windows 기본 앱/파일 연결** (또는 macOS “정보 가져오기 → 다음으로 열기”)에서 확장자별 기본 앱을 바꾸는 영역입니다. (설치 단계에서 특정 확장자를 Antigravity에 등록하는 옵션을 언급하는 가이드들도 있습니다. )

---

**Q1**

**지금 바꾸려는 게 “Antigravity 안에서 열리는 뷰(미리보기 vs 텍스트)”야, 아니면 “윈도우에서 더블클릭 기본 실행 앱”이야?**

**Q2**

**바꾸려는 확장자(예:.md,.csv,.ipynb,.sql)는 뭐고, 원하는 에디터/뷰는 어떤 형태(미리보기/전용 확장 에디터/텍스트)야?**

**Q3**

**현재 Antigravity에서 해당 파일을 열었을 때 오른쪽 아래(언어 모드 표시)와, “Reopen With(다른 에디터로 다시 열기)” 메뉴가 보이는지 확인해볼래?**