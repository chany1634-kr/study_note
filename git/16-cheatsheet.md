# Git 명령어 총정리

자세한 설명은 오른쪽 노트 번호를 참고.

## 1. 시작하기 · 설정

| 명령어 | 하는 일 | 노트 |
|---|---|---|
| `git init` | 현재 폴더를 Git 프로젝트로 설정 (`.git` 폴더 생성) | 01 |
| `git config --global user.name "이름"` | 커밋 작성자 이름 설정 | 01 |
| `git config --global user.email "이메일"` | 커밋 작성자 이메일 설정 | 01 |
| `git config --global alias.[별명] "[명령어]"` | 긴 명령어에 별명 붙이기 (예: `hist`) | 03 |
| `git help [명령어]` | 공식 매뉴얼 보기 (`q`로 나가기) | 01 |

## 2. staging area · 커밋

| 명령어 | 하는 일 | 노트 |
|---|---|---|
| `git add [파일]` / `git add [폴더]` / `git add .` | staging area에 올리기 (`.` = 지금 폴더 전체) | 01 |
| `git restore --staged [파일]` | staging area에서 내리기 (= `git reset [파일]`) | 01 |
| `git status` | 현재 상태 확인. 문제 생기면 제일 먼저 | 01 |
| `git diff` | add **안 한** 변경 보기 | 09 |
| `git diff --staged` | add **한** 변경 보기 (= 커밋될 내용) | 09 |
| `git commit -m "메시지"` | 커밋 남기기 | 01 |
| `git commit` | vim이 열려서 메시지 입력 | 아래 vim 참고 |
| `git commit --amend` | 최신 커밋 수정 → 새 커밋으로 교체 (push 전에만) | 03 |

## 3. 히스토리 보기

| 명령어 | 하는 일 | 노트 |
|---|---|---|
| `git log` | 커밋 히스토리 | 03 |
| `git log --pretty=oneline` (= `git hist`) | 한 줄씩 보기 | 03 |
| `git log --pretty=oneline --all --graph` | 모든 브랜치를 그래프로 보기 | 03 |
| `git show [커밋 ID]` | 커밋의 변경 내용 보기 | 03 |
| `git diff [A] [B]` | 두 커밋 / 두 브랜치 비교 | 03, 10 |
| `git blame [파일]` | 줄마다 어떤 커밋이 만들었는지 | 11 |
| `git reflog` | HEAD가 거쳐 간 기록 (사라진 커밋 찾기) | 04 |
| `git tag [태그] [커밋 ID]` | 커밋에 이름표 붙이기 (`git push origin --tags`로 올리기) | 05 |

## 4. 되돌리기

| 명령어 | 하는 일 | 언제 | 노트 |
|---|---|---|---|
| `git restore [파일]` | 커밋 안 한 수정 되돌리기 | 커밋 전 | 04 |
| `git reset --soft [ID]` | 커밋만 취소 (add 상태 유지) | push 전 | 04 |
| `git reset [ID]` (= `--mixed`) | 커밋 + add 취소 (파일은 유지) | push 전 | 04 |
| `git reset --hard [ID]` | 파일까지 되돌림 | push 전 | 04 |
| `git revert [ID]` | 커밋을 취소하는 **새 커밋** 생성 | push 후 | 11 |

- reset에는 **이동할** 커밋 ID, revert에는 **취소할** 커밋 ID를 적는다.
- 커밋 ID 대신 `HEAD^`, `HEAD~2`처럼 써도 된다.

## 5. 브랜치

| 명령어 | 예전 방식 | 하는 일 | 노트 |
|---|---|---|---|
| `git branch` | | 브랜치 목록 | 06 |
| `git branch [이름]` | | 브랜치 만들기 | 06 |
| `git switch [이름]` | `git checkout [이름]` | 브랜치 이동 | 06 |
| `git switch -c [이름]` | `git checkout -b [이름]` | 만들면서 이동 | 06 |
| `git branch -d [이름]` | | 브랜치 삭제 (합친 것만, 강제는 `-D`) | 06 |

