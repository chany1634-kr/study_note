# Git 작동 흐름

## 전체 흐름

```
Working tree ──add──▶ Staging area ──commit──▶ Local repository ──push──▶ Remote repository
```

| 영역 | 설명 |
|---|---|
| **Working tree** (Working directory) | 내가 실제로 파일을 수정하는 작업 폴더 |
| **Staging area** | 다음 커밋에 넣을 변경 사항을 올려두는 곳 (`git add`) |
| **Local repository** | 내 컴퓨터의 `.git` 폴더. 커밋 기록이 저장됨 (`git commit`) |
| **Remote repository** | GitHub 같은 서버 저장소. 팀원과 공유됨 (`git push`) |

- `commit`까지는 **내 컴퓨터에만** 저장된다.
- `push`를 해야 GitHub(리모트)에 올라간다.

## Staging area의 특징

- 커밋을 해도 staging area가 비워지지 않는다.
- 커밋 직후 staging area는 **방금 커밋한 내용과 같은 상태**로 남아 있다.
- 이후 파일을 수정하고 `git add`하면 그 파일이 새 내용으로 **추가되거나 교체**된다.
