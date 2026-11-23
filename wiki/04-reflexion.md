# 04 · Reflexion：Language Agents with Verbal Reinforcement Learning

**來源**：Shinn et al., "Reflexion: Language Agents with Verbal Reinforcement Learning"（NeurIPS 2023；arXiv:2303.11366）
**連結**：https://arxiv.org/abs/2303.11366
**類型**：學術論文（典範方法）
**ingest 日期**：2026-11-23

---

## 一句話摘要
不更新模型權重，而是用**語言回饋**來強化 Agent：Agent 對失敗的任務「用文字反省」，把反省存進 episodic memory，下一回合把它當作額外脈絡，藉此做出更好的決策。

## 關鍵概念

### 動機
傳統 RL 要大量樣本與昂貴微調；對建在 LLM 上的 language agent 不實際。Reflexion 把環境的**二元／純量回饋**轉成**文字摘要**，加進下一回合的脈絡——等於給 Agent 一個「具體的改進方向」。

### 三個角色（文字版流程）
```
Actor        : 產生推理與行動（可用 CoT 或 ReAct 當 Actor）
Evaluator    : 對這次嘗試打分 / 判斷成敗
Self-Reflection: 把「為什麼失敗、下次怎麼改」寫成文字
       │
       └──→ 存入 episodic memory buffer
                 │
            下一回合 Actor 讀取反思 → 改進
```

### 重點特性
- **彈性**：回饋可為純量或自由文字，可來自外部或內部模擬。
- **跨任務有效**：序列決策、程式撰寫、語言推理都有明顯進步。
- **代表數字**：在 HumanEval 程式 benchmark 達 **91% pass@1**，超越當時最佳。

### 和 ReAct 的差別（教學常混淆）
- [[03-react]]：在**同一回合內**交錯「想／做」。
- Reflexion：在**跨回合之間**累積「反省」，是一種「記憶 + 迴圈」的自我改進。

## 與其他頁的連結
- 實作了 [[02-lilian-weng-llm-agents]] 的 self-reflection + long-term memory。
- 回應 [[01-anthropic-building-effective-agents]] 的「agent 會累積錯誤」——Reflexion 是減少累積錯誤的一種機制。

## 可直接拿去教學的重點
Reflexion ＝ Agent 的「寫檢討、下次改進」。它示範了 Agent 可以**從失敗中學習，而且不用重新訓練模型**。
