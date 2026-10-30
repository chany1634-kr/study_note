# study_note

공부하면서 정리한 노트 모음

## Git

> 빠르게 찾아보려면 → [16. 명령어 총정리](git/16-cheatsheet.md)

### 기초

| 번호 | 노트 | 내용 |
|---|---|---|
| 01 | [기본 명령어](git/01-basics.md) | init, config, add, status, commit, help |
| 02 | [작동 흐름](git/02-workflow.md) | working tree → staging area → repository → remote |
| 03 | [커밋 히스토리](git/03-history.md) | log, show, diff, amend, alias, --graph |
| 04 | [HEAD와 reset](git/04-head-reset.md) | reset 3가지 옵션, reflog 복구 |
| 05 | [태그](git/05-tag.md) | tag, 태그 push |

### 브랜치

| 번호 | 노트 | 내용 |
|---|---|---|
| 06 | [브랜치](git/06-branch.md) | branch, switch, checkout, switch vs reset vs revert |
| 07 | [merge와 conflict](git/07-merge-conflict.md) | 3-way merge, 충돌 해결, --abort |

### GitHub · 협업

| 번호 | 노트 | 내용 |
|---|---|---|
| 08 | [리모트와 origin](git/08-remote-origin.md) | remote add, push -u, tracking, clone |
| 09 | [push 전 체크리스트](git/09-push-checklist.md) | push 전 확인 순서, diff vs diff --staged |
| 10 | [pull과 fetch](git/10-pull-fetch.md) | push 거절, pull = fetch + merge |

### 실전

| 번호 | 노트 | 내용 |
|---|---|---|
| 11 | [blame과 revert](git/11-blame-revert.md) | 줄별 작성자, push한 커밋 취소 |
| 12 | [rebase](git/12-rebase.md) | merge vs rebase, --continue |
| 13 | [stash](git/13-stash.md) | 임시 저장, pop vs apply |
| 14 | [cherry-pick](git/14-cherry-pick.md) | 필요한 커밋만 가져오기 |
| 15 | [.gitignore](git/15-gitignore.md) | 버전 관리에서 제외할 파일 |
| 16 | [명령어 총정리](git/16-cheatsheet.md) | 전체 요약, 상황별 빠른 찾기 |
