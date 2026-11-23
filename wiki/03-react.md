# 03 · ReAct：Synergizing Reasoning and Acting

**來源**：Yao et al., "ReAct: Synergizing Reasoning and Acting in Language Models"（ICLR 2023；arXiv:2210.03629）
**連結**：https://arxiv.org/abs/2210.03629
**類型**：學術論文（典範方法）
**ingest 日期**：2026-11-23

---

## 一句話摘要
讓 LLM **交錯地**產生「推理軌跡（reasoning traces）」與「行動（actions）」：推理幫助建立/追蹤/更新計畫並處理例外；行動則去跟外部來源（知識庫、環境）互動取得新資訊。這就是今天多數 Agent 迴圈的雛形。

## 關鍵概念

### 核心迴圈：Thought → Action → Observation
```
Thought  : 我需要先查 A 的資料
Action   : Search["A"]
Observation: （環境回傳的結果）
Thought  : 根據結果，接下來要…
Action   : …
（重複，直到得出答案 / 觸發停止條件）
```
形式上：把 agent 的動作空間擴充為 Â = A ∪ L，其中 L 是「語言空間」（也就是「想法」本身也算一種動作）。

### 為什麼有效
- **Reasoning only（如 CoT）**：只在腦內推理，無法取得外部新知 → 容易幻覺、錯誤會沿著鏈傳播。
- **Act only**：只會動作，缺乏高層規劃與工作記憶。
- **ReAct＝Reason + Act**：兩者互補，能動態建立並調整計畫，同時用外部資訊校正。

### 實驗結果（可當佐證數字）
- 在問答（HotpotQA）與事實查核（Fever）：透過跟簡單的 Wikipedia API 互動，**減少幻覺與錯誤傳播**。
- 在互動決策 benchmark（ALFWorld、WebShop）：成功率分別**比模仿學習／強化學習基線提高 34、10 個百分點**（原文為 absolute success rate），而且只用 1–2 個 in-context 範例。
- 額外好處：軌跡**更可解釋、更可信**（人看得懂它為何這樣做）。

## 與其他頁的連結
- 是 [[02-lilian-weng-llm-agents]] 中 self-reflection／planning 的具體實作。
- 是 [[01-anthropic-building-effective-agents]] 所說「LLM 根據環境回饋在迴圈中用工具」的學術原型。
- [[04-reflexion]] 以 ReAct 作為可選的 Actor，再加上跨回合的反思。

## 可直接拿去教學的重點
ReAct 讓「想」和「做」綁在一起 → Agent 不再只是一次問答，而是**會查資料、會修正**的循環過程。
