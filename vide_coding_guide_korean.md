# Vibe 코딩 시작하기

Vibe 코딩을 시작하려면 두 가지 도구만 있으면 됩니다:

- **Gemini 2.5 Pro Thinking**  
- **Cursor with Claude Sonnet 4 Thinking**  

모든 것을 올바르게 설정하는 것이 핵심입니다. 완전히 기능적이고 시각적으로 매력적인 게임을 만드는 것에 진지하다면, 견고한 기반을 구축하는 데 시간을 투자하세요.

**핵심 원칙:** *계획이 전부입니다.* AI가 자율적으로 계획하도록 두지 마세요. 그렇지 않으면 코드베이스가 관리할 수 없는 혼란이 될 것입니다.

---

## 계획 세우기

### 1. 게임 디자인 문서

- 게임 아이디어를 가지고 **Gemini 2.5 Pro Thinking**에게 마크다운 형식으로 간단한 **게임 디자인 문서**를 만들어달라고 요청하세요: `game-design-document.md`.  
- 문서를 검토하고 개선하여 비전과 일치하는지 확인하세요. 기본적이어도 괜찮습니다—목표는 AI에게 게임의 구조와 의도에 대한 맥락을 제공하는 것입니다.

### 2. 기술 스택과 `.cursor/rules`

- **Gemini 2.5 Pro Thinking**에게 게임에 가장 적합한 기술 스택을 추천해달라고 요청하세요(예: 멀티플레이어 3D 게임을 위한 ThreeJS와 WebSocket). 이를 `tech-stack.md`로 저장하세요.
  - *가능한 한 가장 간단하면서도 가장 견고한 스택*을 제안하도록 도전시키세요.
- Cursor에서 채팅을 열고 지금까지 만든 두 개의 .md 파일을 선택한 상태에서 `/Generate Cursor Rules` 명령을 사용하세요. 이렇게 하면 `.cursor/rules` 아래에 규칙 세트 `.mdc`가 생성됩니다.
- **중요하게, 생성된 규칙들을 검토하세요.** 규칙들이 **모듈성**(여러 파일)을 강조하고 **모놀리스**(하나의 거대한 파일)를 억제하는지 확인하세요. 수동으로 조정하거나 규칙을 추가해야 할 수도 있습니다. 언제 규칙이 발동되는지도 검토하세요.
  - **중요:** 일부 규칙은 컨텍스트를 유지하는 데 중요하며 Cursor에서 **"Always"** 규칙으로 설정해야 합니다. 이렇게 하면 AI가 코드를 생성하기 전에 *항상* 이러한 규칙들을 참조합니다. 다음과 같은 규칙을 추가하고 "Always"로 표시하는 것을 고려하세요:
>
    > ```
    > # 중요:
    > # 코드를 작성하기 전에 항상 memory-bank/@architecture.md를 읽어라. 전체 데이터베이스 스키마를 포함하라.
    > # 코드를 작성하기 전에 항상 memory-bank/@game-design-document.md를 읽어라.
    > # 주요 기능을 추가하거나 마일스톤을 완료한 후, memory-bank/@architecture.md를 업데이트하라.
    > ```
>
  - 예시: 다른 (비-"Always") 규칙들이 AI를 스택의 모범 사례(네트워킹, 상태 관리 등)로 안내하도록 하세요.
  - *이 전반적인 규칙 설정은 가능한 한 최적화된 게임과 가능한 한 깨끗한 코드를 원한다면 필수입니다.*

### 3. 구현 계획

- **Gemini 2.5 Pro Thinking**에게 다음을 제공하세요:
  - 게임 디자인 문서 (`game-design-document.md`)
  - 기술 스택 추천사항 (`tech-stack.md`)
  - 방금 구성한 Cursor 규칙들 (`.cursor/rules` 파일에서 복사-붙여넣기 가능)
- AI 개발자들을 위한 단계별 지침인 마크다운(`.md`) 형식의 자세한 **구현 계획**을 만들어달라고 요청하세요.
  - 단계들은 작고 구체적이어야 합니다.
  - 각 단계는 올바른 구현을 검증하기 위한 테스트를 포함해야 합니다.
  - 코드는 없고—명확하고 구체적인 지침만 있어야 합니다.
  - 전체 기능 세트가 아닌 *기본 게임*에 초점을 맞추세요 (세부사항은 나중에).

