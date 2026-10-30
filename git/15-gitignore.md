# .gitignore

## .gitignore란?

- 버전 관리할 필요가 없는 파일 이름을 적어두는 파일.
- 여기 적힌 파일은 Git이 **못 본 척**한다. `git add .`을 해도 올라가지 않는다.
- 저장소 맨 위 폴더에 `.gitignore`라는 이름으로 만든다.

## 만들기

```bash
echo ".DS_Store" > .gitignore     # .DS_Store 한 줄이 적힌 파일 만들기
echo "*.log" >> .gitignore        # 한 줄 더 추가하기
```

- `>` → 파일을 새로 만들어서 저장 (기존 내용은 **덮어씀**)
- `>>` → 기존 내용 뒤에 **추가**
- 에디터(Sublime Text, VS Code 등)로 열어서 직접 적어도 된다.

## 자주 무시하는 파일

| 적는 법 | 의미 |
|---|---|
| `.DS_Store` | 맥이 자동으로 만드는 Finder 설정 파일 |
| `*.log` | 이름이 `.log`로 끝나는 모든 파일 |
| `node_modules/` | 그 폴더 전체 |
| `.env` | 비밀번호, API 키 같은 비밀 정보가 담긴 설정 파일 |

## .gitignore는 올려야 할까?

- **올린다.** 무시 규칙이 적힌 파일이라, 올려두면 다른 컴퓨터에서 clone해도 같은 규칙이 적용된다.
- 팀 프로젝트에서는 팀원 모두가 같은 파일을 무시하게 된다.
- `.DS_Store` = 올리면 안 되는 파일 / `.gitignore` = 그걸 막는 규칙 파일

## ⚠️ 주의: 이미 올라간 파일은 무시되지 않는다

- `.gitignore`는 **아직 Git이 관리하지 않는 파일**에만 효과가 있다.
- 이미 커밋된 파일은 `.gitignore`에 적어도 계속 추적된다. 이때는 Git의 관리에서 빼 줘야 한다.

```bash
git rm --cached .DS_Store    # 파일은 내 컴퓨터에 남기고 Git 관리에서만 빼기
git commit -m "Stop tracking .DS_Store"
```

## 뭘 무시해야 할지 모르겠다면

- 버전 관리를 **시작하기 전에** `.gitignore`부터 만들어 두면 깔끔하다.
- GitHub에서 새 저장소를 만들 때 **Add .gitignore** 옵션에서 언어/플랫폼(Python, Node, Java 등)을 고르면 기본 템플릿을 만들어 준다.
- GitHub의 `github/gitignore` 저장소에 언어별 템플릿이 모여 있다.
