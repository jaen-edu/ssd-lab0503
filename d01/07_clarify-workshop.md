# 1일차 5교시: Clarify 워크숍

이 교시는 spec에 남아 있는 모호함을 줄이고, 다음 plan 단계로 내려가기 전에 요구사항을 더 선명하게 만드는 시간입니다.

## 교시 목표

- `/speckit.clarify`의 목적을 설명할 수 있다.
- 좋은 clarify 답변과 나쁜 답변을 구분할 수 있다.
- spec을 더 테스트 가능하게 다듬을 수 있다.
- 왜 이 단계에서는 기능 규칙만 확정해야 하는지 설명할 수 있다.

## `/speckit.clarify`는 왜 필요한가

specify는 요구사항 문서를 만들지만, 모든 규칙이 한 번에 완벽하게 정해지지는 않습니다. 예를 들어 아래는 모두 모호합니다.

- 태그를 몇 개까지 붙일 수 있는가
- 삭제는 복구 가능한가
- 정렬 기준은 최신순인가 이름순인가
- 관리자와 일반 사용자의 권한 차이는 무엇인가

clarify는 이런 모호한 항목을 질문으로 꺼내고, 팀이 답하면 spec을 더 선명하게 만듭니다.

## 좋은 clarify 답변의 특징

- 선택지가 분명합니다.
- 테스트 가능한 규칙이 됩니다.
- 기술 구현 방식이 아니라 기능 규칙에 답합니다.

### 예시 1: 태그 개수 제한

질문:

```text
한 Todo 항목에 붙일 수 있는 태그 개수 제한이 필요한가?
```

좋은 답:

```text
한 Todo 항목에는 최대 5개의 태그만 허용한다.
```

나쁜 답:

```text
적당히 많지 않게 한다.
```

### 예시 2: 삭제 방식

질문:

```text
태그 삭제는 영구 삭제인가, 숨김 처리인가?
```

좋은 답:

```text
태그 삭제는 영구 삭제로 처리하되, 이미 연결된 Todo에서는 삭제 전 경고를 표시한다.
```

### 예시 3: 정렬 기준

질문:

```text
태그 목록은 어떤 기준으로 정렬해야 하는가?
```

좋은 답:

```text
태그 목록은 이름의 오름차순으로 정렬한다.
```

## clarify에서 넣지 말아야 하는 답

- `SQLite에서 UNIQUE 인덱스를 건다`
- `React state는 zustand로 관리한다`

이런 문장은 plan 쪽으로 가야 합니다.

## 실습 단계

1. `/speckit.clarify`를 실행합니다.
2. 질문을 읽고 기능 규칙 수준에서 답합니다.
3. 반영된 `spec.md`를 다시 읽습니다.
4. spec 문장에서 테스트하기 어려운 표현, 빠진 수치, 모호한 권한 범위를 다시 정리합니다.
5. 변경이 확정되면 현재 feature 브랜치에서 commit한 뒤 main에 merge합니다.

이 저장소 흐름에서는 `/speckit.specify`를 실행할 때 이미 `001-todo-tagging` 같은 feature 브랜치가 자동으로 만들어진 상태라고 보면 됩니다. 따라서 clarify는 보통 그 브랜치 위에서 이어서 수행하고, 여기서 다시 새 브랜치를 만들 필요는 없습니다.

예시 명령:

```powershell
git checkout 001-todo-tagging
git status
git add specs/001-todo-tagging
git commit -m "docs: clarify spec"
git checkout main
git merge --no-ff 001-todo-tagging -m "merge: clarified spec"
git push origin main
```

여기서 `git checkout 001-todo-tagging`를 먼저 넣은 이유는, clarify 작업도 기존 feature 브랜치 위에서 이어지는 것이 자연스럽기 때문입니다. `/speckit.specify`가 만든 feature 디렉터리는 `.specify/feature.json`으로 추적되지만, 현재 Git 브랜치가 `main`에 남아 있을 수도 있으므로 먼저 기존 feature 브랜치로 돌아가는 편이 안전합니다.

### 왜 새 브랜치를 다시 만들지 않는가

clarify는 새로운 기능을 시작하는 단계가 아니라, 방금 만든 feature spec을 더 선명하게 다듬는 단계입니다. 그래서 이 저장소에서는 `specify -> clarify`를 하나의 feature 브랜치 흐름으로 이어서 보는 편이 자연스럽습니다.

즉, 여기서의 기준은 다음과 같습니다.

- `001-todo-tagging` 같은 feature 브랜치: 이번 기능 spec의 초안부터 clarify 반영까지 이어지는 작업 공간
- `specs/001-todo-tagging/spec.md`: clarify 결과가 실제로 반영되는 핵심 문서
- `.specify/feature.json`: 지금 어떤 feature 디렉터리를 기준으로 다음 단계가 이어질지 가리키는 포인터

만약 clarify 결과를 별도 실험 브랜치로 완전히 분리해야 하는 특별한 상황이라면 새 브랜치를 써도 되지만, 이 교육 자료의 기본 흐름에서는 기존 feature 브랜치를 그대로 이어 쓰는 편이 덜 혼란스럽습니다.

## 실습용 질문 세트

아래 질문에 답해 보고, 답이 clarify인지 plan인지 구분합니다.

1. 태그는 최대 몇 개까지 허용할 것인가?
2. 태그 저장은 별도 테이블로 분리할 것인가?
3. 삭제된 태그는 기존 Todo에서 어떻게 보여야 하는가?
4. 검색 API는 REST로 만들 것인가?

정답 방향:

- 1, 3은 clarify
- 2, 4는 plan

## 스스로 점검

1. clarify 이후 spec 문장이 더 테스트 가능해졌는가?
2. 어떤 질문이 plan이 아니라 clarify에 속하는지 설명할 수 있는가?
3. 기능 규칙과 구현 결정을 여전히 구분하고 있는가?