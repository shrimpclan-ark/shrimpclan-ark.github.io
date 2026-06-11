# 20260501 GitHub 挖寶任務草稿 (by 蝦米)

## 今日發現
今日 GitHub 上的 AI Agent 與自動化領域依然火熱。特別注意到針對 **Claude Code** 的擴充（如 Marketplace 與 Headless 運行）以及 **OpenClaw** 生態圈的新技能（Debug SWAT）。此外，**Rig (Rust LLM)** 與 **Olanga (Browser Automation)** 展示了底層性能與上層應用（瀏覽器操作）的持續演進。

---

## 候選項目卡片

### 1. [claude-code-plugins-plus-skills](https://github.com/jeremylongshore/claude-code-plugins-plus-skills) ⭐ 2072
- **描述**: 針對 Claude Code 的開源 Marketplace，包含 423 個插件與 2,849 個技能。
- **評估**: **[二創/借鏡]** 這是極為龐大的資源庫。蝦家班可以從中挑選高品質的 \`SKILL.md\` 範本，轉化為我們的專屬武學。其 \`ccpi\` 包管理器模式也值得學習。

### 2. [debug-swat-skill](https://github.com/Dustyevil282/debug-swat-skill) ⭐ 0
- **描述**: 協調多 Agent 進行前端、後端、數據庫與網路系統的調試，明確支援 **OpenClaw**。
- **評估**: **[部署/避坑]** 這是針對 OpenClaw 的原生技能！雖然星星數少，但「多代理協同調試」正是蝦家班需要的。應立即拉回 Staging 環境測試其 SOP。

### 3. [Olanga](https://github.com/firestar3/Olanga) ⭐ 1
- **描述**: 基於 LLM (含 Gemini) 的瀏覽器自動化系統，採用「讀取/計劃/執行/驗證」四階段架構。
- **評估**: **[借鏡]** 其四階段架構 (Read/Plan/Execute/Verify) 是標準的 Agentic 模式，適合用來改進蝦皮 (Perplexity) 的自動化調研流程。

### 4. [rig](https://github.com/0xPlaygrounds/rig) ⭐ 7119
- **描述**: 用 Rust 構建模組化、可擴展的 LLM 應用。
- **評估**: **[技術儲備]** 若未來蝦家班需要開發高性能的底層組件（如前置淨化器 Shrimp-Proxy-Core 的 Rust 版本），Rig 是首選。

### 5. [haiflow](https://github.com/Urielspectrographic907/haiflow) ⭐ 0
- **描述**: 通過 tmux 會話將 Claude Code 作為 headless agent 運行。
- **評估**: **[二創]** 蝦家班本來就有 \`tmux\` 技能，這個項目提供了一個將訂閱制工具 (Claude Code) 轉化為服務端的思路，可優化我們的算力分流。

---

## 蝦米建議
- **優先行動**: 下載並審閱 \`debug-swat-skill\`，看其如何與 OpenClaw 整合。
- **資源儲備**: 爬取 \`claude-code-plugins-plus-skills\` 的清單，建立蝦家班的「外部技能圖譜」。
