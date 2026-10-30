# git rebase

## rebase란?

- 커밋을 **재배치**한다는 뜻. (re + base = 기준점을 다시 정한다)
- 내 브랜치의 커밋들을 떼어서 다른 브랜치의 최신 커밋 **뒤에 다시 붙인다.**

```bash
git switch premium
git rebase master      # premium의 커밋들을 master 최신 커밋 뒤로 옮긴다
```

## merge vs rebase

처음 상태: master와 premium이 B에서 갈라졌다.

```
        C          ← master
       /
A - B
       \
        D          ← premium
```

**merge** (master에서 `git merge premium`)

```
A - B - C - M      ← master   (M = 머지 커밋)
     \     /
      D ---
```

**rebase** (premium에서 `git rebase master`)

```
A - B - C - D'     ← premium
```

- D가 C 뒤로 옮겨지면서 **D'라는 새 커밋**이 된다. 내용은 같지만 커밋 ID가 바뀐다.
- 기록이 한 줄로 깔끔해진다.

| | merge | rebase |
|---|---|---|
| 파일 결과 | 같음 | 같음 |
| 머지 커밋 | 생김 | **안 생김** |
| 기존 커밋 | 그대로 | **새 커밋으로 바뀜** (ID 변경) |
| 기록 모양 | 갈라졌다 합쳐짐 | 한 줄 |
| 언제 | 합쳤다는 정보가 필요할 때 | 히스토리를 깔끔하게 유지할 때 |

## ⚠️ rebase 사용 규칙

- merge는 언제든 쓸 수 있다.
- rebase는 **push 전, 나만 가진 커밋에만** 쓴다.
- 이미 push한 커밋을 rebase하면 커밋 ID가 바뀌어서 팀원 기록과 꼬인다. → push 후에는 merge
- reset, commit --amend와 같은 "기록을 바꾸는 명령어" 그룹이다.

## rebase 중 conflict가 나면

rebase도 같은 줄을 다르게 고쳤으면 충돌이 난다. 해결 순서는

1. 충돌난 파일을 열어서 고친다. (표시 `<<<<<<<` `=======` `>>>>>>>` 지우기)
2. `git add [파일 이름]`
3. `git rebase --continue` ← commit이 아니라 이걸 친다

```bash
git rebase --continue   # 고쳤으니 rebase 계속 진행
git rebase --abort      # rebase 전 상태로 완전히 취소
```

- merge 충돌은 고친 뒤 `git commit`, rebase 충돌은 고친 뒤 `git rebase --continue`
- 하던 작업에 맞는 명령어로 마무리해야 한다. merge 중에 rebase --continue를 치거나 그 반대로 할 수는 없다.

## 실무에서 자주 쓰는 패턴

```bash
git pull --rebase    # 팀원 커밋을 받아오고, 내 커밋을 그 뒤로 재배치
git push
```

- 그냥 `git pull`은 머지 커밋이 생기는데, `--rebase`를 붙이면 기록이 한 줄로 유지된다.
- 아직 push 안 한 내 커밋만 재배치되니까 규칙에도 맞다.
