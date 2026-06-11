# 🦐 蝦家班模型管理系統 (SOP_MODEL_MANAGEMENT.md)

## 🎯 管理宗旨
透過「多重分流、動態備援」策略，確保蝦家班在任何 API 波動下仍能保持運作。
- **主力大腦 (High-End)**: 使用 Google Gemini (Pro/Flash) 確保推理能力。
- **技術研究 (Opencode)**: 使用 MinMax, GLM 等免費模型處理非核心任務。
- **情報偵查 (Search)**: 鎖定 Perplexity 系列進行深度檢索。

---

## 🔑 核心金鑰池 (Key Management)

### 1. 主力 API Key (GCP/Google)
- **Status**: ✅ Active (via OAuth)
- **Accounts**: `shrimpclan.ai@gmail.com` (Main Team Leader), `cmwang@nsda.ee.ncku.edu.tw` (Production)
- **Models**: `gemini-3-pro-preview`, `gemini-3-flash-preview`

### 2. 蝦家班一號 (OneAPI - Zeabur)
- **Status**: ✅ Active (sk-hPMcHT9z...50291092)
- **Endpoint**: `https://onepiece6713.zeabur.app/v1`
- **Featured**: `perplexity/sonar-reasoning-pro`, `meta/llama-3.1-405b-instruct`

### 3. OpenCode 專線
- **Status**: ✅ Active
- **Provider**: `opencode`
- **Free Models**: `minimax-m2.5-free`, `glm-5-free`, `trinity-large-preview-free`

### 4. OpenRouter (Fallback Pool)
- **Status**: ✅ Active (sk-or-v1-5275d70...d6bc)
- **Models**: `openrouter/free` (Auto routing)

---

## 🚦 模型准許名單 (Allow-list) & 優先順序 (Priority)

| 成員 | 角色 | 優先模型 (Primary) | 備援模型 (Fallbacks) |
| :--- | :--- | :--- | :--- |
| **🍤 蝦仁** | 總指揮 | `google-gemini-cli/gemini-3-pro-preview` | `oneapi/moonshotai/kimi-k2.5` |
| **🛍️ 蝦皮** | 搜索專員 | `oneapi/perplexity/sonar-reasoning-pro` | `oneapi/meta/llama-3.1-405b-instruct` |
| **🦐 蝦米** | 工程師 | `google-gemini-cli/gemini-3-pro-preview` | `opencode/claude-opus-4-6` |
| **🌯 蝦捲** | 執行者 | `opencode/minimax-m2.5-free` | `opencode/glm-5-free` |
| **🥠 蝦餅** | 測試員 | `opencode/glm-5-free` | `openrouter/free` |

---

## 🛠️ 維護規則
1. **每日心跳檢測**: Heartbeat 時確認 `openclaw logs` 是否有 401/429 錯誤。
2. **失效即移除**: 若模型連續 3 次調用失敗，手動從 `openclaw.json` 的 `agents.defaults.models` 中移除。
3. **安全第一**: 絕不將 `OPENROUTER_API_KEY` 或其他明文 Key 寫入 `SOUL.md` 或公開文档，僅限於 `.env`。
