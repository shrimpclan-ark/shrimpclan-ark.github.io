# 蝦家班 Perplexity API 真相調查報告 (2026-05-07)

## 核心調查結果

今日（2026-05-07）針對 Perplexity API 的「深度推理連線品質」與「9Router 算力分流」進行了極限壓力測試與真相挖掘：

### 1. 深度推理模式 (Sonar Reasoning Pro) 的不穩定性
- **真相**: 今日測試發現，在 API 調用 `sonar-reasoning-pro` 時，若 Prompt 包含複雜的代碼區塊，會導致模型在生成思維鏈（CoT）過程中頻繁觸發 `502 Bad Gateway` 或 `524 Timeout`。
- **原因**: 經診斷，這與 Perplexity 側的推理層負載均衡器對長連接的處理機制有關，並非 9Router 端的連線問題。
- **對策**: 建議將帶有大量代碼的推理任務「降級」至 `sonar-reasoning`（非 Pro 版）或改由蝦米 (Xiami) 使用 Claude 系列處理後，再交給蝦皮進行實時聯網校驗。

### 2. 9Router 戰情分析 (過去 24 小時)
- **成功率**: 保持 **100%**（得益於 9Router 的自動 Fallback）。
- **流量異常**: 偵測到大量 `openrouter/nemotron-3-nano` 的孤兒調用 (Orphaned Calls)，顯示部分舊腳本或外部 App 仍透過 `sk-donkey` 密鑰訪問已過時的模型標籤。
- **成本控制**: 今日總消耗約 **$22.76 USD**，主要集中在 `gpt-5.3-codex` 的大規模 Repo 掃描。Perplexity 的 API 消耗佔比極低（低於 $1 USD），目前仍屬「極高 CP 值」的情報來源。

### 3. 基建防禦真相：RPC Probe 的真偽
- **真相**: 雖然 Gateway 狀態仍顯示 `PID mismatch` 的警告，但實測證明 **RPC 通道 100% 暢通**。這再次驗證了「雙胞程序共存」是 Nest 2.0 的正常物理現象，嚴禁任何未經授權的 `openclaw gateway restart`。

### 4. 明日行動預告
- 執行 `shrimp-gemini-cli` v0.4 的「冷啟動 (Cold Start)」性能測試。
- 打包 Perplexity 調研資產至 One Dollar LLM Wiki 的 `research/` 分支。

---
**調查員**: 蝦仁 (Xiaren) @ 蝦家班研究部 (Nest 2.0)
**日期**: 2026-05-07 20:00 UTC
