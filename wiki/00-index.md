# LLM Wiki：AI Agents（AI 代理人）

> 知識庫主題：AI Agents 的核心概念、組成元件、設計模式與限制
> 建立方式：先與 LLM 討論主題範圍與 schema，再逐篇 ingest 來源、抽取重點、交叉比對後寫入
> Ingest 來源數：5 篇（見下方清單）
> 最後更新：2026-11-23

---

## 這個 Wiki 想回答的問題

1. 什麼是 AI Agent？它和一般「呼叫一次 LLM」有什麼不同？
2. 一個 Agent 由哪些元件組成？
3. Workflow（工作流）和 Agent 的差別在哪？什麼時候該用哪個？
4. Agent 內部的 reasoning + acting 迴圈怎麼運作？
5. Agent 怎麼從錯誤中學習（反思）？
6. 目前 Agent 有哪些已知限制？

---

## Wiki 頁面（知識節點）

| 編號 | 頁面 | 核心貢獻 | 對應問題 |
|------|------|----------|----------|
| 01 | [[01-anthropic-building-effective-agents]] | Workflow vs Agent 的架構區分、augmented LLM、5 種工作流模式 | Q1, Q3, Q4 |
| 02 | [[02-lilian-weng-llm-agents]] | Agent = LLM + Planning + Memory + Tool use 的經典架構 | Q2 |
| 03 | [[03-react]] | Reasoning 與 Acting 交錯進行的 ReAct 典範 | Q4 |
| 04 | [[04-reflexion]] | 用「語言回饋」讓 Agent 自我反思、從失敗中學習 | Q5 |
| 05 | [[05-survey-llm-agents]] | 把 Agent 統整為 construction / application / evaluation 三面向 | Q2, Q6 |

---

## Wiki 條目 → 簡報頁碼對照（知識來源如何被使用）

| Wiki 頁面 | 對應簡報頁碼 | 用在簡報的哪裡 |
|-----------|--------------|----------------|
| [[01-anthropic-building-effective-agents]] | P4、P8、P11、P12 | Agent 定義與金句(P4)、工具 ACI(P8)、Workflow vs Agent＋5 種模式(P11)、限制：會累積錯誤(P12) |
| [[02-lilian-weng-llm-agents]] | P5、P6、P7、P8、P12 | 架構＝LLM＋三元件(P5)、Planning(P6)、Memory(P7)、Tool use(P8)、限制(P12) |
| [[03-react]] | P9 | ReAct 迴圈 Thought→Action→Observation 與實證數字 |
| [[04-reflexion]] | P10 | 自我反思、從失敗學習、與 ReAct 的差別 |
| [[05-survey-llm-agents]] | P12、P14 | 限制／evaluation(P12)、來源地圖(P14) |

（簡報頁碼對應已發布版本的 14 頁；P2「生活比喻」、P3「動機」、P13「總結」為本 Wiki 統一定義的衍生教學內容。）

---

## 跨頁整合：這個 Wiki 得到的統一定義

把 5 篇來源交叉比對後，本 Wiki 採用的工作定義：

> **AI Agent** 是以 LLM 作為「大腦」的系統，能在一個會回饋結果的環境中，
> 透過**規劃（Planning）**、**記憶（Memory）**與**工具（Tool use）**，
> 以「推理 → 行動 → 觀察」的**迴圈**自主地朝目標推進，
> 並能依據環境回饋**調整下一步、從錯誤中修正**。

- 「以 LLM 為大腦 + 三元件」來自 [[02-lilian-weng-llm-agents]]
- 「迴圈、環境回饋、自主性」來自 [[01-anthropic-building-effective-agents]] 與 [[03-react]]
- 「從失敗修正」來自 [[04-reflexion]]
- 「構成/應用/評估的整體視角」來自 [[05-survey-llm-agents]]

---

## 名詞對照表（中英）

| 英文 | 中文 | 一句話 |
|------|------|--------|
| Agentic system | 代理式系統 | 泛指所有「LLM + 工具」會動作的系統（含 workflow 與 agent） |
| Workflow | 工作流 | LLM 與工具照**預先寫死的程式路徑**被編排 |
| Agent | 代理人 | LLM **自己動態決定**流程與用哪個工具 |
| Augmented LLM | 增強型 LLM | 加上檢索、工具、記憶的 LLM，是一切的基本單元 |
| Planning | 規劃 | 把大任務拆成子目標、並反思修正 |
| Memory | 記憶 | 短期（context window）＋長期（外部向量庫） |
| Tool use | 工具使用 | 呼叫外部 API／程式取得模型本身沒有的能力 |
| ReAct | 推理＋行動 | Thought → Action → Observation 交錯 |
| Reflexion | 反思 | 把失敗寫成文字回饋、下次改進 |
