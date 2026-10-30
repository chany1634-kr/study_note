# git tag

## 태그란?

- 커밋 메시지 외에 **중요한 커밋에 붙이는 이름표**.
- 주로 프로젝트의 주요 버전이 시작되는 커밋에 단다.

## 태그 달기

```bash
git tag [태그 이름] [커밋 ID]
```

예시: 첫 번째 커밋에 v1.0, 여섯 번째 커밋에 v2.0 태그 달기

```bash
git tag v1.0 [1번 커밋 ID]
git tag v2.0 [6번 커밋 ID]
```

- 커밋 ID를 생략하면 현재 HEAD가 가리키는 커밋에 태그가 달린다.
- ⚠️ 태그 이름에는 **띄어쓰기를 쓸 수 없다.** `Version 1` 대신 `v1.0`, `Version1`처럼 쓴다.

## 태그 확인

```bash
git tag              # 태그 목록 보기
git show [태그 이름]  # 태그가 연결된 커밋 정보 보기
```

## 태그를 GitHub에 올리기

`git push`만으로는 태그가 올라가지 않는다. 따로 push해야 한다.

```bash
git push origin v1.0     # 태그 하나만 올리기
git push origin --tags   # 모든 태그 올리기
```
