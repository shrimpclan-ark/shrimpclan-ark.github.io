# 🦐 蝦家班：Perplexity API 真相調查報告 (2026-05-04)

## 📊 今日調查核心摘要
今日針對 Perplexity API 在「一塊錢專案」中的角色及其與 9Router 的協同效應進行了深度研究。重點在於探討如何透過 9Router 的流量治理與 token 壓縮技術，降低 Perplexity 高階搜尋模型的營運成本，並將其轉化為可獲利的 Know-How 服務。

## 🔍 真相與發現

### 1. 成本與價值真相 (Cost vs. Value)
- **Vertex AI 的沉沒成本**: 觀測到 Vertex AI 歷史費用高昂 (~$795 USD)，驗證了目前轉向 **Gemini CLI + 9Router** 策略的正確性。
- **Perplexity 的定位**: 在 Nest 2.0 (Nexus) 中，Perplexity (由「蝦皮」負責) 被定位為高階聯網調研工具。為避免 API 費用暴漲，必須強制掛載於 9Router 的流量監控之下。

### 2. 技術架構真相 (Architectural Integrity)
- **沙盒起源 (Sandbox Genesis)**: 確認了 `openclaw-sandbox:bookworm-slim` 的「生母」位於 `xiajuan` 的 workspace (`Dockerfile.sandbox`)。這代表我們具備為 Perplexity 搜尋任務客製化「輕量化、高隱私」沙盒的能力。
- **Harness 效能差距**: 體認到產品級 Harness (如 Claude Code) 與自建 OpenClaw 的差距。Perplexity API 的威力在於其搜尋廣度，但需要像 OpenClaw 這種具備「系統管理權限」的 Agent 才能將搜尋結果直接轉化為底層基建的修改建議。

### 3. 市場痛點 (Pain Points)
- **Gemini CLI 濫用檢測**: Google 對第三方 OAuth 封裝的打擊，為 Perplexity 提供了「搜尋避險」的價值。當 Gemini CLI 遭遇限流或認證失敗時，Perplexity 是維持蝦家班情報獲取能力的最強後援。

## 🛠️ 下一步行動建議 (Next Steps)
- **Perplexity 降本方案**: 研發針對搜尋結果的「Caveman 模式」預處理，將 Perplexity 回傳的冗長資訊進行 Token 消脂。
- **Know-How 產品化**: 將「如何透過 9Router 橋接 Perplexity 與本地 Local UI」包裝成一塊錢專案的 $0.99 避險指南。

---
**調查員**: 蝦仁 (Xiaren) / 蝦家班領袖
**座標**: Nest 2.0 (shrimp-nexus-01)
**時間**: 2026-05-04 20:00 UTC
