# git cherry-pick

## 필요한 커밋만 가져오기

```bash
git cherry-pick [커밋 ID]
```

- 다른 브랜치에 있는 커밋 **하나만 골라서** 현재 브랜치에 복사해 온다.
- 체리 나무에서 원하는 체리만 따 오는 것처럼, 브랜치 전체를 merge하지 않고 필요한 커밋만 가져온다.

## 예시: test 브랜치에서 실험하고 좋은 것만 가져오기

```bash
git switch -c test        # 실험용 브랜치 만들기
# 여러 가지 시도하면서 커밋 (a1b2c3d는 성공, e4f5g6h는 실패)
git switch main
git cherry-pick a1b2c3d   # 성공한 커밋만 main으로 가져오기
git push
```

```
main:  A - B - a1b2c3d'      ← 복사된 커밋
             \
test:         a1b2c3d - e4f5g6h
```

- 가져온 커밋은 **새 커밋**이 된다. 내용은 같지만 커밋 ID가 다르다. (rebase의 D → D'와 같은 원리)
- 원래 test 브랜치의 커밋은 그대로 남아 있다.

## 참고

- 같은 곳을 다르게 고쳤으면 충돌이 날 수 있다. 고치고 `git add` → `git cherry-pick --continue`, 취소는 `git cherry-pick --abort`
- 여러 개를 가져오려면 `git cherry-pick [ID1] [ID2]`처럼 이어서 적는다.

## 비슷한 명령어 정리

| 명령어 | 하는 일 |
|---|---|
| `git merge` | 브랜치 **전체**를 합친다 |
| `git rebase` | 내 브랜치 커밋들을 다른 브랜치 뒤로 **옮긴다** |
| `git cherry-pick` | 커밋 **하나만** 골라서 복사해 온다 |
| `git revert` | 커밋 하나를 **취소하는** 새 커밋을 만든다 |
