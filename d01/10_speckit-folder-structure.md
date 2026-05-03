# Spec Kit 폴더 구조 해설: `.github`와 `.specify`

이 문서는 Spec Kit을 처음 접하는 학습자가 `.github`와 `.specify` 폴더를 `실제로 무엇을 하는 파일들인가` 관점에서 이해할 수 있도록 만든 해설 문서입니다.

초심자 입장에서는 이 두 폴더가 가장 낯섭니다.

- 파일 이름이 영어로 되어 있습니다.
- Markdown 파일이 많은데, 어떤 것은 문서처럼 보이고 어떤 것은 설정처럼 보입니다.
- `/speckit.specify` 같은 명령이 어디와 연결되는지 바로 보이지 않습니다.

이 문서의 목표는 그 연결을 풀어서 보여 주는 것입니다.

## 먼저 한 줄로 요약하면

- `.github/`는 `Copilot이 Spec Kit 명령을 이해하고 실행하는 방법`이 들어 있는 폴더입니다.
- `.specify/`는 `Spec Kit이 산출물을 만들 때 참고하는 템플릿, 설정, 메모리, 확장, 워크플로`가 들어 있는 폴더입니다.

즉, `.github`는 `AI 에이전트 쪽 연결`, `.specify`는 `Spec Kit 워크플로 본체 쪽 연결`이라고 보면 이해가 쉽습니다.

## 큰 구조 보기

현재 저장소 기준으로 핵심 구조를 단순화하면 아래와 같습니다.

```text
.github/
├─ copilot-instructions.md
├─ agents/
│  ├─ speckit.constitution.agent.md
│  ├─ speckit.specify.agent.md
│  ├─ speckit.plan.agent.md
│  └─ ...
└─ prompts/
   ├─ speckit.constitution.prompt.md
   ├─ speckit.specify.prompt.md
   ├─ speckit.plan.prompt.md
   └─ ...

.specify/
├─ extensions.yml
├─ init-options.json
├─ integration.json
├─ integrations/
│  └─ speckit.manifest.json
├─ memory/
│  └─ constitution.md
├─ templates/
│  ├─ constitution-template.md
│  ├─ spec-template.md
│  ├─ plan-template.md
│  ├─ tasks-template.md
│  └─ checklist-template.md
├─ scripts/
│  └─ powershell/
│     ├─ check-prerequisites.ps1
│     ├─ common.ps1
│     ├─ create-new-feature.ps1
│     └─ setup-plan.ps1
├─ workflows/
│  └─ speckit/
│     └─ workflow.yml
└─ extensions/
   └─ git/
      ├─ extension.yml
      ├─ git-config.yml
      ├─ config-template.yml
      ├─ README.md
      ├─ commands/
      └─ scripts/
```

## `.github` 폴더 설명

`.github`는 GitHub Copilot integration과 연결되는 폴더입니다. 쉽게 말해 `슬래시 명령을 Copilot이 어떻게 해석할지`를 담고 있습니다.

### 1. `copilot-instructions.md`

이 파일은 Copilot에게 항상 적용되는 프로젝트 공통 지침입니다.

현재 저장소에서는 매우 짧게 다음 의미를 가집니다.

- 추가 컨텍스트가 필요하면 현재 plan을 읽어라

즉, 모든 명령의 공통 규칙이나 프로젝트 전반의 지시를 넣는 자리입니다.

### 2. `prompts/`

이 폴더는 `슬래시 명령 이름과 실제 agent를 연결하는 얇은 입구`입니다.

