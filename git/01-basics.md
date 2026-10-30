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
git add .              # working directory의 수정된 파일 전부 올리기
```

```bash
git reset [파일 이름]            # staging area에서 다시 내리기
git restore --staged [파일 이름]  # 같은 기능 (최신 방식)
```

- 내려도 파일 수정 내용은 그대로 남아 있다. staging area에서만 빠진다.

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
