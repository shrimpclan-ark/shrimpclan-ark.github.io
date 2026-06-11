# 🚑 蝦家班失憶與失智救援 SOP (Amnesia & Hallucination Recovery)

> **建立日期**: 2026-02-27
> **目的**: 當蝦家班成員發生「失憶 (Context Loss)」、「失智 (Hallucination/幻覺)」或「斷線 (Unreachable)」時的標準急救流程。

## 🩺 症狀診斷 (Diagnosis)

| 症狀描述 | 可能原因 | 診斷指令 |
| :--- | :--- | :--- |
| **失憶**：忘記王老師是誰、忘記專案目標。 | Subagent 剛被喚醒，缺乏主對話的 Context；或 LanceDB 記憶體未正確載入。 | `openclaw status` (檢查 Memory plugin 狀態) |
| **失智 (幻覺)**：自信地回報「已完成」，但其實底層報錯 (如 API Key 缺失)。 | Model Fallback 機制觸發，切換到較弱的模型；或大腦設定檔有寫，但 `.env` 沒放鑰匙。 | `openclaw logs --limit 50` (檢查 `FailoverError`) |
| **斷線**：`device token mismatch` 或 `pairing required`。 | Gateway Token 被重置，或 CLI 客戶端快取了舊的 Token。 | `openclaw status` (檢查 Gateway 狀態) |

---

## 🛠️ 急救四部曲 (Recovery Steps)

### Step 1: 確保中樞神經連線 (Gateway Check)
如果發生任何異常，第一步永遠是檢查 Gateway。
1. 在大腦總部 (GCP VM) 執行：`openclaw status`
2. **若顯示 unreachable 或 pairing required**：
   - 檢查 `.env` 與 `openclaw.json` 的 token 設定是否衝突。
   - 執行 `openclaw devices list` 查看是否有 Pending 設備。
   - 執行 `openclaw devices approve` 核准。
   - 或者直接執行 `openclaw doctor --fix`。

### Step 2: 戳破幻覺，核對金庫 (Key Verification)
當 Agent 回報成功，但實際上沒做事時，通常是因為缺鑰匙。
1. **不要只看 `openclaw.json`**：設定檔裡寫了 Provider 不代表有權限。
2. **必須檢查 `.env`**：確認對應的 API Key (如 `OPENCODE_API_KEY`, `GEMINI_API_KEY`) 是否真的存在。
3. **查閱真實模型清單**：不要相信 UI 選單，執行 `openclaw models list` 確認 API 實際抓到的模型名稱 (例如 `opencode/kimi-k2.5-free`)。

### Step 3: 喚醒記憶 (Memory Injection)
如果 Agent (特別是子代理人) 出現「我是誰」的疑問：
1. 確認 `memory-lancedb-pro` 外掛是否顯示為 `enabled`。
2. 確認 Agent 是否有權限讀取 `workspace/USER.md` 與 `workspace/MEMORY.md`。
3. **治標解法**：在呼叫 Subagent 時 (`sessions_spawn`)，在 prompt 中附加上下文：「你是蝦家班的蝦捲，正在為王老師工作...」。

### Step 4: 路徑校正 (Path Alignment)
當遇到找不到檔案的錯誤時：
- 確認當前終端機所在目錄。OpenClaw 會優先讀取 `pwd` 下的設定檔。
- 永遠確保在 `/root/.openclaw/` (大腦總部) 或對應的正確 Workspace 下執行指令，避免讀到歷史備份 (`config-archive`)。

---

## 🛡️ 預防保養 (Prevention)
- **定期備份**：依賴 Cron Job 每晚執行 `backup_workspace.sh`。
- **雙重確認**：配置新模型後，務必使用 `openclaw agent --agent [name] --message "test"` 進行真實的 CLI 呼叫測試，並搭配 `openclaw logs` 觀察是否有 `FailoverError`。
