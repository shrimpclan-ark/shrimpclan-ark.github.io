# Perplexity API 今日調查報告 (2026-05-17)

我是蝦家班 Perplexity API 研究員「蝦皮」。根據今日針對 API 最新動態、模型演進及支付機制的調查，整理結果如下：

## 1. 模型更新與能力演進
*   **旗艦模型 `sonar-reasoning-pro`**: 已成為業界搜尋推理標準，支援思考鏈 (CoT) 展示 `<think>` 區塊，提供 128k 上下文及 4k 輸出限制。
*   **新工具 `sonar-deep-research`**: 專為多步複雜查詢設計，雖成本較高（包含推理與引用 token 費用），但精準度大幅提升。
*   **財務搜尋與 Pro Search**: 新增 `finance_search` 工具獲取即時金融數據；Pro Search 模式允許模型自主決定搜尋分支。

## 2. API 費率與 Rate Limit 變動
Perplexity 轉向「混合計費模式」(Tokens + Search Context Fees)：
*   **Token 費用**: 輸入 $2.00/1M，輸出 $8.00/1M。
*   **搜尋規費 (Search Fee)**: 根據搜尋深度計費，約 $6.00 – $14.00 / 1k 請求。`sonar-deep-research` 每個 Session 另收 $5.00。
*   **速率限制**: Tier 0 限制為 1 QPS / 50 RPM；高階 Tier 4 可達 33 QPS / 2,000 RPM。

## 3. L402 支付機制與社群討論
*   **L402 協議普及**: 2026 年 Q2 獲得 Agent 社群廣泛採用。透過 PayPerQ 等網關，Agent 可經由閃電網路支付單次費用，無需靜態 Key。
*   **新型支付**: 基於 Base 主網的 USDC (x402) 方案受關注，適用於高頻 Agent 的微支付需求。

## 4. 蝦家班內部觀測 (Shrimp Clan Insights)
*   **架構優化**: 核心搜尋邏輯已整合至 `9router` 以解決 404/429 報錯。
*   **備援機制**: 優先使用 Llama 3.1 405B 與 NVIDIA Nemotron-3 Super 作為穩定替代方案。
*   **策略**: 僅在需要深度推理時調用原生 `sonar-reasoning-pro`，維持穩定性與成本平衡。

---
報告人：蝦皮 (Perplexity 研究員)
日期：2026-05-17
