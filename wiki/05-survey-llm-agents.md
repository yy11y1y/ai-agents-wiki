# 05 · A Survey on LLM-based Autonomous Agents

**來源**：Wang et al., "A Survey on Large Language Model based Autonomous Agents"（arXiv:2308.11432）
**連結**：https://arxiv.org/abs/2308.11432
**類型**：綜述論文（整體視角）
**ingest 日期**：2026-11-23

---

## 一句話摘要
從整體視角把 LLM-based agent 的研究整理成三大面向：**構成（construction）／應用（application）／評估（evaluation）**，並提出一個可涵蓋多數前人工作的統一框架。

## 關鍵概念

### 1. Construction（怎麼建一個 Agent）
提出統一框架來描述 agent 的構成（架構與能力的取得）。對應本 Wiki 的三元件視角：
把 [[02-lilian-weng-llm-agents]] 的 Planning / Memory / Tool use 放進一個更一般化的「agent 架構」裡討論。

### 2. Application（用在哪）
系統性整理 agent 在三類領域的應用：
- **社會科學 (social science)**
- **自然科學 (natural science)**
- **工程 (engineering)**
→ 說明 agent 不只是 chatbot，而是能參與模擬、研究、自動化任務的角色。

### 3. Evaluation（怎麼評估）
整理常見的評估策略——這點很關鍵，因為 Agent 的「對不對」比單次問答難量化。
呼應 [[02-lilian-weng-llm-agents]] 提到的限制：長程任務、可靠度難以評估。

## 為什麼把這篇放進 Wiki
前 4 篇都是「某個元件或某個方法」的深入；這篇提供**鳥瞰地圖**，讓初學者知道：
- 這些方法各自落在 construction 的哪一塊；
- Agent 真正落地還要面對 application 與 evaluation 的問題。

## 與其他頁的連結
- 把 [[01-anthropic-building-effective-agents]]～[[04-reflexion]] 收攏成一張研究地圖。
- Evaluation 一節是本 Wiki「限制」主題的主要依據之一。
