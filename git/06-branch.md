# 브랜치 (branch)

## 브랜치란?

- 나뭇가지를 하나 추가하듯 작업 흐름을 **나눠서**, 서로의 작업에 영향을 주지 않게 해 주는 기능.
- 여러 버전을 나눠서 관리할 수 있다.
  - 예: 무료 버전 / 유료 버전, 배포용 / 개발용 / 테스트용
- 레포지토리를 만들고 첫 커밋을 하면 기본 브랜치가 자동으로 생긴다.
  - 요즘은 `main`, 예전에는 `master`라는 이름을 주로 썼다.

## 브랜치 명령어

```bash
git branch                  # 브랜치 목록 보기 (* 표시가 현재 브랜치)
git branch premium          # premium 브랜치 만들기
git branch -d premium       # premium 브랜치 삭제
```

- `-d`는 이미 합쳐진(merge된) 브랜치만 삭제한다. 합치지 않은 작업이 있으면 삭제를 막아 준다.
- 합치지 않은 브랜치를 강제로 지우려면 `-D`를 쓴다. (작업이 사라지니 주의)
- 지금 내가 있는 브랜치는 삭제할 수 없다. 다른 브랜치로 이동한 뒤 삭제한다.

## 브랜치 이동

```bash
git switch premium          # premium 브랜치로 이동
git switch -c premium       # premium 브랜치를 만들면서 바로 이동
```

예전 방식(같은 기능):

```bash
git checkout premium
git checkout -b premium
```

- `checkout`은 브랜치 이동과 파일 되돌리기 기능을 둘 다 가지고 있어서 헷갈리기 쉽다.
- 그래서 Git 2.23부터 역할을 나눴다.
  - 브랜치 이동 → `git switch`
  - 파일 되돌리기 → `git restore`
- 즉 `checkout = switch + restore`

## switch vs reset

| | 움직이는 것 | 용도 |
|---|---|---|
| `switch` / `checkout` | HEAD만 | 브랜치 이동, 과거 커밋 구경 |
| `reset` | HEAD + 브랜치 | 커밋 취소 |

## 참고: cat

```bash
cat [파일 이름]
```

- Git 명령어가 아니라 터미널 명령어. 파일 내용을 터미널에 출력한다.
- 브랜치를 이동한 뒤 파일 내용이 어떻게 바뀌었는지 확인할 때 쓰기 좋다.
- `git show`는 **커밋 정보**를 보여주고, `cat`은 **지금 파일 내용**을 보여준다.
