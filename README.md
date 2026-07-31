# Korean Writing Reviewer

한국어 문서의 교정, 문체 개선, 구조 정리와 선택적 품질 평가를 위한 Agent Skill입니다.

같은 한국어 검토 기준을 두 개의 독립 설치본으로 제공합니다.

| 환경 | 설치본 |
|---|---|
| Claude Code, Codex, Hermes, VS Code 기반 에이전트 및 일반 Agent Skills 환경 | `skills/general-agent/` |
| Obsidian YOLO | `skills/obsidian-yolo/` |

두 설치본을 같은 환경에 동시에 설치하지 마십시오. 필요한 폴더 하나만 선택합니다.

## 주요 기능

- 원문·인용·수치·조건·코드·링크·고유명사 보호
- 한국어 맞춤법, 띄어쓰기, 호응, 조사·어미와 높임 검토
- 번역투, 과도한 명사화, 반복되는 종결형과 AI 상투 문체 검토
- 대본·보고서·기술 문서 등 9개 문서 유형별 기준
- 어문 규범 확인과 사실 확인의 분리
- 긴 문서의 섹션 단위 처리와 전체 일관성 재검사
- 문서 유형별 100점 평가
- `evaluate / improve / evaluate-and-improve` 작업 모드
- 평가 전 원문 고정과 수정 여부 명시
- 점수제의 조건부 실행
- 최소 수정과 원문 역검증

## 지원 문서 유형

- 대본
- 업무 보고서·공공 문서
- 기술 문서
- 이메일·메시지
- 개인 메모·지식 노트
- 조사·학습 자료
- 회의록·프로젝트 기록
- 게시글·댓글
- 일반 설명문·교육 자료

## 저장소 구조

```text
korean-writing-reviewer/
├── README.md
├── LICENSE
├── CHANGELOG.md
└── skills/
    ├── general-agent/
    │   ├── SKILL.md
    │   └── references/
    │       ├── common-criteria.md
    │       ├── document-profiles.md
    │       ├── editor-protection.md
    │       ├── long-document-workflow.md
    │       ├── korean-ai-patterns.md
    │       ├── examples.md
    │       ├── scoring-common.md
    │       ├── scoring-*.md
    │       ├── scoring-examples.md
    │       └── source-basis.md
    └── obsidian-yolo/
        ├── SKILL.md
        └── references/
            └── ...
```

각 설치 폴더는 다른 폴더에 의존하지 않는 완전한 스킬 패키지입니다.

## General Agent 설치

`skills/general-agent/`의 내용을 사용하는 에이전트의 스킬 폴더 안에 `korean-writing-reviewer`라는 폴더로 복사합니다.

예시:

```text
<agent-skills-dir>/korean-writing-reviewer/
├── SKILL.md
└── references/
```

대상 환경의 실제 스킬 경로와 편집 도구 규칙을 따르십시오. 이 설치본은 특정 편집기 DSL을 강제하지 않습니다.

## Obsidian YOLO 설치

`skills/obsidian-yolo/`의 내용을 볼트의 다음 위치에 복사합니다.

```text
<Obsidian Vault>/YOLO/skills/korean-writing-reviewer/
├── SKILL.md
└── references/
```

YOLO 설치본은 `mode: always`를 사용하지만 다음 작업에는 문장 검토를 확대 적용하지 않습니다.

- 코드만 생성하는 작업
- 파일 이동·삭제·이름 변경
- 단순 경로·설정 조작
- 한국어 자연어 결과가 없는 작업

기존 Markdown 파일의 편집 출력은 YOLO의 `obsidian-output-format` 규칙을 따릅니다.

## 작업 모드

평가와 개선을 분리합니다.

| 모드 | 동작 |
|---|---|
| `evaluate` | 현재 문서 원문을 평가하고 수정하지 않음 |
| `improve` | 점수 없이 최소 수정 |
| `evaluate-and-improve` | 원문 평가 → 개선 → 수정본 재평가 |

예를 들어 `평가해 줘`는 현재 원문만 평가합니다. `평가하고 개선해 줘`라고 요청해야 원문 점수 산출 후 수정과 재평가를 수행합니다.

평가 결과에는 다음을 명시합니다.

- 평가 대상
- 문서 수정 여부
- 원문 점수와 수정본 점수의 구분

## 점수 평가

점수표는 일반 교정 때 자동으로 실행하지 않습니다. 평가 요청에서는 현재 원문을 수정하지 않고 점수를 산출하며, 개선까지 명시한 경우에만 원문 평가 후 수정하고 재평가합니다.

다음 경우에 점수표를 적용합니다.

- 사용자가 점수나 등급을 요청함
- 출판·제출·배포 전 최종 검수
- 여러 수정본 비교
- 품질 회귀 평가 또는 자동화
- 문서 전체의 엄격한 평가 요청

일반 작성·교정에서는 `BLOCK / FIX / REVIEW / KEEP`, 최소 수정과 역검증만 적용합니다.

## 기준 자료

한국어 어문 규범, 공공언어와 언어 예절 자료를 참고하되 원문 자료와 평가표를 복제하지 않고 독자적으로 재구성했습니다. 세부 출처와 활용 범위는 각 설치본의 `references/source-basis.md`에 정리되어 있습니다.

## 라이선스

MIT License
