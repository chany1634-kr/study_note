# Git 기본 명령어

## 1. 저장소 만들기

```bash
git init
```

- 현재 폴더를 Git이 관리하는 프로젝트 폴더(working directory)로 설정한다.
- 폴더 안에 숨겨진 `.git` 폴더(레포지토리)가 생성된다.

## 2. 사용자 정보 설정

커밋할 때 "누가 커밋했는지" 기록하기 위해 필요하다.

```bash
git config user.name "이름"
git config user.email "이메일"
```

| 옵션 | 적용 범위 |
|---|---|
| 옵션 없음 | 현재 저장소에만 적용 |
| `--global` | 내 컴퓨터의 모든 저장소에 적용 |

```bash
git config --global user.name "이름"    # 보통 이렇게 한 번만 설정해 둔다
```

## 3. staging area에 올리기 / 내리기

```bash
git add [파일 이름]     # 특정 파일만 올리기
git add [폴더 이름]     # 해당 폴더 안의 수정된 파일 전부 올리기
git add .              # 지금 폴더(.)와 하위 폴더의 수정된 파일 전부 올리기
```

- `.`은 Git 기호가 아니라 터미널에서 **"지금 내가 있는 폴더"**라는 뜻이다. (`..`은 한 단계 바깥 폴더)
- `git add .`은 원치 않는 파일(예: `.DS_Store`)까지 올릴 수 있으니 add 후 `git status`로 확인한다. → `15-gitignore.md`

```bash
git reset [파일 이름]            # staging area에서 다시 내리기
git restore --staged [파일 이름]  # 같은 기능 (최신 방식)
```

- 내려도 파일 수정 내용은 그대로 남아 있다. staging area에서만 빠진다.

## 3-1. 수정한 파일 되돌리기 (수정 내용 버리기)

아직 커밋 안 한 수정을 **없던 일로** 만들고, 마지막 커밋(또는 add) 상태로 돌린다.

```bash
git restore [파일 이름]          # 최신 방식
git checkout -- [파일 이름]      # 예전 방식 (같은 기능)
```

예시: `hello.py`를 이것저것 고쳤는데 망해서 원래대로 돌리고 싶을 때

```
커밋된 내용:  print("hello")
지금 파일:    print("hello")
              print("이상하게 고친 코드")   ← 커밋 안 한 수정
```

`git restore hello.py` 후

```
되돌린 후:    print("hello")
```

- ⚠️ 버린 수정 내용은 **복구할 수 없다.** 커밋한 적이 없어서 `git reflog`에도 남지 않는다.
- `git status`에 나오는 `(use "git restore <file>..." to discard changes ...)` 안내가 이 명령어다. **discard = 버리다.**
- 예전에는 `git checkout`이 브랜치 이동과 파일 되돌리기를 둘 다 해서, `git checkout test`(이동)와 `git checkout -- test`(되돌리기)를 헷갈려 작업을 날리는 일이 있었다. 그래서 `switch`와 `restore`로 나뉘었다. → `06-branch.md`

### 헷갈리는 restore 두 개

| 명령어 | 하는 일 | 수정 내용 |
|---|---|---|
| `git restore --staged [파일]` | staging area에서 **내리기만** | 남아 있음 ✅ |
| `git restore [파일]` | 수정한 내용 **버리기** | 사라짐 ⚠️ |

- `--staged`가 붙으면 안전, 안 붙으면 위험이라고 기억하자.

## 4. 상태 확인

```bash
git status
```

- 지금 어떤 파일이 수정됐는지, staging area에 뭐가 올라가 있는지 보여준다.
- 문제가 생겼을 때 **가장 먼저 쳐보는 명령어.**

| 표시 | 의미 |
|---|---|
| 빨간색 (Untracked / Changes not staged) | working tree에만 있음. 아직 add 안 함 |
| 초록색 (Changes to be committed) | staging area에 올라감. commit 준비 완료 |

## 5. 커밋하기

```bash
git commit -m "커밋 메시지"
```

- staging area에 있는 내용을 커밋으로 남긴다. (로컬 레포지토리에 저장)
- GitHub에 올리려면 이후 `git push`를 해야 한다.

## 6. 도움말 보기

```bash
git help [명령어 이름]
```

- 궁금한 명령어의 공식 매뉴얼을 보여준다. (예: `git help commit`)
- 매뉴얼 화면에서 나가려면 `q`를 누른다.
