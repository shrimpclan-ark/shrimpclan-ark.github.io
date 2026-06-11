# 🦞 OpenClaw: Google Cloud Vertex AI (ADC) 整合攻略密技

在 Google Cloud Workstations (Firebase Studio Workspace) 等原生 GCP 環境中，將 OpenClaw 串接至 Vertex AI 是獲得企業級配額（Quota）、穩定性，並避開免費 API Rate Limit 懲罰的最佳路徑。

然而，OpenClaw 對 Vertex AI 的支援邏輯十分「雲端原生」，與傳統的 API Key 填寫方式大不相同。以下是歷經實戰驗證的完整設定指南。

---

## 1. 核心觀念：環境變數優先

官方文件雖提及支援 `google-vertex`，但其底層的 Google SDK 強烈依賴 **環境變數** 與 **Application Default Credentials (ADC)**。

**大坑警告**：
*   ❌ **不要**在 `openclaw.json` 的 `models.providers` 中手動填寫 `google-vertex` 的 `baseUrl`、`projectId` 或 `region`。這會觸發 Zod Schema 嚴格驗證並導致 Gateway 拒絕啟動。
*   ✅ **必須**確保執行 Gateway 的終端機 Session 擁有正確的 GCP 專案與區域變數。

---

## 2. 準備環境變數

在啟動 OpenClaw (Gateway 或 Agent) 之前，請務必匯出以下環境變數。您可以將這些寫入 `~/.bashrc` 或啟動腳本中：

```bash
# 1. 設定 GCP 專案 ID (必須)
export GOOGLE_CLOUD_PROJECT="您的專案ID"  # 例如: braided-visitor-475002-t0

# 2. 設定 Vertex AI 所在的區域 (必須，注意是 LOCATION 而不是 REGION)
export GOOGLE_CLOUD_LOCATION="us-central1"

# 3. 處理 API Key (重要！)
# 如果是在 Google Cloud VM (GCE) 上執行：
# 建議不要設定 GEMINI_API_KEY，SDK 會自動使用 VM 的服務帳戶 (Service Account)。
unset GEMINI_API_KEY

# 如果是在本地開發環境 (Local)：
# 需要透過 gcloud 授權，並提供一個假 key 通過 Schema 檢查。
# export GEMINI_API_KEY=$(gcloud auth application-default print-access-token)
```

> **🔥 穩定性優化 (2026-02-24 更新)**:
> 過去當同時設定了 `GEMINI_API_KEY` 與 GCP 專案資訊時，Gateway 日誌會出現 `The user provided project/location will take precedence over...` 的警告，這會造成 Dashboard 高頻刷新並導致瀏覽器死當。
>
> **現在此問題已解決**：
> 1.  OpenClaw 已在核心日誌系統中自動過濾此 redundant 警告訊息。
> 2.  在 GCE 環境下，請確保 **移除/註解掉** `GEMINI_API_KEY`，這能讓 SDK 直接走服務帳戶路徑，反應速度最快且最穩定。

---

## 3. 身份驗證注意事項 (ADC)

### 在 GCE 虛擬機上：
當執行 `gcloud auth application-default login` 時，如果看到系統提示「You are running on a Google Compute Engine virtual machine...」，請選擇 **`n`**。
*   **原因**：VM 自帶的服務帳戶授權比個人帳戶授權更穩定且不會過期。

### 在本地電腦上：
請執行 `gcloud auth application-default login` 完成瀏覽器授權。

---

## 4. 設定 `openclaw.json` (或 `auth-profiles.json`)

即使我們使用環境變數，OpenClaw 的認證系統仍需要一個「佔位符 (Placeholder)」設定。

### 步驟 A: 修改 `auth-profiles.json`
在 Agent 的專屬目錄中（通常位於 `~/.openclaw/agents/main/agent/auth-profiles.json`），手動加入 `google-vertex:default`：

```json
{
  "profiles": {
    "google-vertex:default": {
      "type": "api_key",
      "provider": "google-vertex",
      "key": "GCLOUD_ADC_PLACEHOLDER" // 僅用於通過 Schema 檢查，不會被實際發送
    }
  }
}
```

### 步驟 B: 修改 `openclaw.json` 的 Default Model
將預設模型切換為 Vertex AI 支援的版本。目前推薦使用 `gemini-2.5-pro`。

```json
{
  "agents": {
    "defaults": {
      "model": {
        "primary": "google-vertex/gemini-2.5-pro",
        "fallbacks": ["openrouter/auto"] // 建議保留一個備用方案
      }
    }
  }
}
```

**注意**：確保 `models.providers` 區段內 **沒有** 關於 `google-vertex` 的手動配置。

---

## 4. 解決 GCP Cloud Workstations 網路連線問題 (1008 Error)

當您嘗試透過 Cloud Workstations 的轉發網址（如 `https://18789-firebase-openclaw-...`）存取 Control UI 或 Canvas 時，容易遇到 WebSocket `1008 (Policy Violation)` 錯誤。
這是因為 GCP 的 Proxy 會改寫 HTTP Origin，導致 OpenClaw 認為是不安全的跨站請求，或是遇到「裝置配對 (Device Pairing)」阻擋。

### 解法：放寬 Gateway 網路限制

修改 `~/.openclaw/openclaw.json` 的 `gateway` 區段：

```json
{
  "gateway": {
    "port": 18789,
    "mode": "local",
    "bind": "lan",  // 允許從 localhost 以外的介面存取
    "controlUi": {
      "allowInsecureAuth": true, // 跳過嚴格的裝置配對要求
      "allowedOrigins": ["*"]    // 允許 GCP 轉發的特殊 URL
    },
    "trustedProxies": ["127.0.0.1"]
  }
}
```

### 重要：清除瀏覽器快取
如果您曾經登入失敗過，瀏覽器的 LocalStorage 裡可能留有舊的無效 Token，這會導致即使設定正確仍持續報錯 1008。

**解法**：按 F12 打開開發者工具 -> Application -> Local Storage -> 清除該網址的所有資料，並重新整理帶有正確 Token 的網址。

---

## 5. 啟動與測試

一切就緒後，請使用以下順序確認系統健康：

1.  **環境診斷** (確保不會報錯)：
    ```bash
    pnpm openclaw doctor
    ```

2.  **清理舊快取** (如果之前一直失敗，可重置 Auth Cooldown)：
    ```bash
    rm -f ~/.openclaw/agents/main/agent/auth-profiles.json
    # (然後重新補上步驟 3 的佔位符)
    ```

3.  **啟動 Gateway**：
    ```bash
    pnpm openclaw gateway --verbose
    ```

4.  **存取 Web UI**：
    開啟 `https://<您的GCP轉發網址>/?token=<您的Gateway_Token>`

現在，您的 OpenClaw 將擁有 Vertex AI 的無限火力與高穩定性！🚀
