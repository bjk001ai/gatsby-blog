---
title: "Git 기초 명령어 완벽 정리 🐙"
date: "2026-05-16"
description: "개발자라면 반드시 알아야 할 Git 기초 명령어를 한눈에 정리합니다."
---

## 들어가며

Git은 개발자라면 반드시 알아야 할 버전 관리 도구입니다.
처음엔 어렵게 느껴지지만, 자주 쓰는 명령어만 알면 충분해요!

---

## Git 기본 흐름

\`\`\`
작업 디렉토리 → (git add) → 스테이징 영역 → (git commit) → 로컬 저장소 → (git push) → 원격 저장소
\`\`\`

---

## 필수 명령어 정리

### 초기 설정

\`\`\`bash
# 사용자 이름 설정
git config --global user.name "내 이름"

# 이메일 설정
git config --global user.email "내이메일@gmail.com"

# 설정 확인
git config --list
\`\`\`

---

### 저장소 생성 & 클론

\`\`\`bash
# 새 저장소 초기화
git init

# 원격 저장소 복제
git clone https://github.com/유저명/저장소명.git
\`\`\`

---

### 변경사항 저장

\`\`\`bash
# 변경된 파일 확인
git status

# 특정 파일 스테이징
git add 파일명

# 전체 파일 스테이징
git add .

# 커밋
git commit -m "커밋 메시지"

# add + commit 한번에
git commit -am "커밋 메시지"
\`\`\`

---

### 원격 저장소 연동

\`\`\`bash
# 원격 저장소 연결
git remote add origin https://github.com/유저명/저장소명.git

# 원격 저장소 확인
git remote -v

# push (업로드)
git push origin main

# pull (다운로드)
git pull origin main
\`\`\`

---

### 브랜치

\`\`\`bash
# 브랜치 목록 확인
git branch

# 브랜치 생성
git branch 브랜치명

# 브랜치 이동
git checkout 브랜치명

# 생성 + 이동 한번에
git checkout -b 브랜치명

# 브랜치 합치기
git merge 브랜치명

# 브랜치 삭제
git branch -d 브랜치명
\`\`\`

---

### 되돌리기

\`\`\`bash
# 스테이징 취소
git restore --staged 파일명

# 변경사항 취소 (마지막 커밋 상태로)
git restore 파일명

# 커밋 되돌리기 (기록 남김)
git revert HEAD

# 커밋 되돌리기 (기록 삭제 ⚠️)
git reset --hard HEAD~1
\`\`\`

---

### 로그 확인

\`\`\`bash
# 커밋 히스토리
git log

# 한 줄로 보기
git log --oneline

# 그래프로 보기
git log --oneline --graph
\`\`\`

---

## 커밋 메시지 잘 쓰는 법 ✍️

| 타입 | 설명 |
|------|------|
| `feat` | 새로운 기능 추가 |
| `fix` | 버그 수정 |
| `docs` | 문서 수정 |
| `style` | 코드 포맷 변경 |
| `refactor` | 리팩토링 |
| `test` | 테스트 추가 |

\`\`\`bash
# 좋은 커밋 메시지 예시
git commit -m "feat: 로그인 기능 추가"
git commit -m "fix: 버튼 클릭 오류 수정"
git commit -m "docs: README 업데이트"
\`\`\`

---

## 결론 💡

> **자주 commit, 자주 push — Git은 습관이에요!**

처음엔 `add → commit → push` 이 세 가지만 익혀도 충분합니다.
브랜치와 merge는 협업할 때 자연스럽게 익혀지니까요 😊