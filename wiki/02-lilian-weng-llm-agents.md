# 02 · LLM Powered Autonomous Agents（Lilian Weng）

**來源**：Lilian Weng（OpenAI），"LLM Powered Autonomous Agents"（2023/06/23，Lil'Log）
**連結**：https://lilianweng.github.io/posts/2023-06-23-agent/
**類型**：技術綜述／經典架構文
**ingest 日期**：2026-11-23

---

## 一句話摘要
提出最被廣泛引用的架構：**Agent＝以 LLM 為大腦（brain）＋ Planning ＋ Memory ＋ Tool use**。重點是：Agent 不是「一顆更強的模型」，而是**一個結構**。

## 關鍵概念

### 核心架構圖（文字版）
```
            ┌─────────── Planning 規劃 ───────────┐
            │  任務拆解 (CoT / Tree of Thoughts)   │
            │  自我反思 (ReAct / Reflexion)        │
            └─────────────────────────────────────┘
                              │
   Memory 記憶 ─────────→  [ LLM 大腦 ]  ←───────── Tool use 工具
   短期：context window        核心控制器        呼叫外部 API / 程式
   長期：外部向量庫 (MIPS)
```

### 1. Planning（規劃）
- **任務拆解 Task decomposition**：把大任務拆成小而可管理的子目標。
  - *Chain of Thought (CoT)*：要求模型「一步一步想」。
  - *Tree of Thoughts*：每步產生多個候選想法，像樹一樣搜尋。
  - *LLM+P*：把長程規劃交給外部古典規劃器，LLM 負責把問題翻成 PDDL 再翻回來。
- **自我反思 Self-reflection**：從過去行動中學習、修正未來決策。
  - *ReAct*、*Reflexion* 歸在這裡（詳見 [[03-react]]、[[04-reflexion]]）。

### 2. Memory（記憶）
- **短期記憶**：放在 context window 裡的資訊（如 in-context learning）；**有限**。
- **長期記憶**：外部儲存，通常是**向量資料庫**，用快速近似最近鄰（MIPS/ANN）查詢，突破 context 限制。

### 3. Tool use（工具使用）
- 呼叫外部 API／程式，補足模型本身缺的能力（如即時資料、程式執行）。
- *MRKL*：一個通用 LLM 把查詢路由給「專家模組」（可為神經或符號式，如計算機）。
- *Toolformer*：微調模型，讓它自己決定何時、如何呼叫工具 API。
- *API-Bank*：評測工具增強型 LLM 的 benchmark。

### 4. 已知挑戰（限制）
- **有限的 context length**：限制可用的歷史／指令／工具輸出；檢索有幫助但不如完整 attention。
- **長程規劃困難**：在長歷史上規劃、以及從意外錯誤中恢復，仍很難。
- **自然語言介面不可靠**：模型會格式錯誤或不照指令，很多 agent 程式碼都在解析輸出。

## 與其他頁的連結
- 三元件（Planning/Memory/Tool）是本 Wiki 的骨架；[[01-anthropic-building-effective-agents]] 的 augmented LLM 是其工程化說法。
- Planning 下的 self-reflection 直接展開成 [[03-react]] 與 [[04-reflexion]]。
- 限制一節呼應 [[05-survey-llm-agents]] 的 evaluation 難題。
