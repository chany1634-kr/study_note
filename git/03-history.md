# 커밋 히스토리 다루기

## 커밋 히스토리 확인

```bash
git log                      # 커밋 히스토리 전체 보기
git log --pretty=oneline     # 한 줄씩 보기
git log --pretty=oneline --all   # 모든 브랜치의 커밋 보기
git log --pretty=oneline --all --graph   # 브랜치 흐름을 그림으로 보기
```

- `--all`은 대시 **2개**. 여러 브랜치 커밋을 한 번에 볼 수 있지만, 섞여 나와서 읽기 어렵다.
- `--graph`를 붙이면 브랜치가 갈라지고 합쳐지는 모양을 선으로 그려 준다.

```
*   c3d4e5f Merge branch 'premium'     ← 머지 커밋 (두 선이 다시 만나는 곳)
|\
| * b2c3d4e Add premium feature        ← premium 브랜치 커밋
* | a1b2c3d Fix price                  ← master 브랜치 커밋
|/
* 9f8e7d6 Initial commit               ← 갈라지기 전 공통 조상 (base)
```

- `*` = 커밋 하나
- 선이 **갈라지는 곳** = 브랜치가 나뉜 지점
- 선이 **다시 합쳐지는 곳** = merge한 지점 (머지 커밋)
- alias로 쓰면 `git hist --all --graph`

## 커밋 변경 사항 확인

```bash
git show [커밋 ID]
```

- 커밋 ID는 앞부분만 적어도 된다.
- 최소 4글자부터 가능하지만, 다른 커밋과 겹칠 수 있으니 **보통 앞 7글자**를 쓴다.

## 두 커밋 간의 차이 비교

```bash
git diff [커밋 A ID] [커밋 B ID]
```

## 최근 커밋 수정하기

```bash
git commit --amend
```

- 방금 한 커밋을 수정해서 **새 커밋으로 교체**한다. (커밋 ID가 바뀜)
- 커밋 메시지를 고치거나, 빠뜨린 파일을 추가할 때 사용한다.
- ⚠️ 기존 커밋을 바꾸는 명령어이므로 **push 전에만** 사용한다.

## alias: 명령어에 별명 붙이기

`git log --pretty=oneline`처럼 긴 명령어를 짧은 별명으로 쓸 수 있다.

```bash
git config --global alias.[별명] "[명령어]"
```

예시:

```bash
git config --global alias.hist "log --pretty=oneline"
git hist          # = git log --pretty=oneline
git hist --all    # 뒤에 옵션을 이어 붙일 수도 있다
```

- 명령어에 띄어쓰기가 있으면 따옴표로 감싼다.
- `--global`을 붙이면 내 컴퓨터의 모든 저장소에서 사용할 수 있다.
- ⚠️ 별명은 Git에 원래 있는 명령어 이름을 덮어쓸 수 없다. Git 2.54부터 `git history`라는 명령어가 새로 생겨서, `history`라는 별명은 무시된다. → `hist` 같은 다른 이름을 쓰자.
