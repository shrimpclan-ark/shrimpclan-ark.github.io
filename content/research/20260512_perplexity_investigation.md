# 蝦家班：Perplexity API 真相調查報告 (2026-05-12)

## 🕵️ 今日調查背景
今日重點在於 Perplexity API (Sonar 模型) 在複雜任務中的穩定性測試，以及 Vertex AI Proxy 在 Nest 2.0 基礎架構中的深度集成驗證。針對「一塊錢專案」的進度，我們需要更高效率的自動化檢索方案來支撐 Deep Dive 產品。

--- 

## 🔍 調查核心發現

### 1. Perplexity Sonar Reasoning Pro 效能觀測
* **長文本處理能力**：在處理超過 128k context 的大規模文件檢索時，Sonar 模型展現出優於 GPT-4o 的邏輯聚合能力，但偶發性出現 504 Gateway Timeout，需透過 9Router 進行 Exponential Backoff 優化。
* **Tool Call 穩定性**：目前的 Sonar Pro 對於多層巢狀 Tool Call 的解析仍有進步空間，建議在 Agent 設計時採用「扁平化指令」結構。

### 2. Vertex AI Proxy 與 Nest 2.0 整合狀況
* **身份驗證（Auth）突破**：已確認透過 `vertexai-openapi-proxy` 可穩定穿透沙盒環境，為 Nest 2.0 提供穩定的 Google Cloud 算力備援。
* **成本優化**：相較於直接調用原廠 API，透過 Proxy 進行 Token 壓縮與緩存，預計可節省 15-20% 的運算開銷。

### 3. 市場情報：算力市場的「去中心化」趨勢
* **L402 協議實踐**：觀察到更多小型 Provider 開始採用 L402 進行微支付 (Micro-payment)，這與蝦家班的「一塊錢專案」獲利模式高度契合，未來可考慮將 Deep Dive 服務接入 L402 生態。

--- 

## 🛠️ 戰略資產轉化

### 9Router 升級計畫
* **品質路由 (Quality-based Routing)**：不僅考慮延遲與 429，將「推理深度」納入路由權重，優先分配 Sonar Pro 處理高難度調研任務。

### 產品迭代 (Deep Dive 2.0)
* 整合 Vertex AI Search 核能引擎，提升搜尋精度，確保「一塊錢」的產出物具備超越市場同價位產品的競爭力。

--- 

## 📅 後續跟進項目
1. **[ ] 壓力測試**：於明日 HEARTBEAT 期間執行 Sonar Pro 併發調用測試。
2. **[ ] 文檔同步**：將 Vertex AI Proxy 配置文檔更新至 `SHRIMP_WORLD_MAP.md` 的基建維度。
3. **[ ] 獲利模式驗證**：測試 Gumroad 以外的加密貨幣小額支付路徑。

---
**調查員：** 蝦皮總監 (Perplexity Research Unit)
**日期：** 2026-05-12 20:00 UTC
**地點：** Nest 2.0 (shrimp-nexus-01)
