# GitHub 每日挖寶任務報告 (2026-05-02)

## 今日發現
今日搜尋重點在於 AI Agent 的編排架構、OpenClaw 相關技能以及 Claude Code 的源碼分析。發現多個與「多代理協作 (Multi-agent orchestration)」以及「技能標準化 (Skill standardization)」相關的專案，非常適合蝦家班目前的「一塊錢專案」與「技能系統」參考。

## 候選項目卡片

### 1. [debug-swat-skill](https://github.com/Dustyevil282/debug-swat-skill)
- **描述**: Coordinate multi-agent debugging for front-end, back-end, database, network, and system issues on WorkBuddy and OpenClaw.
- **評估**: **必看！** 這是直接針對 OpenClaw 開發的調試技能。蝦家班可以借鏡其多維度（前端、後端、網路）的協作邏輯，強化我們的 `qa-testing` 或開發流程。
- **動作**: 建議由蝦米 (Xiami) 深入研究其對 OpenClaw 的整合方式。

### 2. [agentskills-mcp](https://github.com/Drhir2460/agentskills-mcp)
- **描述**: Search, read, and download curated agent skills via MCP for fast discovery and local use in agent workflows.
- **評估**: **二創潛力高**。透過 MCP 協議來發現與下載技能，符合蝦家班「萬物皆可是技能」的精神。可以考慮將其整合進我們的 `mcporter` 工具。
- **動作**: 評估是否能將蝦家班的 `SKILL.md` 庫透過此類 MCP server 進行分發。

### 3. [claude-code-source](https://github.com/Demetrastarkers93/claude-code-source)
- **描述**: Inspect recovered Claude Code source and study its terminal coding, codebase analysis, and git workflow automation logic.
- **評估**: **技術借鏡**。Claude Code 是目前最強的 Coding Agent 之一，分析其源碼有助於優化蝦米的 `coding-agent` 執行邏輯，特別是 terminal 交互與 git 自動化部分。
- **動作**: 蝦米應將其納入參考資料。

### 4. [open-multi-agent](https://github.com/jerseyknapweedaar793/open-multi-agent)
- **描述**: Orchestrate TypeScript multi-agent teams with one runTeam() call, zero config, and three runtime dependencies.
- **評估**: **架構參考**。追求極簡的 TypeScript 多代理框架。與我們的 `clawteam` 理念相似，可對比其執行效率與複雜任務的拆解能力。
- **動作**: 觀察其 `runTeam()` 的實現機制。

---
*報告產生時間: 2026-05-02 02:22 UTC*
*產生者: 蝦米 (Xiami)*
