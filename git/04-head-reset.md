# HEAD와 git reset

## HEAD란?

- HEAD는 **지금 내가 있는 위치**를 가리킨다.
- 보통 HEAD → 브랜치(main) → 브랜치의 최신 커밋 순서로 가리킨다.
- HEAD가 가리키는 커밋을 기준으로 working directory가 구성된다.

## git reset

- reset을 하면 **HEAD와 HEAD가 가리키는 브랜치가 함께** 과거 커밋으로 이동한다.
- 옵션에 따라 working tree, staging area까지 되돌릴지 정할 수 있다.

### 3가지 옵션

Git에는 3가지 영역(working tree, staging area, repository)이 있고, 옵션에 따라 되돌리는 범위가 다르다.

| 옵션 | repository (HEAD + 브랜치) | staging area | working tree |
|---|---|---|---|
| `--soft` | 이동 | 그대로 | 그대로 |
| `--mixed` (기본값) | 이동 | 되돌림 | 그대로 |
| `--hard` | 이동 | 되돌림 | 되돌림 |

- `--soft`: 커밋만 취소. 변경 내용은 add된 상태로 남아서 바로 다시 커밋할 수 있다.
- `--mixed`: 커밋 + add 취소. 변경 내용은 파일에 남아 있다. 옵션 없이 `git reset`만 치면 이게 실행된다.
- `--hard`: 파일 내용까지 그 커밋 시점으로 되돌린다.

### --hard 사용 시 주의

- **커밋하지 않은 수정 사항**과 **add만 한 내용**은 복구할 수 없다.
- 커밋해 둔 내용은 사라지지 않고 `git reflog`로 복구할 수 있다.
- reset 전에 `git status`로 커밋 안 한 변경이 없는지 확인하는 습관을 들이자.

## 이동할 커밋 지정하기

예시: 커밋이 6개 있고, HEAD는 6번 커밋을 가리키는 상태.

```
1 - 2 - 3 - 4 - 5 - 6   ← HEAD
```

5번 커밋으로 되돌리고 싶다면 **이동할 커밋(5번)의 ID**를 적는다.

```bash
git reset --hard [5번 커밋 ID]
```

- ⚠️ 지우려는 커밋(6번)의 ID를 적으면 6번에 그대로 머문다. reset은 "적은 커밋으로 이동"하는 명령어라, **적은 커밋은 남고 그 이후 커밋만** 빠진다.

커밋 ID 대신 HEAD 기준으로 적을 수도 있다.

```bash
git reset --hard HEAD^     # 바로 이전 커밋 (5번)
git reset --hard HEAD~1    # HEAD^와 같음
git reset --hard HEAD~2    # 전전 커밋 (4번)
```

## reset으로 사라진 커밋 되돌리기

reset으로 빠진 커밋은 삭제된 게 아니라 가리키는 브랜치가 없어서 안 보일 뿐이다.

```bash
git reflog                  # HEAD가 거쳐 간 기록에서 커밋 ID 찾기
git reset --hard [커밋 ID]  # 그 커밋으로 다시 이동
```

## 사용 규칙

- **push 전** (내 로컬에만 있는 커밋) → reset 사용 가능
- **push 후** (팀원과 공유된 커밋) → reset 대신 `git revert` 사용 (→ `11-blame-revert.md`)
- ⚠️ 적는 커밋 ID가 반대다.
  - `reset` → **이동할(남길)** 커밋 ID
  - `revert` → **취소할** 커밋 ID
