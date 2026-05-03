# 1일차 7교시: Implement와 기준선 생성

이 교시는 plan과 tasks를 바탕으로 실제 구현을 진행하고, 2일차 Brownfield 실습의 기준선인 `baseline-v1.0`을 만드는 시간입니다.

## 교시 목표

- `/speckit.implement`를 한 번에 전부 맡기지 않고 단계적으로 사용할 수 있다.
- 구현 중간에 spec, plan, tasks와 코드의 정합성을 확인할 수 있다.
- 테스트를 통과한 상태를 기준선으로 남길 수 있다.
- `baseline-v1.0` 태그를 생성할 수 있다.

## `/speckit.implement`는 어떻게 써야 하는가

implement는 `tasks를 따라 실제 코드를 만드는 단계`입니다. 이 단계에서 가장 중요한 원칙은 `한 번에 끝내려고 하지 않는 것`입니다.

좋은 사용 방식:

- 범위를 제한해서 실행한다.
- 중간 결과를 읽는다.
- 테스트를 돌린다.
- 다음 단계로 넘어갈지 사람이 결정한다.

## 다양한 `/speckit.implement` 입력 예시

### 예시 1: 첫 2개 작업만 구현

```text
tasks.md의 앞에서부터 2개 작업만 구현해줘.
데이터 모델과 관련 테스트를 먼저 작성하고, 끝나면 멈춰서 변경 내용을 요약해줘.
```

### 예시 2: API 계층만 먼저 구현

```text
이번 단계에서는 태그 생성, 삭제, 조회 API와 관련 단위 테스트까지만 구현해줘.
프론트엔드 UI는 아직 건드리지 마.
```

### 예시 3: 테스트 우선 구현

```text
tasks.md를 기준으로 이번 단계의 수용 기준을 만족하는 테스트를 먼저 만들고,
그 다음 최소한의 코드 변경으로 통과시켜줘.
```

### 예시 4: 중간 점검 포함

```text
3개 작업 단위로 진행해줘.
각 작업이 끝날 때마다 어떤 acceptance criteria를 만족했는지 요약하고,
다음 작업으로 넘어가기 전에 검토 포인트를 제시해줘.
```

## 이런 입력은 피한다

```text
전체 다 구현해줘.
```

문제점:

- 범위가 너무 큽니다.
- 중간 검토 지점이 없습니다.
- drift가 생겨도 늦게 발견됩니다.

## 구현 중 확인해야 할 것

1. 생성된 코드가 spec의 수용 기준을 만족하는가
2. plan의 구조와 맞는가
3. tasks 순서가 실제로 지켜졌는가
4. 테스트가 함께 만들어졌는가
5. 불필요한 파일이 추가되지 않았는가

## 구현 중 습관

각 의미 있는 단계마다 아래 명령으로 상태를 확인합니다.

```powershell
git status
git diff
```

## 테스트 확인

프로젝트에서 사용하는 테스트 명령을 실행합니다.

예시:

```powershell
uv run pytest
```

테스트가 모두 통과해야 기준선으로 삼을 수 있습니다.

## 기준선 커밋과 merge

이 단계는 구현과 테스트를 마친 뒤 프로젝트 전체 변경을 남기는 단계입니다. 여기서는 `git add .`가 상대적으로 자연스럽지만, 그래도 먼저 `git status`로 `.venv`, 비밀 파일, 캐시 파일이 섞이지 않았는지 확인해야 합니다.

```powershell
git checkout -b feat/greenfield-implementation
git status
git add .
git commit -m "feat: complete greenfield baseline"
git checkout main
git merge --no-ff feat/greenfield-implementation -m "merge: greenfield baseline"
git push origin main
```

## 태그 생성

```powershell
git tag baseline-v1.0
git push origin baseline-v1.0
```

## 1일차 종료 점검

아래 질문에 스스로 답할 수 있어야 합니다.

1. Constitution과 Spec의 차이는 무엇인가?
2. Specify와 Plan의 차이는 무엇인가?
3. Clarify는 왜 필요한가?
4. Tasks 없이 바로 implement하면 어떤 문제가 생기는가?
5. baseline-v1.0 태그를 왜 남기는가?

## 다음 단계

1일차가 끝나면 2일차에서는 이 baseline을 보호하면서 변경 요구를 다루게 됩니다. `d02/README.md`부터 시작합니다.