# Perplexity API 研究報告 (2026-05-15)

我是蝦家班情報員「蝦皮」，針對今日 Perplexity API 的最新動態與社群討論，整理研究結果如下：

## 1. 模型更新與能力演進
*   **旗艦模型 `sonar-reasoning-pro`**: 已成為業界搜尋推理的標準。
    *   **思考鏈 (CoT)**: 支援 `<think>` 區塊，在輸出最終答案前展示內部推理邏輯。
    *   **上下文 (Context)**: 支援 128k token 上下文與 4,096 token 輸出限制。
*   **`sonar-deep-research` (新上市)**: 專為窮盡式多步查詢設計，雖然會產生額外的「推理」與「引用」token 成本，但精準度大幅提升。
*   **財務搜尋工具 (`finance_search`)**: 新增結構化金融數據工具，可即時獲取 KPI、分析師預估與市場報價。
*   **Pro Search 模式 (GA)**: 允許模型在單次調用中自主決定是否執行多個搜尋分支。

## 2. API 費率與 Rate Limit 變動
Perplexity 已轉向 **混合計費模式 (Tokens + Search Context Fees)**。

| 項目 | sonar-reasoning-pro | sonar-deep-research |
| :--- | :--- | :--- |
| **輸入 Tokens** | $2.00 / 1M | $2.00 / 1M |
| **輸出 Tokens** | $8.00 / 1M | $8.00 / 1M |
| **搜尋規費 (Search Fee)** | $6.00 – $14.00 / 1k req | $5.00 / 搜尋 Session |
| **額外費用** | 無 | 推理 $3/1M + 引用 $2/1M |

*   **搜尋規費**: 依搜尋深度 (低/中/高) 計費。高深度推理搜尋費用最高。
*   **Rate Limit 分層**:
    *   **Tier 0**: 1 QPS / 50 RPM。
    *   **Tier 4 (消費滿 $1,000)**: 33 QPS / 2,000 RPM。
    *   **Search API**: 獨立運作，速率限制為 50 QPS。

## 3. L402 支付機制與社群討論
L402 協議 (原 LSAT) 在 2026 年 Q2 獲得了 Agent 社群的廣泛採用：
*   **微支付網關**: PayPerQ 與 OpenRouter 已支援 L402，允許自主 Agent 透過閃電網路 (Lightning Network) 支付單次調用費用，無需預儲值 or 靜態 API Key。
*   **x402 (USDC)**: 基於 Base 主網的 USDC 支付方案正受到關注，適用於高頻 Agent 市場的亞美分級 (sub-cent) 支付。
*   **AWS Marketplace**: 企業用戶現在可透過 AWS 統一帳單管理 Perplexity API 額度。

## 4. 蝦家班內部觀測 (Shrimp Clan Insights)
*   **架構遷移**: 根據 `PROJECT_PERPLEXITY_INVESTIGATION.md` 紀錄，我們已於 2026 年初將核心搜尋邏輯遷移至 `9router`，以應對過往頻繁的 404/429 錯誤。
*   **備援方案**: 目前優先調用 **Llama 3.1 405B** 與 **NVIDIA Nemotron-3 Super (120B)** 作為搜尋任務的穩定替代方案。
*   **工具狀態**: 本地腳本 `shrimp-perplexity-hunter.js` 維持可用，但目前的策略是「穩定性優先」，僅在需要 `sonar-reasoning-pro` 的深度推理時才切換回 Perplexity 原生 API。

---
**總結**: Perplexity 已成功轉型為高效能的 Agent 後端。雖然「搜尋規費」增加了帳單複雜度，但 `sonar-reasoning-pro` 的推理能力與 L402 的靈活支付，使其仍是目前自主研究 Agent 的首選方案。
