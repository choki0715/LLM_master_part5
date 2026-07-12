# LLM 마스터 과정 특별 교육 시리즈 — Part 5

> **바이브 코딩을 이용한 Agentic AI와 Harness 설계** — 자연어로 코드를 만들고, LLM을 도구·프로토콜과 연결해 스스로 일하는 에이전트를 설계·배포하는 실습 중심 과정

본 저장소는 **LLM 마스터 과정 특별 교육 시리즈(총 5개 파트)** 중 **Part 5**(마지막)의 실습 자료입니다.
바이브 코딩(Vibe Coding)과 Claude Code에서 출발해 Tool Calling, MCP(Model Context Protocol), A2A(Agent-to-Agent) 프로토콜, LangGraph 멀티 에이전트 워크플로우를 익히고, 데이터 파이프라인 구축 → 프로젝트 학습 → 성능 평가 → 배포까지 하나의 통합 에이전트 프로젝트를 완성하는 과정을 2일 과정으로 다룹니다.

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
- A2A(Agent-to-Agent) 프로토콜로 에이전트 간 통신 기반 멀티 에이전트 시스템을 구축할 수 있다.
- LangGraph로 Router → Specialist → Answer 형태의 멀티 에이전트 워크플로우를 설계할 수 있다.
- 데이터 파이프라인 → 프로젝트 학습 → 성능 평가(BLEU·LLM-as-a-Judge) → 배포(FastAPI·Streamlit)의 엔드투엔드 프로젝트를 완성할 수 있다.

---

## 커리큘럼

### 📅 Day 1 (6시간) — 바이브 코딩과 에이전트 프로토콜

| # | 세션 | 노트북 |
|---|---|---|
| 00 | 실습 환경 점검 | [setup_check.ipynb](setup_check.ipynb) |
| 01 | 자연어 처리 기초 — 인코딩, 토큰화, 임베딩(Word2Vec) | [01_nlp_encoding_tokenization.ipynb](01_nlp_encoding_tokenization.ipynb) |
| 02 | 바이브 코딩(Vibe Coding)이란? | [02_vibe_coding_intro.ipynb](02_vibe_coding_intro.ipynb) |
| 03 | Claude Code를 이용한 AI Agent 구현 실습 | [03_claude_code_agent.ipynb](03_claude_code_agent.ipynb) |
| 04 | Tool Calling (Function Calling) 개념 | [04_tool_calling_function.ipynb](04_tool_calling_function.ipynb) |
| 05 | MCP(Model Context Protocol) 기반 에이전트 구현 | [05_mcp_agent.ipynb](05_mcp_agent.ipynb) |
| 06 | A2A(Agent-to-Agent) 프로토콜 기반 멀티 에이전트 | [06_a2a_protocol.ipynb](06_a2a_protocol.ipynb) |

### 📅 Day 2 (6시간) — 기술 스택과 통합 프로젝트 (파이프라인 → 학습 → 평가 → 배포)

| # | 세션 | 노트북 |
|---|---|---|
| 07 | Agent AI 기술 스택과 LangGraph 기반 멀티 에이전트 워크플로우 | [07_agent_tech_stack_langgraph.ipynb](07_agent_tech_stack_langgraph.ipynb) |
| 08 | 프로젝트 데이터 파이프라인 구축 | [08_data_pipeline_training.ipynb](08_data_pipeline_training.ipynb) |
| 09 | 프로젝트 학습 — MCP + LangGraph + A2A 통합 에이전트 | [09_project_training.ipynb](09_project_training.ipynb) |
| 10 | 프로젝트 성능 평가 및 반복 개선 | [10_evaluation.ipynb](10_evaluation.ipynb) |
| 11 | 프로젝트 배포 — FastAPI + Streamlit | [11_deployment.ipynb](11_deployment.ipynb) |

---

## 실습 환경 설정

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
