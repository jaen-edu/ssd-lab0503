# 1일차 6교시: Plan / Tasks / Analyze 워크숍

이 교시는 `무엇을 만들지`가 정해진 뒤, `어떻게 만들지`와 `어떤 순서로 만들지`를 정리하는 시간입니다.

## 교시 목표

- `/speckit.plan`에 넣어야 하는 내용을 설명할 수 있다.
- `/speckit.specify`와 `/speckit.plan`의 차이를 명확히 구분할 수 있다.
- `plan.md`, `data-model.md`, `research.md`, `contracts/`의 역할을 이해한다.
- `/speckit.tasks` 결과를 읽고 구현 순서의 적절성을 검토할 수 있다.
- `/speckit.analyze`를 언제 실행해야 하는지 설명할 수 있다.

## `/speckit.plan`의 역할

plan은 `구현 설계 문서`입니다. 여기에 들어가는 것은 주로 다음과 같습니다.

- 기술 스택 선택
- 아키텍처 방향
- 데이터 모델
- 인터페이스 또는 API 계약
- 테스트 전략
- 성능, 보안, 배포 제약

## `/speckit.specify`와 다시 비교

주제: 교육용 과제 제출 기능

### specify에 맞는 문장

- 학생은 마감 전까지 과제를 제출할 수 있어야 한다.
- 강사는 제출 시간과 제출 버전을 볼 수 있어야 한다.
- 학생은 자신의 제출만 볼 수 있어야 한다.

### plan에 맞는 문장

- 백엔드는 FastAPI, 프론트엔드는 Vite를 사용한다.
- 제출물 버전을 `submission_versions` 테이블로 관리한다.
- 파일 업로드는 로컬 저장소 대신 S3 호환 스토리지를 사용한다.
- pytest와 Playwright를 검증 전략에 포함한다.

## `/speckit.plan` 입력 예시

### 예시 1: Todo 태그 기능

```text
기존 Todo 앱에 태그 기능을 추가하기 위한 구현 계획을 작성해줘.

- 프론트엔드는 기존 Vite + Vanilla JavaScript 구조를 유지한다.
- 백엔드는 FastAPI를 사용한다.
- 데이터 저장은 SQLite를 사용한다.
- Todo와 Tag는 다대다 관계로 설계한다.
- 태그 생성, 삭제, 조회, 필터 API를 정의한다.
- pytest 기반 단위 테스트와 API 테스트 전략을 포함한다.
- 입력 검증과 중복 태그 방지 방식을 설명한다.
```

### 예시 2: 사진 앨범 앱

```text
사진 앨범 앱의 구현 계획을 작성해줘.

- 프론트엔드는 React를 사용한다.
- 사진 메타데이터는 SQLite에 저장한다.
- 앨범 내부에 하위 앨범은 허용하지 않는다.
- 드래그 앤 드롭 정렬 구조를 고려한 상태 관리 방식을 제안한다.
- 이미지 파일은 로컬 폴더에 보관한다.
- 자동 테스트 전략과 주요 컴포넌트 구조를 포함한다.
```

### 예시 3: 회의실 예약 도구

```text
회의실 예약 도구의 구현 계획을 작성해줘.

- 백엔드는 Django, 데이터베이스는 PostgreSQL을 사용한다.
- 중복 예약 방지를 위한 트랜잭션 전략을 포함한다.
- 관리자 승인 플로우와 일반 사용자 예약 플로우를 분리한다.
- 예약 생성, 승인, 취소 API 계약을 정의한다.
- 감사 로그 저장 구조와 테스트 전략을 포함한다.
```

## plan에 넣으면 안 되는 것

- `사용자는 태그로 Todo를 찾을 수 있어야 한다`
- `강사는 제출 이력을 볼 수 있어야 한다`

이 문장은 구현 방법이 아니라 요구사항이므로 spec에 있어야 합니다.

## `/speckit.tasks`의 역할

tasks는 `구현 순서가 보이는 작업 목록`입니다.

좋은 tasks는 다음 특징을 가집니다.

- 선행 관계가 자연스럽습니다.
- 테스트 또는 검증 작업이 포함됩니다.
- 작업 단위가 지나치게 크지 않습니다.
- implement가 그대로 따라갈 수 있을 만큼 구체적입니다.
- phase1~phaseN 
- 하나의 phase는 일반적으로 2~3시간 분량

