# OpenSpec: Shrimp-ClawHub (蝦家班技能中樞) 規格書

## 1. 願景與背景 (Vision & Context)
解決蝦家班/蝦工坊在跨環境 (VM/Firebase) 運作時，技能 (Skills) 散亂、版本混亂、且缺乏語意連結的問題。打破「開發後遺忘、踩坑才想起」的惡性循環。

## 2. 核心目標 (Objectives)
- **語意化索引**：將所有 `SKILL.md` 深度整合進 Vertex AI Search。
- **環境透明化**：實現「一套 Skill，全域調用」，無論在大腦 (VM) 還是雙手 (Firebase)。
- **版本確定性**：建立主版本機制，消除重複與過時路徑。

## 3. 三層架構設計 (System Architecture)
...
### 3.6 具象連結與雪球層 (Linkage & Snowballing)
- **實例綁定機制 (Instance Binding)**：每個 Skill 可關聯多個「具象執行案例 (Case Studies)」，提供 Agent 實戰參數參考。
- **自動反哺迴路 (Feedback Loop)**：實作「成功案例自動提取」，將每次成功解決痛點的對話精華轉化為該 Skill 的「附加知識組」。
- **雪球效應監控**：統計 Skill 的「經驗累積量」，作為衡量蝦家班技術資產價值 (Equity) 的核心指標。

## 4. 交付 Opus 的關鍵工單 (Tasks for Opus)
...
8. **開發 `shrimp-link-builder`**：自動掃描 `memory/` 檔案，利用 Vertex AI 提取並建立「記憶-技能」的雙向連結。

## 5. 驗收標準 (Definition of Done)
- [ ] Agent 能透過指令 `shrimp-search "處理 PDF"` 精準定位到 `nano-pdf` 並顯示其路徑。
- [ ] 執行 `shrimp-sync` 後，VM 與 Firebase 的技能目錄完全一致。