예를 들어 [speckit.specify.prompt.md](../.github/prompts/speckit.specify.prompt.md#L1)는 거의 내용이 없습니다.

```md
---
agent: speckit.specify
---
```

이 뜻은 다음과 같습니다.

- 사용자가 `/speckit.specify`를 입력하면
- Copilot은 `speckit.specify` agent를 실행한다

즉, `prompts/`는 `명령 라우터`에 가깝습니다.

### 3. `agents/`

이 폴더는 실제로 가장 중요한 실행 규칙이 들어 있는 곳입니다.

예를 들어 [speckit.specify.agent.md](../.github/agents/speckit.specify.agent.md#L1)를 보면 다음과 같은 내용이 들어 있습니다.

- 실행 전에 어떤 hook을 확인할지
- feature directory를 어떻게 정할지
- `spec-template.md`를 어떻게 사용할지
- 어떤 경우 `[NEEDS CLARIFICATION]`를 남길지
- spec 품질을 어떤 기준으로 검증할지

즉, `agents/`는 `이 명령이 실제로 어떤 절차로 동작해야 하는가`를 설명하는 운영 매뉴얼입니다.

### `.github/prompts`와 `.github/agents`의 차이

- `prompts/`: 어떤 agent를 호출할지 지정하는 얇은 연결 파일
- `agents/`: 그 agent가 실제로 따라야 하는 자세한 실행 규칙

초심자 관점에서는 `prompts는 입구`, `agents는 본문`이라고 기억하면 됩니다.

## `.specify` 폴더 설명

`.specify`는 Spec Kit이 실제 산출물을 만들고 확장 기능을 붙이는 데 필요한 파일들을 모아 둔 폴더입니다.

### 1. `templates/`

이 폴더는 Spec Kit 산출물의 원형이 되는 템플릿 모음입니다.

현재 저장소에 있는 템플릿:

- `constitution-template.md`
- `spec-template.md`
- `plan-template.md`
- `tasks-template.md`
- `checklist-template.md`

예를 들어 `/speckit.specify`가 실행되면, agent는 이 템플릿을 읽고 새 기능용 `spec.md`를 만듭니다. 즉, 템플릿은 `문서의 빈 양식`입니다.

### 2. `memory/`

이 폴더는 프로젝트의 지속적인 메모리를 둡니다.

현재는 `constitution.md`가 있습니다.

이 파일은 단순 참고 문서가 아니라, 이후 spec과 plan, 코드가 따라야 하는 상위 기준입니다. 따라서 `memory/constitution.md`는 프로젝트의 헌법 문서라고 봐도 됩니다.

### 3. `extensions.yml`

이 파일은 확장 기능과 hook 연결을 정리하는 중앙 설정입니다.

현재 저장소를 보면 다음 의미를 읽을 수 있습니다.

- `before_constitution` 전에 `speckit.git.initialize`를 실행
- `before_specify` 전에 `speckit.git.feature`(branch)를 실행
- `before_plan`, `before_tasks`, `before_implement` 등에서는 선택적으로 auto-commit hook 사용

즉, `extensions.yml`은 `핵심 명령 전후에 어떤 확장 명령을 끼워 넣을지`를 정하는 파일입니다.

### 4. `extensions/`

이 폴더는 Spec Kit 확장 기능이 들어가는 곳입니다. 현재 저장소에는 `git` 확장이 들어 있습니다.

`git` 확장 안에는 다음이 있습니다.

- `extension.yml`: 확장의 메타데이터, 제공 명령, hook 정의
- `commands/`: 확장이 제공하는 개별 명령 문서
- `scripts/`: bash / powershell 스크립트 구현
- `config-template.yml`: 기본 설정 템플릿
- `git-config.yml`: 현재 프로젝트에 실제 적용된 설정
- `README.md`: 영어 설명 문서

### `extensions/git/extension.yml`은 무엇을 말하는가

이 파일을 보면 git 확장이 제공하는 명령이 드러납니다.

- `speckit.git.feature`
- `speckit.git.validate`
- `speckit.git.remote`
- `speckit.git.initialize`
- `speckit.git.commit`

또한 hook도 정의합니다.

- constitution 전에 git repo 초기화
- specify 전에 feature branch 생성
- 각 단계 전후에 선택적 auto-commit

즉, 이 파일은 `이 확장이 무엇을 제공하고 언제 끼어드는가`를 설명하는 확장 명세서입니다.

### 5. `scripts/`

이 폴더는 Spec Kit이 실행 중 사용할 수 있는 도우미 스크립트가 들어 있습니다.

현재 PowerShell 기준으로는 다음이 있습니다.

- `check-prerequisites.ps1`: 준비 상태 확인
- `common.ps1`: 공통 함수
- `create-new-feature.ps1`: 새 feature 준비
- `setup-plan.ps1`: plan 관련 준비

이 파일들은 학습자가 매번 직접 열 필요는 없지만, `Spec Kit이 내부에서 어떤 운영 작업을 하는지` 이해할 때 유용합니다.

### 6. `workflows/`

이 폴더는 Workflow Engine 관련 파일을 둡니다.

현재 [workflow.yml](../.specify/workflows/speckit/workflow.yml#L1)을 보면 다음 흐름이 정의되어 있습니다.

- `specify`
- spec review gate
- `plan`
- plan review gate
- `tasks`
- `implement`

즉, 단일 명령을 각각 따로 치는 방식뿐 아니라 `승인 지점이 있는 흐름 전체`를 정의할 수 있다는 뜻입니다.

### 7. `init-options.json`

이 파일은 `specify init` 당시 선택한 옵션을 기록합니다.

현재 저장소 기준 주요 값:

- `integration: copilot`
- `branch_numbering: sequential`
- `here: true`
- `context_file: .github/copilot-instructions.md`
- `speckit_version: 0.8.3`

즉, `이 프로젝트를 어떤 방식으로 초기화했는가`를 나중에 확인할 수 있게 남겨 둔 기록입니다.

### 8. `integration.json`

이 파일은 현재 어떤 integration이 설치되었는지 간단히 기록합니다.

현재 값은 `copilot`, `0.8.3`입니다.

즉, `이 프로젝트는 Copilot integration 기준으로 구성되었다`는 짧은 표시입니다.

### 9. `integrations/speckit.manifest.json`

이 파일은 설치된 integration이 어떤 파일을 배치했는지 해시와 함께 기록하는 manifest입니다.

학습자 관점에서는 다음 정도만 알면 충분합니다.

- 초기화 시 어떤 파일이 설치되었는지 추적할 수 있다
- 무결성 확인이나 업데이트 판단에 도움을 준다

## 실제 명령이 어떻게 연결되는가

초심자가 가장 이해하기 어려운 부분은 `슬래시 명령 -> 어느 파일 -> 어떤 결과물`의 연결입니다.

### 예: `/speckit.specify`

흐름을 간단히 풀면 아래와 같습니다.

1. 사용자가 `/speckit.specify`를 입력합니다.
2. `.github/prompts/speckit.specify.prompt.md`가 `speckit.specify` agent를 가리킵니다.
3. `.github/agents/speckit.specify.agent.md`가 실행 규칙을 설명합니다.
4. agent는 `.specify/extensions.yml`에서 pre-hook이 있는지 확인합니다.
5. 필요하면 `speckit.git.feature` 같은 hook이 먼저 실행됩니다.
6. agent는 `.specify/templates/spec-template.md`를 읽습니다.
7. feature directory와 `spec.md`를 만들고 내용을 채웁니다.
8. 필요하면 `.specify/feature.json` 같은 상태 파일도 갱신합니다.

즉, `prompt -> agent -> extension hook -> template -> output 문서` 흐름으로 이해하면 됩니다.

### 예: `/speckit.constitution`

1. prompt가 constitution agent를 연결합니다.
2. constitution agent는 `.specify/memory/constitution.md`를 갱신 대상으로 봅니다.
3. 없으면 템플릿에서 생성합니다.
4. 필요하면 pre-hook으로 git 초기화를 수행합니다.
5. 결과를 constitution 문서에 반영합니다.

즉, constitution은 `template에서 출발해 memory의 실제 헌법 문서로 굳어지는 과정`입니다.

## 어떤 파일은 읽기만 하고, 어떤 파일은 수정해도 되는가

### 보통 읽기 위주로 보는 파일

- `.github/agents/*.agent.md`
- `.github/prompts/*.prompt.md`
- `.specify/integrations/*.json`
- `.specify/scripts/*`

이 파일들은 시스템 동작 방식 이해에는 좋지만, 초심자가 자주 직접 수정할 대상은 아닙니다.

### 프로젝트 커스터마이징 시 수정할 수 있는 파일

- `.github/copilot-instructions.md`
- `.specify/templates/*.md`
- `.specify/memory/constitution.md`
- `.specify/extensions.yml`
- `.specify/extensions/git/git-config.yml`

즉, `프로젝트 규칙`, `문서 템플릿`, `hook 사용 방식`, `확장 설정`은 프로젝트에 맞게 조정할 수 있습니다.

## 영어 파일을 읽을 때 번역 기준

영어 파일을 모두 정밀 번역할 필요는 없습니다. 아래 기준으로 보면 됩니다.

### `.github/agents/*.agent.md`

이 파일은 `Copilot에게 주는 작업 지시서`입니다.

읽을 때는 아래 질문만 보면 충분합니다.

- 이 명령의 입력은 무엇인가?
- 실행 전에 무엇을 확인하는가?
- 어떤 템플릿이나 파일을 읽는가?
- 최종 산출물은 무엇인가?

### `.specify/templates/*.md`

이 파일은 `최종 문서의 틀`입니다.

읽을 때는 아래를 봅니다.

- 어떤 섹션을 반드시 채워야 하는가?
- 어떤 질문을 문서에 남기게 되어 있는가?
- 어떤 산출물을 기대하는가?

### `.specify/extensions/*.yml`

이 파일은 `언제 어떤 명령을 자동으로 끼워 넣을지`를 말합니다.

읽을 때는 아래를 봅니다.

- 어떤 command를 제공하는가?
- before/after hook이 무엇인가?
- optional인지 mandatory인지?

## 학습자가 직접 해 보면 좋은 확인 명령

```powershell
Get-ChildItem -Force .github
Get-ChildItem -Force .specify
Get-ChildItem .github\agents
Get-ChildItem .github\prompts
Get-ChildItem .specify\templates
Get-Content .specify\extensions.yml
Get-Content .specify\init-options.json
```

이 정도만 읽어도 `Spec Kit이 막연한 마법이 아니라 파일 기반 워크플로`라는 점이 분명해집니다.

## 초심자용 요약

- `.github`는 `Copilot이 이 명령을 어떻게 이해할지`를 담는다.
- `.specify`는 `Spec Kit이 어떤 템플릿과 규칙으로 문서를 만들지`를 담는다.
- `prompts`는 입구, `agents`는 실행 규칙이다.
- `templates`는 문서 양식, `memory`는 프로젝트의 누적 기준, `extensions.yml`은 hook 연결표다.
- `extensions/git`은 Git 브랜치, 초기화, auto-commit을 붙여 주는 선택 확장이다.

이 구조를 이해하면 `/speckit.constitution`, `/speckit.specify`, `/speckit.plan`이 왜 서로 다른 입력을 요구하는지도 훨씬 선명하게 보입니다.