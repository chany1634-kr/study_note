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

> 쉽게 기억하기: `--hard`만 **working directory를 초기화**하고, `--mixed`와 `--soft`는 **working directory를 건드리지 않는다.**

### 활용: 불필요한 커밋 정리하기 (push 전)

ver1을 커밋하고, 이어서 개선한 ver2도 커밋했다. 그런데 ver1 커밋은 기록에 남길 필요가 없다.

```
A - ver1 - ver2   ← HEAD
```

```bash
git reset --soft [A 커밋 ID]    # ver1 이전 커밋으로 이동
git commit -m "Add ver2"
```

```
A - ver2'         ← HEAD
```

- ⚠️ ver1의 ID가 아니라 **ver1 바로 이전 커밋(A)**의 ID를 적는다. (`HEAD~2`라고 써도 된다)
- `--soft`라서 ver1 + ver2의 변경이 add된 상태로 남아 있다. 그래서 `git add` 없이 바로 commit해도 된다.
- 결과적으로 **두 커밋을 하나로 합친 것**이다. ver2가 ver1을 고친 버전이라면 최종 파일은 ver2 내용이 된다.
- `--hard`를 쓰면 ver2 작업까지 파일에서 사라지니 이 상황엔 쓰면 안 된다.

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

- 커밋 ID를 몰라도 괜찮다. `git reflog`에 HEAD가 지금까지 가리켰던 커밋이 전부 나온다.
- 진짜 삭제는 reflog 보관 기간이 지난 뒤 Git이 `git gc`로 알아서 정리한다.

### switch와 돌아오는 법 비교

| | 움직이는 것 | 비유 | 돌아오는 법 |
|---|---|---|---|
| `switch` / `checkout` | HEAD만 | 구경 가기 (브랜치는 제자리) | `git switch master` |
| `reset` | HEAD + 브랜치 | 브랜치를 끌고 감 | `git reflog`로 ID 찾아서 다시 reset |

## push하면 커밋이 완전히 삭제되나?

- 아니다. push는 삭제와 관계없다.
- 이미 push한 커밋을 reset하면 → 로컬이 서버보다 뒤처져서 push가 거절된다.
- `git push --force`로 억지로 올려도 팀원 컴퓨터엔 남아 있고 협업이 꼬여서 거의 금지다.

## 사용 규칙

- **push 전** (내 로컬에만 있는 커밋) → reset 사용 가능
- **push 후** (팀원과 공유된 커밋) → reset 대신 `git revert` 사용 (→ `11-blame-revert.md`)
- ⚠️ 적는 커밋 ID가 반대다.
  - `reset` → **이동할(남길)** 커밋 ID
  - `revert` → **취소할** 커밋 ID

## 한 줄 요약

- 이동 → `switch`
- **커밋했지만 아직 push 안 한** 커밋 취소 → `reset` (soft / mixed / hard)
- push한 커밋 취소 → `revert`
- 커밋도 안 한 수정 사항 되돌리기 → `git restore [파일 이름]`