- `checkout = switch + restore`

## 6. 합치기

| 명령어 | 하는 일 | 노트 |
|---|---|---|
| `git merge [브랜치]` | 현재 브랜치에 다른 브랜치 합치기 | 07 |
| `git merge --abort` | merge 통째로 취소 | 07 |
| `git rebase [브랜치]` | 내 커밋을 그 브랜치 최신 커밋 뒤로 옮기기 (push 전에만) | 12 |
| `git rebase --continue` / `--abort` | 충돌 해결 후 계속 / 취소 | 12 |
| `git cherry-pick [커밋 ID]` | 커밋 하나만 골라서 현재 브랜치로 복사 | 14 |

충돌 해결: 파일 열기 → `<<<<<<<` `=======` `>>>>>>>` 지우고 수정 → `git add` → `git commit` (rebase면 `git rebase --continue`)

## 7. 리모트 (GitHub)

| 명령어 | 하는 일 | 노트 |
|---|---|---|
| `git clone [주소]` | GitHub 저장소를 처음 가져오기 (origin·tracking 자동) | 08 |
| `git remote add origin [주소]` | 리모트를 origin이라는 이름으로 등록 | 08 |
| `git remote -v` | 등록된 리모트 확인 | 08 |
| `git push -u origin main` | 처음 push + tracking 연결 | 08 |
| `git push` | 로컬 커밋 올리기 | 08 |
| `git fetch` | 리모트 최신 커밋을 **가져오기만** | 10 |
| `git pull` | 가져와서 합치기 (= fetch + merge) | 10 |
| `git pull --rebase` | 가져와서 내 커밋을 그 뒤로 재배치 | 12 |
| `git push --force-with-lease` | 기록을 바꾼 뒤 강제 push (**나만 쓰는 브랜치만**) | 09 |

## 8. 임시 저장 · 무시

| 명령어 | 하는 일 | 노트 |
|---|---|---|
| `git stash` | 작업 내용 임시 저장 (새 파일까지는 `-u`) | 13 |
| `git stash list` | 목록 보기 (`stash@{0}`이 최신) | 13 |
| `git stash apply [stash@{n}]` | 꺼내기 (목록에 남음) | 13 |
| `git stash drop [stash@{n}]` | 지우기 | 13 |
| `git stash pop [stash@{n}]` | 꺼내고 지우기 (= apply + drop) | 13 |
| `.gitignore` | 적힌 파일은 Git이 무시 | 15 |

- stash에서 번호를 생략하면 가장 최근 것에 적용된다.

## 9. vim (커밋 메시지 창)

| 키 | 하는 일 |
|---|---|
| `i` | 입력 시작 |
| `Esc` | 입력 끝 |
| `:wq` | 저장하고 나가기 |
| `:q!` | 저장 안 하고 나가기 |

## 10. 알아두면 좋은 사실

- `git push`와 `git pull`은 **브랜치 단위**로 동작한다. main에서 push하면 main만 올라가고 premium은 안 올라간다. (`git push --all`은 모든 브랜치)
- 기록을 바꾸는 명령어(`reset`, `rebase`, `commit --amend`)는 **push 전에만**. push 후에는 `revert`, `merge`.
- 무언가 이상하면 일단 `git status`.

## 11. 상황별 빠른 찾기

| 상황 | 명령어 |
|---|---|
| add 잘못했다 | `git restore --staged [파일]` |
| 커밋 메시지 오타 (push 전) | `git commit --amend -m "..."` |
| 방금 커밋 취소 (push 전) | `git reset --soft HEAD^` |
| push한 커밋 취소 | `git revert [ID]` |
| reset 잘못했다 | `git reflog` → `git reset --hard [ID]` |
| push가 거절됐다 | `git pull` → (충돌 해결) → `git push` |
| 작업 중에 급히 다른 브랜치로 | `git stash` → `git switch` → 돌아와서 `git stash pop` |
| 다른 브랜치 커밋 하나만 필요 | `git cherry-pick [ID]` |
