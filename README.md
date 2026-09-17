# LLM 마스터 과정 특별 교육 시리즈 — Part 5

> **바이브 코딩을 이용한 Agentic AI와 Harness 설계** — 자연어로 코드를 만들고, LLM을 도구·프로토콜과 연결해 스스로 일하는 에이전트를 설계하는 실습 중심 과정

본 저장소는 **LLM 마스터 과정 특별 교육 시리즈(총 5개 파트)** 중 **Part 5**(마지막)의 실습 자료입니다.
바이브 코딩(Vibe Coding)과 Claude Code에서 출발해 Tool Calling, MCP(Model Context Protocol), LangGraph 멀티 에이전트 워크플로우까지, LLM을 도구와 연결해 스스로 일하는 에이전트를 설계하는 과정을 2일 과정으로 다룹니다.

---

## 강의 정보

| 항목 | 내용 |
|---|---|
| **과정명** | (특별교육) [인공지능 : LLM 마스터] — **Part 5** (5개 파트 중 다섯 번째, 마지막) |
| **주제** | 바이브 코딩을 이용한 Agentic AI와 Harness 설계 |
| **일정** | 2026-09-19 ~ 09-20 · **2일 / 총 12시간** (Day 1: 6시간, Day 2: 6시간) |
| **난이도** | 고급 |
| **강사** | **김의중** (아이덴티파이 대표) |
| **교재** | **딥러닝 개념과 활용** (김의중 저) |
| **형식** | 이론 + Jupyter Notebook 실습 병행 |

---

## 학습 목표

- 바이브 코딩(Vibe Coding)의 개념과 VSCode + Claude Code 개발 환경을 이해하고 구성할 수 있다.
- Tool Calling(Function Calling)으로 LLM이 외부 도구를 호출하는 메커니즘을 구현할 수 있다.
- MCP(Model Context Protocol)로 도구를 표준화하여 여러 LLM 호스트에서 재사용할 수 있다.
- LangGraph로 Supervisor 패턴의 멀티 에이전트 워크플로우를 설계할 수 있다.

---

## 커리큘럼

### 📅 Day 1 (6시간) — 바이브 코딩과 Claude Code

| # | 세션 | 노트북 |
|---|---|---|
| 00 | 실습 환경 점검 | [setup_check.ipynb](setup_check.ipynb) |
| 01 | 자연어 처리 기초 — 인코딩, 토큰화, 임베딩(Word2Vec) | [01_nlp_encoding_tokenization.ipynb](01_nlp_encoding_tokenization.ipynb) |
| 02 | 바이브 코딩(Vibe Coding)이란? | [02_vibe_coding_intro.ipynb](02_vibe_coding_intro.ipynb) |
| 03 | Claude Code를 이용한 AI Agent 구현 실습 | [03_claude_code_agent.ipynb](03_claude_code_agent.ipynb) |

### 📅 Day 2 (6시간) — 에이전트 기술 스택 (Tool Calling → MCP → LangGraph)

| # | 세션 | 노트북 |
|---|---|---|
| 04 | Tool Calling (Function Calling)과 Agent 루프 | [04_tool_calling_function.ipynb](04_tool_calling_function.ipynb) |
| 05 | MCP(Model Context Protocol) 기반 에이전트 구현 | [05_mcp_agent.ipynb](05_mcp_agent.ipynb) |
| 06 | Agent AI 기술 스택과 LangGraph 기반 멀티 에이전트 워크플로우 | [06_agent_tech_stack_langgraph.ipynb](06_agent_tech_stack_langgraph.ipynb) |

---

## 실습 환경 설정

### VSCode 원격 접속 (Remote SSH)

실습은 AWS 서버에 접속해 진행합니다. 로컬 PC의 VSCode에서 **Remote - SSH** 확장으로 서버에 붙는 방식입니다.

1. **Remote - SSH 확장 설치** — VSCode Extensions(`Ctrl+Shift+X`)에서 `Remote - SSH` 를 검색해 설치합니다.

2. **SSH config 등록** — `~/.ssh/config`(Windows: `C:\Users\<사용자>\.ssh\config`) 파일에 접속 정보를 추가합니다.

    ```ssh-config
    Host llm_part5_aws
        HostName 3.35.71.158
        User ubuntu
        IdentityFile C:\Users\HPE\Downloads\llm_master_part5.pem
    ```

    > `HostName`(서버 IP)과 `IdentityFile`(pem 키 경로)은 발급받은 값으로 바꿔주세요.

3. **접속** — VSCode 좌측 하단 `><` 아이콘 → **Connect to Host…** → `llm_part5_aws` 선택 → 새 창에서 서버에 연결됩니다.

#### ⚠️ pem 키 권한 거부 시 (Windows PowerShell)

`Permissions for '...pem' are too open` 오류가 나면, 키 파일 권한을 본인만 읽을 수 있도록 제한합니다.

```powershell
icacls C:\경로\llm_master_part5.pem /inheritance:r
icacls C:\경로\llm_master_part5.pem /grant:r "$($env:USERNAME):(R)"
```

### Claude Code 설치 (터미널)

