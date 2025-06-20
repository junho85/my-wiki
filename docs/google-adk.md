# Google ADK (Agent Development Kit) 소개

Google ADK(Agent Development Kit)는 Google에서 제공하는 에이전트(Agent) 개발을 위한 도구 및 프레임워크입니다. ADK를 활용하면 다양한 플랫폼과 서비스에서 동작하는 지능형
에이전트를 쉽고 빠르게 개발할 수 있습니다.

## 왜 ADK인가? 더 나은 에이전트 개발의 필요성

정교하고 프로덕션 수준의 AI 에이전트 구축은 복잡하고 시간이 많이 소요됩니다. 특히 다중 에이전트 및 다중 모달 시스템에서는 이러한 어려움이 더욱 두드러집니다.

- **다중 모달 시스템(Multi-modal System)**: 여러 형태의 데이터나 입력(예: 텍스트+이미지, 음성+텍스트, 비디오+오디오+텍스트 등)을 동시에 처리하고 이해할 수 있는 AI 시스템을 의미합니다.
- Google의 내부적 경험이 이러한 복잡성을 줄이기 위한 ADK 생성의 원동력이 되었습니다.

## ADK의 핵심 원칙

- **모델 독립적**: Google Gemini 또는 다른 LLM(대형 언어 모델) 사용 가능
- **배포 독립적**: 로컬, Google Cloud 또는 기타 인프라에서 실행 가능
- **상호 운용성**: 기존 서비스 또는 다른 프레임워크의 에이전트와 통합 가능

## 핵심 개념 (Core Concepts)

ADK는 강력하고 유연한 에이전트 개발을 가능하게 하는 몇 가지 핵심 원시 타입과 개념을 중심으로 구축되었습니다.

### 에이전트 (Agent)

특정 작업을 위해 설계된 기본 작업 단위입니다. 에이전트는 의사 결정을 내리고 작업을 수행하는 중심적인 역할을 합니다.

1. **LLM 에이전트 (LlmAgent)**
    - 복잡한 추론을 위해 언어 모델을 사용
    - 동적이고 언어 중심적인 작업에 이상적
2. **워크플로우 에이전트**
    - **SequentialAgent**: 하위 에이전트를 순서대로 실행
    - **ParallelAgent**: 하위 에이전트를 동시에 실행
    - **LoopAgent**: 특정 조건이 충족될 때까지 하위 에이전트를 반복 실행
3. **사용자 정의 에이전트**
    - BaseAgent를 상속하여 맞춤형 로직 구현 가능

### 도구 (Tool)

에이전트에게 대화 이상의 능력을 부여하여 외부 API와 상호작용하고, 정보를 검색하고, 코드를 실행하거나 다른 서비스를 호출할 수 있게 합니다.

1. **함수 도구 (FunctionTool)**
    - 개발자가 직접 정의하는 파이썬 함수
2. **내장 도구**
    - SearchTool: Google 검색 기능
    - CodeExecutionTool: 코드 실행 기능
    - RAG(Retrieval-Augmented Generation) 등
3. **툴셋 (BaseToolset)**
    - 여러 도구를 동적으로 관리하는 컬렉션

### 콜백 (Callbacks)

에이전트 프로세스의 특정 시점에서 실행되도록 제공하는 사용자 정의 코드 스니펫으로, 검사, 로깅 또는 동작 수정을 가능하게 합니다.

### 세션 관리 (Session Management)

- **Session**: 단일 대화의 컨텍스트를 처리
- **State**: 해당 대화에 대한 에이전트의 작업 메모리
- **Events**: 대화 기록

### 메모리 (Memory)

에이전트가 여러 세션에 걸쳐 사용자에 대한 정보를 기억할 수 있게 하여 장기적인 컨텍스트를 제공합니다(단기 세션 State와는 구별됨).

### 아티팩트 관리 (Artifact Management)

세션이나 사용자와 연관된 파일 또는 바이너리 데이터(이미지, PDF 등)를 저장, 로드 및 관리할 수 있게 합니다.

### 코드 실행 (Code Execution)

에이전트(주로 도구를 통해)가 복잡한 계산이나 작업을 수행하기 위해 코드를 생성하고 실행하는 능력입니다.

### 계획 (Planning)

에이전트가 복잡한 목표를 더 작은 단계로 분해하고 ReAct 플래너와 같이 이를 달성하는 방법을 계획할 수 있는 고급 기능입니다.

### 모델 (Models)

LlmAgent를 구동하는 기본 LLM으로, 추론 및 언어 이해 능력을 가능하게 합니다.

### 이벤트 (Event)

세션 중에 발생하는 일(사용자 메시지, 에이전트 응답, 도구 사용)을 나타내는 기본 통신 단위로, 대화 기록을 형성합니다.

### 러너 (Runner)

실행 흐름을 관리하고, 이벤트를 기반으로 에이전트 상호작용을 조율하며, 백엔드 서비스와 조정하는 엔진입니다.

## 주요 특징

- **확장성**: 다양한 플랫폼(웹, 모바일, IoT 등)에서 에이전트를 개발하고 배포할 수 있습니다.
- **표준화된 인터페이스**: Google의 표준 API와 연동이 용이하며, 음성, 텍스트 등 다양한 입력 방식 지원
- **통합 개발 환경**: 개발, 테스트, 배포를 위한 통합 도구 제공
- **보안 및 개인정보 보호**: Google의 보안 정책과 가이드라인을 따름

## 활용 예시

- 챗봇, 가상 비서, IoT 기기 제어 에이전트 등 다양한 인공지능 기반 서비스 개발

## 참고 자료

- [Agent Development Kit](https://google.github.io/adk-docs/) 
