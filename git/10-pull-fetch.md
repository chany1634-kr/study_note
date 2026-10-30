# pull과 fetch (협업할 때)

## 상황: push가 거절될 때

개발자 A와 B가 같은 리모트 레포지토리에서 작업한다.

1. B가 먼저 자기 커밋을 push했다.
2. A가 push하려고 하면 **거절(rejected)된다.**
   - 리모트에 A가 아직 받지 않은 B의 커밋이 있기 때문이다.
   - 메시지 예: `! [rejected] main -> main (fetch first)`
3. A는 먼저 B의 커밋을 받아서 합친 뒤에 push해야 한다.

```bash
git pull        # B의 커밋을 받아서 내 브랜치에 합친다
# (conflict가 나면 해결 → git add → git commit)
git push        # 이제 push 가능
```

- conflict는 **둘이 같은 곳을 다르게 고쳤을 때만** 난다. 다른 곳을 고쳤으면 Git이 자동으로 합쳐 준다.
- 합치면 머지 커밋이 생겨서, A의 커밋과 B의 커밋이 갈라졌다가 다시 만나는 모양이 된다.

## pull = fetch + merge

| 명령어 | 하는 일 |
|---|---|
| `git fetch` | 리모트의 최신 커밋을 **가져오기만** 한다. 내 브랜치는 그대로 |
| `git merge` | 가져온 내용을 내 브랜치에 합친다 |
| `git pull` | 위 두 개를 **한 번에** 한다 (자동으로 합침) |

## fetch는 언제 쓰나?

pull은 가져오자마자 자동으로 합친다. **합치기 전에 먼저 확인하고 싶으면** fetch를 쓴다.

- 리모트의 내용을 merge하기 전에 점검해야 할 때
- 리모트 내용과 내 코드를 비교해서 문제가 없는지 검토해야 할 때

## fetch 후 확인하고 합치기

```bash
git fetch
# 출력 예: premium -> origin/premium

git diff premium origin/premium   # 내 로컬 premium vs 리모트 premium 비교
git merge origin/premium          # 확인했으면 합치기
```

- `origin/premium` = fetch로 가져온 **리모트 premium 브랜치의 사본**
  - 내 로컬 브랜치: `premium`
  - 리모트 브랜치의 사본: `origin/premium`
- ⚠️ `origin` 자체는 사본이 아니라 **리모트 레포지토리의 이름(별명)**이다. 사본은 `origin/premium`처럼 `origin/브랜치이름` 형태다.

## git diff 정리

| 명령어 | 비교 대상 |
|---|---|
| `git diff` | working tree ↔ staging area (add 안 한 변경) |
| `git diff --staged` | staging area ↔ 마지막 커밋 (add 한 변경) |
| `git diff [커밋 A] [커밋 B]` | 두 커밋 간의 차이 |
| `git diff [브랜치 A] [브랜치 B]` | 두 브랜치 간의 차이 |

- `git diff A B`는 **A에서 B로 가면 뭐가 바뀌는지**를 보여준다.
- `git diff premium origin/premium`에서 `+` 줄 = 리모트에만 있는 내용, `-` 줄 = 내 로컬에만 있는 내용.

## clone vs pull

| 명령어 | 언제 |
|---|---|
| `git clone [주소]` | 처음 한 번. 저장소 전체를 내 컴퓨터로 복사 |
| `git pull` | 그 이후. 새로 생긴 커밋만 받아옴 |
