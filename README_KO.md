# 나의 AI 스택

[English](README.md) | 한국어

2025년 현재 내가 실제로 사용하고 있는 AI 기반 개발 환경. 단순히 코드를 작성하는 것이 아니라, AI 에이전트를 오케스트레이션하여 더 빠르고 더 좋은 소프트웨어를 만든다.

## 핵심: Claude Code + oh-my-claudecode

[Claude Code](https://claude.ai/code)는 나의 주력 AI 코딩 어시스턴트 (CLI).
그 위에 [oh-my-claudecode (OMC)](https://github.com/anthropics/oh-my-claudecode)를 올려서 Claude Code를 풀 개발 플랫폼으로 확장하여 사용한다.

### 왜 Claude Code인가?

- 터미널 네이티브 — 이미 작업하는 환경에서 바로 동작
- 자율적 멀티 스텝 실행이 가능한 에이전트 모드
- MCP (Model Context Protocol) 지원으로 기능 확장 가능
- 세션 간 지속되는 대화 컨텍스트

### oh-my-claudecode (OMC) v4.9.3

OMC는 Claude Code 위에 위임 우선(delegation-first) 아키텍처를 추가한다:

```
사용자 요청
    │
    ▼
┌─────────────────┐
│   오케스트레이터  │  ← 전문 에이전트에게 작업 라우팅
│  (Claude Opus)   │
└────────┬────────┘
         │
    ┌────┼────┬────────┬──────────┐
    ▼    ▼    ▼        ▼          ▼
 탐색   실행   디자인   아키텍트  리서치
(Haiku) (Sonnet) (Sonnet) (Opus)  (Sonnet)
```

**32개 전문 에이전트** — 3단계 모델 티어:

| 티어 | 모델 | 용도 | 에이전트 |
|------|------|------|----------|
| LOW | Haiku | 빠른 조회, 간단한 수정 | `explore`, `executor-low`, `architect-low`, `writer` |
| MEDIUM | Sonnet | 일반 구현, UI, 테스트 | `executor`, `designer`, `researcher`, `qa-tester` |
| HIGH | Opus | 아키텍처, 심층 디버깅, 보안 | `architect`, `planner`, `critic`, `security-reviewer` |

**주요 실행 모드:**

| 모드 | 설명 |
|------|------|
| **Autopilot** | 아이디어에서 동작하는 코드까지 완전 자율 실행 |
| **Ultrawork** | 여러 에이전트를 활용한 최대 병렬 실행 |
| **Ralph** | 검증 완료될 때까지 멈추지 않는 지속 루프 |
| **Team** | N개 에이전트가 공유 작업 목록에서 협업 |
| **Pipeline** | 순차적 에이전트 체이닝 (예: 탐색 → 아키텍트 → 실행) |

## MCP 서버

Model Context Protocol 서버로 Claude Code의 기능을 확장:

| 서버 | 용도 |
|------|------|
| **Context7** | 실시간 라이브러리/프레임워크 공식 문서 조회 |
| **Framer** | 디자인 도구 연동 — CMS, 페이지, 코드 파일 |
| **Gmail** | 이메일 연동 |
| **Google Calendar** | 캘린더 연동 |

## gstack 스킬 (30+)

Claude Code 위에 구축된 프로덕션급 워크플로우:

| 카테고리 | 스킬 | 기능 |
|----------|------|------|
| **QA & 테스트** | `/qa`, `/qa-only`, `/browse` | 헤드리스 브라우저 QA, 버그 탐지, 시각적 테스트 |
| **코드 리뷰** | `/review`, `/plan-eng-review` | 머지 전 diff 리뷰, 아키텍처 리뷰 |
| **배포** | `/ship`, `/land-and-deploy` | PR 생성, CI/CD, 배포 검증 |
| **기획** | `/plan-ceo-review`, `/plan-eng-review`, `/plan-design-review` | 다각도 기획 리뷰 (CEO, 엔지니어링, 디자인) |
| **디자인** | `/design-consultation`, `/design-review` | 디자인 시스템 생성, 시각적 QA |
| **보안** | `/cso` | OWASP Top 10, STRIDE 위협 모델링, 의존성 감사 |
| **모니터링** | `/canary`, `/benchmark` | 배포 후 카나리 체크, 성능 회귀 감지 |
| **문서화** | `/document-release`, `/retro` | 릴리스 문서, 주간 회고 |

## 기타 AI 도구

| 도구 | 역할 | 사용 시점 |
|------|------|-----------|
| **OpenAI Codex CLI + OMX** | 독립적 세컨드 오피니언 | 크로스 모델 코드 리뷰, 적대적 기획 검증. OMX (Oh My codeX)로 Codex에도 멀티 에이전트 오케스트레이션 적용 |
| **Antigravity** | AI 기반 개발 환경 | 시각적 컨텍스트를 활용한 협업형 AI 코딩 |
| **Cursor** | 비주얼 AI 코드 에디터 | 시각적 diff/컨텍스트가 필요할 때 |
| **VS Code** | 전통적 IDE | 익스텐션, 디버깅 UI, git 연동 |

## 플러그인

| 플러그인 | 용도 |
|----------|------|
| **oh-my-claudecode** | 멀티 에이전트 오케스트레이션 레이어 |
| **swift-lsp** | iOS 개발을 위한 Swift 언어 서버 프로토콜 지원 |

## HUD (헤드업 디스플레이)

실시간 에이전트 활동을 보여주는 커스텀 상태 표시줄:

```
node ~/.claude/hud/omc-hud.mjs
```

표시 항목: 활성 모드, 실행 중인 에이전트, 작업 진행 상황, 모델 사용량 — 터미널 상태바에서 한눈에 확인.

## 나의 워크플로우

일반적인 기능 개발 흐름:

```
1. 원하는 것을 설명         →  "autopilot: X를 위한 REST API 만들어줘"
2. OMC가 자동으로 기획      →  코드베이스 탐색, 계획 수립
3. 에이전트가 병렬 실행     →  executor가 코드 작성, designer가 UI 담당
4. 검증 실행               →  architect가 리뷰, 테스트 통과
5. 배포                    →  /ship으로 PR 생성, CI 실행
6. 모니터링                →  /canary로 프로덕션 감시
```

## 철학

- **AI 네이티브 개발** — AI는 자동완성이 아니라 전문가 팀이다
- **직접 하기보다 위임** — 적절한 에이전트에게 적절한 모델 티어로 라우팅
- **완료 전 검증** — 증거 없이 완료를 선언하지 않는다
- **멀티 모델 합의** — 중요한 결정은 서로 다른 AI 모델로 교차 검증

---

*이 문서는 스택이 변화함에 따라 지속적으로 업데이트됩니다.*
