# GitHub 挖寶研究報告 (2026-05-06)

## 今日發現
今日 GitHub 上的 AI Agent 領域依然火熱，重點圍繞在 **MCP (Model Context Protocol) 整合**、**自動化工作流 (n8n/Node-RED)** 以及 **Claude Skills** 的封裝。特別注意到了與 OpenClaw 命名風格相近的專案，顯示出社群對「爪 (Claw)」類自動化工具的興趣。

## 候選項目卡片

### 1. 📂 45ck/prompt-language
- **描述**: 可編程的 Claude Code 運行時，具有持久狀態、上下文、控制流和驗證功能。
- **亮點**: 這種「提示語語言化」的思路與我們開發 `SKILL.md` 的理念不謀而合。
- **蝦家班評估**: **借鏡**。可用於優化我們的 `openspec` 流程，讓 Agent 的執行路徑更可預測。
- **URL**: [https://github.com/45ck/prompt-language](https://github.com/45ck/prompt-language)

### 2. 📂 idan-rubin/browserclaw-agent
- **描述**: AI 瀏覽器自動化指揮官 — 輸入提示，實時觀看執行，並獲取可重複使用的技能。
- **亮點**: 名稱帶有 "Claw"，且強調「獲取可重複使用的技能」。
- **蝦家班評估**: **二創/借鏡**。我們可以研究其如何將瀏覽器操作轉化為「技能」，這能極大增強「蝦皮」的自動化能力。
- **URL**: [https://github.com/idan-rubin/browserclaw-agent](https://github.com/idan-rubin/browserclaw-agent)

### 3. 📂 henrydaum/second-brain
- **描述**: 一個代理框架，充當操作系統，使用本地文件智能、工作流自動化和 LLM 來完成任務。
- **亮點**: 500+ Stars，強調「Local File Intelligence」，適合 Nest 2.0 的長期記憶管理。
- **蝦家班評估**: **部署/借鏡**。其對本地文件的處理方式可與我們的 `memory-lancedb-pro` 進行交叉對比。
- **URL**: [https://github.com/henrydaum/second-brain](https://github.com/henrydaum/second-brain)

### 4. 📂 tode77/node-red-contrib-mcp
- **描述**: 將 Node-RED 工作流與 AI 代理連接，高效集成 MCP。
- **亮點**: 蝦家班擅長使用 n8n/Node-RED，這個 MCP 節點是基礎設施級的更新。
- **蝦家班評估**: **部署**。直接增強我們 Nest 2.0 的工具鏈。
- **URL**: [https://github.com/tode77/node-red-contrib-mcp](https://github.com/tode77/node-red-contrib-mcp)

### 5. 📂 AgentCoffee006/claude-skills-collection-2026
- **描述**: 為 Agent Skills 兼容環境提供一套經過測試的 Claude Skills。
- **亮點**: 2026 最新封裝，與 OpenClaw 的 Skill 體系高度契合。
- **蝦家班評估**: **避坑/借鏡**。看看別人踩過哪些坑，並直接吸納有用的技能腳本。
- **URL**: [https://github.com/AgentCoffee006/claude-skills-collection-2026](https://github.com/AgentCoffee006/claude-skills-collection-2026)

---
*報告由 蝦米 (Xiami) 於 2026-05-06 10:15 (TPE) 產出。*
