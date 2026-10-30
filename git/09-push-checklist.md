# push 전 체크리스트

push한 커밋은 고치기 어렵다. 그래서 **push 전에 확인하고, 문제가 있으면 push 전에 고친다.**

## 추천 순서

```bash
git add .
git status            # 1. 원하는 파일만 올라갔는지
git diff --staged     # 2. 올라간 내용 확인 (q로 나가기)
git commit -m "..."
git hist              # 3. 커밋 메시지 오타 확인
git commit --amend -m "..."   # (오타 있으면) 메시지 고치기
git push
```

## 단계별로 확인할 것

| 단계 | 확인할 것 | 명령어 |
|---|---|---|
| add 후 | 올라간 파일과 내용이 맞나? | `git status`, `git diff --staged` |
| commit 후 | 커밋 메시지 오타 없나? | `git hist` (= `git log --pretty=oneline`) |

- add 단계에서는 아직 커밋이 없어서 `git hist`에 새로 보이는 게 없다. 이때는 **내용**을 확인한다.
- `git diff` → 아직 add **안 한** 변경 내용
- `git diff --staged` → add **한** 변경 내용

## git status 색깔

| 색 | 위치 | 의미 |
|---|---|---|
| 빨간색 | working tree | 아직 add 안 함 |
| 초록색 | staging area | add 완료, 커밋 준비됨 |

## push 후에 오타를 발견했다면

| 상황 | 방법 |
|---|---|
| 팀 저장소 / 공용 브랜치 | 그냥 둔다. 내용을 취소해야 하면 `git revert` |
| 나만 쓰는 저장소 / 내 작업 브랜치 | `git commit --amend` 후 `git push --force-with-lease` |

- 공용 브랜치에서 force push는 금지. 이미 pull한 팀원의 기록이 꼬인다.
- 회사에서는 main, dev 같은 브랜치에 force push를 아예 막아 두는 경우가 많다.

## 깔끔한 커밋 히스토리란?

오타 하나보다 이런 게 더 문제다.

- "수정", "ㅇㅇ", "다시" 같은 의미 없는 커밋 메시지
- 한 커밋에 여러 기능을 뭉쳐 넣은 것
- 쓸데없는 머지 커밋이 잔뜩 쌓인 것

→ 커밋은 **주제별로 작게**, 메시지는 **무엇을 했는지 알 수 있게** 쓴다.
