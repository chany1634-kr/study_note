# 리모트 레포지토리와 origin

## 로컬 레포지토리를 GitHub에 처음 올리기

GitHub에서 빈 저장소(예: Math_Box)를 만든 뒤, 내 컴퓨터의 로컬 레포지토리를 연결해서 올린다.

```bash
git remote add origin https://github.com/kyuri-dev/Math_Box.git
git push -u origin master
```

## 1. git remote add origin [주소]

- `https://github.com/kyuri-dev/Math_Box.git`라는 리모트 레포지토리를 **origin이라는 이름으로 등록**한다.
- 이후로는 긴 주소 대신 `origin`이라고만 쓰면 된다.
- origin은 "근원, 기원"이라는 뜻. 처음 추가하는 리모트를 origin이라고 부르는 게 관례다.

```bash
git remote -v      # 등록된 리모트 이름과 주소 확인
```

## 2. git push -u origin master

- 로컬의 master 브랜치(와 관련된 모든 커밋)를 origin으로 보낸다.
- `-u`는 `--set-upstream`의 약자.
- 로컬 master가 origin의 master를 **tracking(추적)**하도록 연결한다.

### tracking이란?

- 로컬 브랜치 하나가 리모트 브랜치 하나와 짝지어져서 계속 바라보는 상태.
- 이 연결을 **tracking connection**이라고 한다.
- 한 번 연결해 두면 다음부터는 이렇게만 써도 된다.

```bash
git push
git pull
```

### -u를 안 하면?

매번 어디로 보낼지 직접 적어야 한다.

```bash
git push origin master:master
```

- `origin` : 리모트 레포지토리
- `master:master` : `[로컬 브랜치]:[리모트 브랜치]`
  - **앞의 master = 내 로컬 master 브랜치** (보내는 쪽)
  - **뒤의 master = 리모트의 master 브랜치** (받는 쪽)
- 두 이름이 같으면 줄여서 `git push origin master`라고 써도 된다.

## clone으로 시작하면?

- `git clone`으로 받은 저장소는 origin 등록과 tracking 연결이 **자동으로** 되어 있다.
- 그래서 `git remote add`나 `-u` 없이 바로 `git push`, `git pull`을 쓸 수 있다.
- `git status`에서 `Your branch is up to date with 'origin/main'`이 보이면 연결된 상태다.

| 시작 방법 | origin 등록 | tracking 연결 |
|---|---|---|
| `git init` 후 직접 연결 | `git remote add origin [주소]` | `git push -u origin main` |
| `git clone` | 자동 | 자동 |

## origin/main 이름표

`git log`에서 보이는 이름표의 의미:

| 이름표 | 의미 |
|---|---|
| `main` | 내 로컬 브랜치 |
| `origin/main` | 마지막으로 push/fetch했을 때 GitHub의 main 상태를 기억한 사본 |
| `origin/HEAD` | GitHub 저장소의 기본 브랜치 표시. clone했을 때만 생긴다 |

- `git push origin main`처럼 **띄어쓰기**는 "origin 서버로 main 브랜치를"이라는 뜻
- `origin/main`처럼 **슬래시**는 그 자체가 하나의 이름