## `/speckit.analyze`는 왜 여기서 실행하는가

analyze는 여러 산출물 사이의 충돌과 누락을 찾는 명령입니다. 이 명령이 제대로 동작하려면 적어도 `spec.md`, `plan.md`, `tasks.md`가 모두 준비되어 있어야 합니다.

따라서 plan과 tasks가 생성된 다음에 실행합니다.

이 단계에서 analyze가 주로 보는 것은 다음과 같습니다.

- constitution의 원칙과 spec/plan/tasks가 충돌하는가
- plan의 방향이 spec 요구사항을 충분히 만족시키는가
- tasks가 plan과 spec을 빠짐없이 반영하는가
- 테스트와 검증 작업이 상위 문서와 일치하는가

즉, clarify가 `질문에 답해 spec을 선명하게 만드는 단계`라면, analyze는 `여러 산출물을 나란히 놓고 서로 맞는지 검증하는 단계`입니다.

## `/speckit.tasks` 실행 시 주의

많은 경우 `/speckit.tasks`는 plan이 충분하면 추가 설명 없이도 실행할 수 있습니다. 다만 아래처럼 우선순위를 보강할 수는 있습니다.

```text
테스트와 데이터 모델 작업을 먼저 두고, UI 작업은 그 다음에 오도록 tasks를 작성해줘.
```

또는

```text
API, 데이터 모델, 프론트엔드 순서가 드러나게 작업 단위를 나눠줘.
```

## tasks 검토 질문

1. 데이터 모델 작업이 구현보다 먼저 오는가?
2. 테스트 작업이 빠지지 않았는가?
3. 너무 큰 작업이 하나로 뭉쳐 있지 않은가?
4. 수동 검증만 있고 자동 검증이 빠져 있지 않은가?

## Workflow Engine 메모

설계서 기준 v0.8.3에서는 Workflow Engine으로 SDD 흐름을 자동화할 수 있습니다. 다만 자동화가 있더라도 사람의 승인 지점은 그대로 중요합니다.

## 실습 단계

1. `/speckit.plan`을 실행합니다.
2. `plan.md`, `data-model.md`, `research.md`, `contracts/`를 읽습니다.
3. `/speckit.tasks`를 실행합니다.
4. `tasks.md`를 검토합니다.
5. `/speckit.analyze`를 실행합니다.
6. analyze 결과를 보고 `spec`, `plan`, `tasks` 중 무엇을 고칠지 결정합니다.
7. 변경이 확정되면 현재 feature 브랜치에서 commit한 뒤 main에 merge합니다.

예시 명령:

```powershell
git checkout 001-todo-tagging
git status
git add specs/001-todo-tagging .github
git commit -m "docs: add plan tasks and analysis"
git checkout main
git merge --no-ff 001-todo-tagging -m "merge: implementation plan"
git push origin main
```

여기서도 `git checkout 001-todo-tagging`를 먼저 넣은 이유는, plan, tasks, analyze까지가 같은 feature 브랜치 흐름 안에서 이어지는 작업이기 때문입니다. `/speckit.specify`가 만든 feature 디렉터리는 `.specify/feature.json`으로 추적되지만, 현재 Git 브랜치가 `main`에 남아 있을 수도 있으므로 먼저 기존 feature 브랜치로 돌아가는 편이 안전합니다.

### analyze 결과에서 무엇을 고쳐야 하는가

- spec 문장이 부족하거나 모호하면 `spec.md`를 고칩니다.
- 기술 방향이나 데이터 모델 설명이 어긋나면 `plan.md`를 고칩니다.
- 구현 순서나 검증 작업이 빠졌으면 `tasks.md`를 고칩니다.

analyze의 목적은 새 문서를 만드는 것이 아니라, 이미 만들어진 산출물 사이의 불일치를 찾아 적절한 문서로 다시 되돌려 보내는 것입니다.

## 스스로 점검

1. spec과 plan 문장을 서로 바꿔 놓았을 때 어색함을 느낄 수 있는가?
2. tasks를 보고 바로 구현 순서를 상상할 수 있는가?
3. 검증 작업이 tasks에 포함되어 있는가?