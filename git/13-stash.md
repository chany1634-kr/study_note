# git stash

## 언제 쓰나?

아직 커밋하지 않은 작업이 있는데 **다른 브랜치로 가야 할 때.**

- 그냥 commit하고 이동 → 미완성 작업이 불필요한 커밋으로 남는다.
- 커밋 없이 이동 → 이동이 막히거나, 작업이 다른 브랜치에 섞일 수 있다.
- 그래서 stash로 **잠깐 치워두고** 이동한 뒤, 돌아와서 다시 꺼낸다.

예: 작업 중에 다른 브랜치로 긴급하게 가서 버그를 고쳐야 할 때

## 기본 사용법

```bash
git stash              # 작업 내용을 임시 저장 → working tree는 최근 커밋 상태로 깨끗해짐
git switch hotfix      # 다른 브랜치로 가서 작업
git switch premium     # 원래 브랜치로 돌아와서
git stash pop          # 임시 저장한 작업 꺼내기
```

- stash한 내용은 **stack**(쌓아두는 목록)에 저장된다. 가장 최근 것이 맨 위.
- ⚠️ 기본으로는 **Git이 이미 관리하는 파일의 변경**만 저장된다. 새로 만든 파일(Untracked)까지 넣으려면 `git stash -u`

## 꺼내기: pop vs apply

| 명령어 | 꺼낸 뒤 stash 목록 |
|---|---|
| `git stash pop` | **지워짐** (= apply + drop) |
| `git stash apply` | **남아 있음** |

- 보통은 `pop`을 쓴다.
- `apply`는 목록에 계속 남으니까, 다 쓰면 `drop`으로 정리한다.
- 꺼낼 때도 같은 곳을 바꿨으면 충돌이 날 수 있다. 충돌이 나면 pop이어도 목록에서 지워지지 않는다.

## 목록 보기와 지우기

```bash
git stash list                # 저장된 목록 보기
# stash@{0}: WIP on premium: ...   ← 가장 최근
# stash@{1}: WIP on premium: ...

git stash apply stash@{1}     # 특정 번호 꺼내기
git stash drop stash@{1}      # 특정 번호 지우기
git stash pop stash@{1}       # 특정 번호 꺼내고 지우기
```

| 명령어 | 하는 일 | 번호 생략하면 |
|---|---|---|
| `git stash` | 작업 내용 임시 저장 | - |
| `git stash list` | 저장된 목록 조회 | - |
| `git stash apply [번호]` | 적용 (목록에 남음) | 가장 최근 것 |
| `git stash drop [번호]` | 삭제 | 가장 최근 것 |
| `git stash pop [번호]` | 적용 + 삭제 | 가장 최근 것 |

- 번호는 `git stash list`로 먼저 확인하고 쓴다.
- 하나를 지우면 뒤 번호가 당겨진다. (stash@{2} → stash@{1})

## 잘못된 브랜치에서 작업했을 때

```bash
git stash              # 잘못된 브랜치에서 작업 치워두기
git switch premium     # 원래 작업할 브랜치로 이동
git stash pop          # 여기서 꺼내기
```

- stash는 브랜치에 묶여 있지 않아서, 다른 브랜치에서 꺼낼 수 있다.

## 팁

- 짧게 자리 비울 때 → stash
- 오래 비울 때 → 임시 커밋이 더 안전하다. (stash는 쌓이면 뭐가 뭔지 잊어버리기 쉽다)
