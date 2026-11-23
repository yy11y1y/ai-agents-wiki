# 01 · Building Effective Agents（Anthropic）

**來源**：Anthropic Engineering, "Building Effective Agents"（Erik Schluntz & Barry Zhang, 2024/12）
**連結**：https://www.anthropic.com/engineering/building-effective-agents
**類型**：工程實務指南
**ingest 日期**：2026-11-23

---

## 一句話摘要
最成功的 Agent 多半不是靠複雜框架，而是靠**簡單、可組合的模式**；關鍵在於分清楚 **workflow** 與 **agent**，並從最簡單的解法開始，只在必要時才增加複雜度。

## 關鍵概念

### 1. Agentic systems（代理式系統）＝ 總稱
Anthropic 把所有變體統稱 agentic systems，但在架構上做一個重要區分：
- **Workflow（工作流）**：LLM 與工具被「預先寫好的程式路徑」編排（predefined code paths）。可預測、一致。
- **Agent（代理人）**：LLM **動態主導**自己的流程與工具使用，"maintaining control over how they accomplish tasks"。

### 2. 基本單元：Augmented LLM（增強型 LLM）
一切的 building block＝「加上檢索（retrieval）、工具（tools）、記憶（memory）」的 LLM。
現代模型能自己產生查詢、選工具、決定要記住什麼。

### 3. 五種 Workflow 模式（重要！簡報會用到）
| 模式 | 做法 | 何時用 |
|------|------|--------|
| **Prompt chaining** 提示鏈 | 拆成循序步驟，每步吃上一步輸出；步驟間可加「gate」檢查 | 任務可清楚拆成固定步驟；用延遲換準確度 |
| **Routing** 路由 | 先分類輸入，再送到專門的提示／模型 | 不同類型輸入要分流（簡單問題給小模型） |
| **Parallelization** 平行化 | *Sectioning*（拆成獨立子任務同時做）或 *Voting*（同任務跑多次取共識） | 子任務可平行；或需多次嘗試提高信心 |
| **Orchestrator-workers** 協調者–工人 | 中央 LLM 動態拆任務、分派給 worker、再整合 | 子任務無法事先寫死，要看輸入才知道 |
| **Evaluator-optimizer** 評估–優化 | 一個 LLM 生成、另一個評估回饋，形成迴圈 | 有明確評估標準、且迭代確實有幫助 |

### 4. Agent 的迴圈怎麼運作
- 從人類的指令或討論開始 → 之後**自主**規劃與行動，必要時回來找人確認。
- 每一步都從**環境取得 ground truth**（工具結果、程式執行輸出）來評估進度。
- 通常有**停止條件**（例如最大迭代次數）或在檢查點暫停。
- 機制上：就是「LLM 根據環境回饋、在迴圈中使用工具」。

### 5. 何時用 agent、何時用 workflow
- **先找最簡單的解**，常常「單次 LLM 呼叫＋檢索＋範例」就夠了。
- **Workflow**：任務定義清楚、要可預測與一致性。
- **Agent**：開放式問題、步數無法預測或寫死、需要彈性。
- 代價：Agent 更貴、會**累積錯誤**，要在 sandbox 大量測試並加 guardrails。

### 6. 工具設計（ACI）
- 工具定義值得跟 prompt 一樣用心做 prompt engineering。
- 設計「Agent–Computer Interface (ACI)」：清楚文件、使用範例、邊界。
- 用 "poka-yoke"（防呆）讓工具難以被誤用（例：要求絕對路徑消除相對路徑錯誤）。

## 與其他頁的連結
- 「augmented LLM＝檢索＋工具＋記憶」呼應 [[02-lilian-weng-llm-agents]] 的 Memory／Tool use。
- 「迴圈＋環境回饋」是 [[03-react]] 的工程化版本。
- 「停止條件、累積錯誤」是 [[04-reflexion]] 想處理的問題之一。

## 可直接拿去教學的金句（短引用）
- Agents：LLM "maintaining control over how they accomplish tasks."