### 4. 메모리 뱅크

- 프로젝트를 위한 새 폴더를 만들고 Cursor에서 여세요.
- 프로젝트 폴더 내에 `memory-bank`라는 하위 폴더를 만드세요.
- `memory-bank`에 다음 파일들을 추가하세요:
  - `game-design-document.md`
  - `tech-stack.md`
  - `implementation-plan.md`
  - `progress.md` (완료된 단계를 추적하기 위한 빈 파일 생성)
  - `architecture.md` (파일 목적을 문서화하기 위한 빈 파일 생성)
- *참고: `.cursor/rules` 파일은 2단계에서 규칙을 저장할 때 Cursor에 의해 프로젝트 루트 디렉터리에 자동으로 생성됩니다.*

---

## 기본 게임 Vibe 코딩하기

이제 재미있는 부분이 시작됩니다!

### 모든 것이 명확한지 확인하기

- Cursor에서 **Claude Sonnet 4 Thinking**을 선택하세요.
- 프롬프트: `/memory-bank`의 모든 문서를 읽어보세요. `implementation-plan.md`가 명확한가요? 100% 명확하게 만들기 위한 질문은 무엇인가요?
- 보통 9-10개의 질문을 하는데, 답변하고 그에 따라 `implementation-plan.md`를 편집하여 더 나아지도록 프롬프트하세요.

### 첫 번째 구현 프롬프트

- Cursor에서 **Claude Sonnet 4 Thinking**을 선택하세요.
- 프롬프트: `/memory-bank`의 모든 문서를 읽고 구현 계획의 1단계를 진행하세요. 제가 테스트를 실행하겠습니다. 제가 테스트를 검증할 때까지 2단계를 시작하지 마세요. 제가 검증하면 `progress.md`를 열고 미래 개발자들을 위해 한 일을 문서화하세요. 그런 다음 각 파일이 무엇을 하는지 설명하기 위해 `architecture.md`에 아키텍처 인사이트를 추가하세요.

### 워크플로우

- 1단계 완료 후:
- Git에 변경사항을 커밋하세요 (익숙하지 않다면 Gemini 2.5에게 도움을 요청).
- 새 composer를 시작하세요 (`Cmd + N`, `Cmd + I`).
- 프롬프트: 이제 memory-bank의 모든 파일을 살펴보고, progress.md를 읽어 이전 작업을 이해한 다음 2단계를 진행하세요. 제가 테스트를 검증할 때까지 3단계를 시작하지 마세요.
- 전체 `implementation-plan.md`가 완료될 때까지 이 과정을 반복하세요.

---

## 세부사항 추가하기

- 각 주요 기능에 대해 짧은 단계와 테스트가 포함된 새로운 `feature-implementation.md` 파일을 만드세요.
- 점진적으로 구현하고 테스트하세요.

---

## 버그 수정 및 막힘 해결

- 프롬프트가 실패하거나 게임이 망가지면:
- Cursor에서 "restore"를 클릭하고 작동할 때까지 프롬프트를 개선하세요.
- 오류의 경우:
- **JavaScript 오류의 경우:** 콘솔(`F12`)을 열고, 오류를 복사하여 Cursor에 붙여넣기—또는 시각적 결함의 경우 스크린샷을 제공하세요.
- **Lazy 옵션:** 수동 복사/스크린샷을 건너뛰기 위해 [BrowserTools](https://browsertools.agentdesk.ai/installation)를 설치하세요.
- 막혔다면:
- 마지막 Git 커밋으로 되돌리고 (`git reset`) 새로운 프롬프트로 다시 시도하세요.
- *정말* 막혔다면:
- [RepoMix](https://repomix.com/)를 사용하여 전체 코드베이스를 하나의 파일로 만들고 **Gemini 2.5 Pro Thinking**에게 도움을 요청하세요.

---

## 기타

- **더 좋은 프롬프트 출력:** "think as long as needed to get this right, I am not in a hurry. What matters is that you follow precisely what I ask you and execute it perfectly. Ask me questions if I am not precise enough."를 추가하세요.
