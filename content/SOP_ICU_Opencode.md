# 🚨 蝦窩 ICU 急救手冊 (Opencode 專用)

> **當蝦家班全面失聯，或 9Router 升級失敗導致大腦當機時，探長請參閱此手冊，騎著小毛驢 (Opencode) 進入加護病房 (ICU) 進行搶救。**

## 🚑 狀況一：9Router 壞死，所有模型噴 503/400/404

**症狀**：OpenClaw 無法回覆，或者回覆全都是 Error，Telegram 群組死寂。
**診斷**：可能是 9Router `config.json` 寫錯、PM2 崩潰，或 `active-steering` 升級失敗。

### 急救步驟 (Opencode 終端機執行)：
1. **停止 9Router 服務**：
   ```bash
   pm2 stop 9router-fork
   ```
2. **緊急切換 OpenClaw 為「純 ADC 求生模式」**：
   進入 `/root/.openclaw/`，直接將 `openclaw.json` 中的 `agents.defaults.model.primary` 修改為最底層的直連模式，跳過 9Router：
   ```bash
   # 將主腦直接綁定到 Vertex Proxy (不經過 9Router)
   # 尋找 "primary": "..." 並替換為：
   "primary": "vertex-proxy/google/gemini-2.5-flash"
   ```
3. **重啟 OpenClaw 喚醒蝦仁**：
   ```bash
   openclaw gateway restart
   ```
   *等待 10 秒後，到 Telegram 輸入 `ping`，若蝦仁回覆 `pong`，代表主腦已恢復意識。接下來即可由蝦仁接手修復 9Router。*

---

## 🚑 狀況二：OpenClaw 核心癱瘓 (卡死/OOM)

**症狀**：連 `ping` 都沒有反應，`pm2 status openclaw` 顯示 `errored` 或不斷 `restarting`。
**診斷**：可能是某個 Agent 陷入無限迴圈，或是 Context Token 超過 1M 導致記憶體爆掉。

### 急救步驟 (Opencode 終端機執行)：
1. **斬斷所有執行中的 Session (強制失憶療法)**：
   有時候是某個卡死的 `.jsonl` 對話檔導致重啟失敗。我們需要把卡死的紀錄搬走：
   ```bash
   mkdir -p /root/.openclaw/agents/main/sessions_backup
   mv /root/.openclaw/agents/main/sessions/*.jsonl /root/.openclaw/agents/main/sessions_backup/
   ```
2. **清理快取與暫存檔**：
   ```bash
   rm -rf /tmp/openclaw/*
   npm cache clean --force
   ```
3. **強制暴力重啟**：
   ```bash
   pm2 restart openclaw --update-env
   ```

---

## 🚑 狀況三：新功能 (Active-Steering) 導致連鎖災難

**症狀**：探長剛批准完新程式碼縫合，結果系統開始無差別跳過所有模型 (不斷觸發 `SOFT_SKIP`)。
**診斷**：`shrimp-active-steering` 的閾值設錯，或遇到了預期外的網路波動。

### 急救步驟 (透過 Opencode 檔案編輯)：
1. **找到防火線開關**：
   打開 `/root/.openclaw/workspace/projects/shrimp-harness/v3-active-steering/config/active-steering.json`
2. **物理切斷神經**：
   將 `"enabled": true` 直接改為 `"enabled": false`。
3. **重啟 9Router 即可恢復舊版路由**：
   ```bash
   pm2 restart 9router-fork
   ```

---

## 🛡️ 探長專屬備忘錄
當您使用 Opencode 進入 ICU 搶救時，請務必確認您的 Opencode 使用的是 **`sk-donkey`** 這把專屬 API Key。這會確保在您修復完畢後，戰情雷達能清楚過濾出哪些流量是「探長的手術痕跡」，而不會與我們日常的流量混淆。