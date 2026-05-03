# 1일차 실습 2: SDD Greenfield 워크숍 안내

## 1일차 파일 순서

### 1교시: 환경 구성과 저장소 시작

- `02_environment-setup.md`
- `10_speckit-folder-structure.md`

### 2교시: SDD 철학과 단계 구분

- `04_sdd-philosophy.md`

### 3교시: Constitution 작성

- `05_constitution-workshop.md`

### 4교시: Specify 작성

- `06_specify-workshop.md`

### 5교시: Clarify

- `07_clarify-workshop.md`

### 6교시: Plan / Tasks / Analyze

- `08_plan-tasks-workshop.md`

### 7교시: Implement / 기준선 생성

- `09_implement-baseline-workshop.md`

### 참고 솔루션

- `11_solution-guide.md`

## 먼저 기억할 구분

- `/speckit.constitution`: 팀이 지킬 원칙과 품질 기준
- `/speckit.specify`: 사용자가 원하는 결과와 수용 기준
- `/speckit.plan`: 기술 스택, 구조, 데이터, 인터페이스
- `/speckit.tasks`: 구현 순서와 작업 단위
- `/speckit.implement`: tasks를 따라 실제 구현 진행

초심자가 가장 자주 헷갈리는 지점은 아래 두 가지입니다.

### `constitution`과 `specify`의 차이

- constitution은 `이 프로젝트에서 항상 지켜야 하는 규칙`
- specify는 `이번에 만들 기능이 만족해야 하는 요구사항`

### `specify`와 `plan`의 차이

- specify는 `무엇을 왜 만드는가`
- plan은 `어떻게 만들 것인가`

## 권장 읽기 순서

1. `04_sdd-philosophy.md`에서 경계를 먼저 이해합니다.
2. `05_constitution-workshop.md`와 `06_specify-workshop.md`를 연속으로 읽으며 입력 예시 차이를 봅니다.
3. `07_clarify-workshop.md`에서 모호성 제거를 익힙니다.
4. `08_plan-tasks-workshop.md`에서 설계, 작업 분해, 산출물 일관성 검증을 합니다.
5. `09_implement-baseline-workshop.md`에서 구현과 기준선 태그까지 마무리합니다.

Spec Kit 내부 구조까지 이해하고 싶다면 `10_speckit-folder-structure.md`를 추가로 읽으면 좋습니다. 특히 `.github`와 `.specify`가 어떤 역할을 나누는지 자세히 설명해 둔 참고 문서입니다.

실습 결과를 비교해 볼 참고 답안이 필요하면 `11_solution-guide.md`를 함께 읽으면 좋습니다. 입력 예시와 기대 산출물 방향을 교시별로 정리해 두었습니다.

## 다음 단계

7교시까지 끝나면 2일차에서는 이 기준선을 보호하면서 Brownfield 변경 흐름을 다룹니다. `d02/README.md`부터 이어서 진행합니다.