Session 02~03의 바이브 코딩 실습은 터미널에서 **Claude Code** CLI를 사용합니다. 서버 접속 후 터미널(`` Ctrl+` ``)에서 아래 순서로 설치합니다.

1. **Claude Code 설치** — 셋 중 하나를 선택합니다. 네이티브 설치 스크립트는 Node.js가 필요 없어 권장합니다.

    ```bash
    # (권장) 네이티브 설치 스크립트 — Node.js 불필요
    curl -fsSL https://claude.ai/install.sh | bash
    ```

    ```bash
    # npm 설치 — Node.js 18 이상 필요
    npm install -g @anthropic-ai/claude-code
    ```

    ```bash
    # macOS Homebrew
    brew install --cask claude-code
    ```

2. **PATH 확인** — 설치 후 `claude` 명령이 안 잡히면 설치 경로를 PATH에 추가합니다.

    ```bash
    export PATH="$HOME/.local/bin:$PATH"
    echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
    ```

3. **실행 및 로그인** — 프로젝트 폴더에서 `claude`를 실행하면 브라우저 로그인 창이 열립니다. Claude Pro/Max 구독 계정 또는 Anthropic Console(API) 계정으로 로그인합니다.

    ```bash
    cd ~/LLM_master_part5
    claude
    ```

4. **설치 확인**

    ```bash
    claude --version
    claude doctor
    ```

> 💡 VSCode에서는 Extensions(`Ctrl+Shift+X`)에서 `Claude Code` 확장을 설치하면 사이드 패널에서도 같은 기능을 사용할 수 있습니다.

### ANTHROPIC_API_KEY 저장 방법

Claude Code를 브라우저 로그인 대신 API 키로 사용할 때는 `ANTHROPIC_API_KEY`를 아래 세 방법 중 하나로 등록합니다.

**방법 1. 셸 환경변수** — 현재 터미널에서만 유효합니다. 터미널을 닫으면 사라집니다.

```bash
export ANTHROPIC_API_KEY="sk-ant-api03-..."
claude
```

**방법 2. Claude Code 설정 파일** — `~/.claude/settings.json`에 넣으면 터미널·VSCode 어디서든 적용됩니다.

```json
{
  "env": {
    "ANTHROPIC_API_KEY": "sk-ant-api03-...",
    "ANTHROPIC_MODEL": "claude-sonnet-5"
  }
}
```

**방법 3. VS Code 설정에 직접 넣기 (권장)** — `Cmd/Ctrl + Shift + P` → **Preferences: Open User Settings (JSON)** → 아래를 추가합니다.

```json
{
  "claudeCode.environmentVariables": [
    { "name": "ANTHROPIC_API_KEY", "value": "sk-ant-api03-..." },
    { "name": "ANTHROPIC_MODEL", "value": "claude-sonnet-5" }
  ],
  "claudeCode.disableLoginPrompt": true
}
```

> ⚠️ API 키는 절대 git에 커밋하지 마세요. 위 설정 파일들은 모두 저장소 밖(홈 디렉터리·VS Code 사용자 설정)에 있으므로 안전합니다.

### 저장소 복제 및 환경 구성

먼저 저장소를 복제합니다.

```bash
git clone https://github.com/choki0715/LLM_master_part5.git
cd LLM_master_part5
```

이후 깡통(clean) Ubuntu 상태에서 다음 스크립트로 실습 환경을 자동 구성합니다. `sudo` 없이 `uv`로 독립형 **Python 3.11**을 설치하고 가상환경을 생성합니다.

```bash
bash setup.sh
```

생성되는 가상환경:

| 환경 | 용도 |
|---|---|
| `venv` | 메인 환경 (langchain 0.3 / openai / anthropic / mcp[cli] / langgraph / fastapi / streamlit 등) — 모든 Part 5 노트북에서 사용 |
| `venv-quant` | 양자화 전용 (torch 2.2 / transformers 4.46 / auto-gptq / autoawq) — 선택 사항 |

> Python 3.11을 고정하는 이유: 최신 Python(3.14)에서는 gensim·auto-gptq·autoawq 등 다수 ML 패키지의 사전 빌드 휠이 없어 설치가 깨지기 때문입니다.

> 💡 Part 5 실습은 대부분 API 기반이라 GPU 없이 실행할 수 있습니다. 다만 다음 API 키가 필요합니다: **`OPENAI_API_KEY`**(노트북 LLM 실습), **`ANTHROPIC_API_KEY`**(Session 03 Claude Code / 바이브 코딩). 키는 노트북과 같은 폴더의 `.env` 파일에 넣어두면 자동으로 로드됩니다.

### 설치 확인

환경 구성 후 [setup_check.ipynb](setup_check.ipynb)를 실행해 주요 패키지와 GPU/CUDA 인식 여부를 점검하세요.

```bash
source venv/bin/activate
jupyter notebook   # 또는 VS Code / JupyterLab 사용
```

---

## 시리즈 구성

**LLM 마스터 과정 특별 교육 시리즈**는 총 5개 파트로 구성되며, 각 파트는 2일 / 12시간 과정입니다. (난이도: 고급)

| 파트 | 일정 | 주제 |
|---|---|---|
| Part 1 | 2026-08-08 ~ 08-09 | LLM 아키텍처 분석 및 HuggingFace, LangChain 활용 |
| Part 2 | 2026-08-15 ~ 08-16 | 모델 경량화와 추론 최적화 |
| Part 3 | 2026-08-22 ~ 08-23 | 강화학습을 통한 LLM 정렬 파인튜닝 |
| Part 4 | 2026-09-12 ~ 09-13 | 지식증강 — 벡터 RAG & 그래프 RAG & 온톨로지 RAG |
| **Part 5** *(본 저장소)* | 2026-09-19 ~ 09-20 | 바이브 코딩을 이용한 Agentic AI와 Harness 설계 |

---

## 라이선스 및 저작권

본 교육 자료의 모든 노트북과 코드는 **© AIDENTIFY. All rights reserved.**
교육 목적 외 무단 복제·배포를 금합니다.
