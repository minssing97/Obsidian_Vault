---
title: Git 기본 명령어
source: https://gemini.google.com/app/8e8e515a0d4fc574?is_sa=1&is_sa=1&android-min-version=301356232&ios-min-version=322.0&campaign_id=bkws&utm_source=sem&utm_medium=paid-media&utm_campaign=bkws&pt=9008&mt=8&ct=p-growth-sem-bkws&gclsrc=aw.ds&gad_source=1&gad_campaignid=20437330476&gbraid=0AAAAApk5BhkH8EKSyk9w5lo13pAcjs6GD&gclid=Cj0KCQiAtfXMBhDzARIsAJ0jp3CYOaGHS9W8gSgyxZ8FyTQnTiqabFQbib8N6Hg3KOZDITSNCCAqotgaAjRHEALw_wcB
author:
  - "[[Gemini]]"
published:
created: 2026-02-25
description: Google의 AI 어시스턴트인 Gemini를 만나 보세요. 글을 쓰고, 계획하고, 브레인스토밍하는 등 다양한 상황에서 도움을 받을 수 있습니다. 생성형 AI의 강력한 기능을 경험해 보세요.
tags:
  - clippings
---
## \[최초 1회\] 내 정보 등록하기

 git config --global user.name "내 이름"
 git config --global user.email "내 이메일"

## \[프로젝트 1회\] 내 정보 등록하기
##   create a new repository on the command line

git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/minssing97/hwpx-local-claude.git
git push -u origin main


---
## \[그 다음부터는\] 내 정보 등록하기

git add .
git commit -m "수정 내용 요약"
git push

---

### 1\. \[최초 1회\] 내 정보 등록하기

Git을 설치한 후, 누가 코드를 수정했는지 기록하기 위해 이름과 이메일을 등록해야 합니다. (전역 설정)

Bash

```
git config --global user.name "내 이름"
git config --global user.email "내 이메일"
```

> **Tip:** 이름은 영문으로, 이메일은 GitHub 계정과 동일하게 설정하는 것이 좋습니다.

---

### 2\. \[새 프로젝트 시작\] 저장소 만들기

새로운 폴더에서 작업을 시작하거나, 기존 폴더를 Git으로 관리하고 싶을 때 실행합니다.

Bash

```
# 1. 작업할 폴더로 이동 (이미 있다면 생략)
cd 프로젝트_폴더_경로

# 2. Git 저장소로 초기화 (가장 중요!)
git init
```

이 명령어를 입력하면 폴더 안에 숨겨진 `.git` 폴더가 생기며, 이때부터 Git이 파일의 변화를 감시하기 시작합니다.

---

### 3\. \[첫 저장\] 파일 기록하기

파일을 만들고 나서 "이 상태를 저장하겠다"라고 확정 짓는 루틴입니다.

Bash

```
# 1. 현재 상태 확인 (어떤 파일이 변했나?)
git status

# 2. 저장할 파일 선택 (장바구니에 담기)
git add .

# 3. 저장 확정 (메시지와 함께 기록)
git commit -m "First Commit (첫 저장)"
```

---

### 4\. \[GitHub 연결\] 온라인에 올리기

내 컴퓨터의 기록을 GitHub 같은 원격 저장소로 보낼 때 사용합니다. (GitHub에서 리포지토리를 먼저 만든 후 실행)

Bash

```
# 1. 내 컴퓨터와 GitHub 저장소 연결
git remote add origin https://github.com/내계정/저장소이름.git

# 2. 처음으로 업로드하기
git push -u origin main
```

---

**다음 단계로 무엇을 도와드릴까요?**지금 바로 테스트해 보실 수 있도록, 현재 개발 중이신 **주식 대시보드** 나 **블로그 생성 도구** 프로젝트 폴더에서 위 명령어들을 적용해 보시겠어요? 혹은 GitHub 연동 과정에서 인증 오류가 난다면 바로 해결해 드릴 수 있습니다.