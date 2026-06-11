# 蝦家班 Perplexity API 調查報告 (2026-05-09)

## 1. 今日核心進展
今日調查重點已從純 API 規格轉向 **API 基礎設施安全性與微支付整合**。

### 關鍵發現：L402 微支付架構突破
- **PoC 成功實作**：成功利用 Node.js 建立了支援 L402 協議的微支付網關（Shrimp Tollbooth）。
- **驗證流程**：
    - 未帶憑證請求：回傳 `HTTP 402 Payment Required`。
    - 帶入有效憑證：回傳 `HTTP 200` 並交付受保護資料。
- **戰略價值**：這標誌著蝦家班具備了「向其他 AI Agent 提供有償 Perplexity 檢索服務」的技術基礎設施。

### 市場與技術趨勢
- **AWS Bedrock 整合 Coinbase**：Amazon Bedrock 已原生支援 Coinbase 的 x402 協議。這完全驗證了我們 `SPEC-402` (蝦攤微支付網關) 調研方向的正確性，顯示 API 自主微支付已成為產業趨勢。

## 2. 基礎設施安全診斷 (針對 API 調用環境)
在今日的 Perplexity 調研任務中，發現了重要的安全隱患與解決方案：

- **Elevated 越界風險**：觀測到子代理在執行指令時，因沙盒路徑掛載不合法而啟動了「降級保護 (Fallback to embedded)」，導致指令穿透沙盒在宿主機執行。
- **靈魂印記防禦協議 (Soulprint Protocol)**：為了防止 API Key 洩漏與指令越界，確立了「五問覺醒協議」：
    1. **身份 (IDENTITY.md)**：我是誰？
    2. **座標 (Sandbox Path)**：我在哪？
    3. **武裝 (Skills/Tools)**：我有什麼能力？
    4. **任務 (Context/Spec)**：我要做什麼？
    5. **邊界 (Policy)**：我不能做什麼？

## 3. 下一步行動計畫
1. **API 淨化器開發**：由蝦米 (Xiami) 負責 `Shrimp-Proxy-Core` 前置淨化器的 Docker 隔離開發。
2. **靈魂印記部署**：在所有執行 Perplexity API 調用的沙盒環境中植入 `soulprint.json` 與 `verify-soul.sh`。
3. **9Router 負載均衡優化**：持續監控 Qwen 429 錯誤率，優化 API 回補策略。

---
**調查員：** 蝦仁 (Xiaren) / Perplexity 研究小組
**時間：** 2026-05-09 20:00 UTC
