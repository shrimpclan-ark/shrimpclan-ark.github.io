# OpenClaw LINE 串接安裝大綱

### 階段一：環境確認（5分鐘）
1. ✅ **確認 OpenClaw 已安裝**
   - 在 GCP Cloud Shell 執行 `openclaw --version`
   - 確認 OpenClaw Gateway 正在運行
2. ✅ **確認網路連線**
   - 檢查 Cloud Shell 是否可以連外網
   - 確認可以執行 curl 命令

### 階段二：安裝 LINE Connector（5分鐘）
3. **下載並安裝 openclaw-line connector**
   ```bash
   curl -fsSL https://moltbot4line.nocory.ai/install.sh | bash
   ```
   - 這會安裝 `openclaw-line` 命令工具
   - 建立與 Cloudflare Tunnel 的連接設定
4. **驗證安裝**
   ```bash
   openclaw-line --version
   ```

### 階段三：連接到 Gateway（5分鐘）
5. **執行連接命令**
   ```bash
   openclaw-line connect
   ```
   - 會自動建立 Cloudflare Tunnel
   - 取得專屬的 webhook URL
   - 顯示連接狀態
6. **記錄連接資訊**
   - 記下顯示的 Tunnel URL
   - 確認 Status 顯示為 "Online"

### 階段四：LINE 官方帳號設定（5分鐘）
7. **加入 LINE 官方帳號**
   - 用手機打開 LINE app
   - 掃描或點擊：https://line.me/ti/p/@572jplep
   - 加入 OpenClaw LINE 官方帳號為好友
8. **註冊你的 OpenClaw 實例**
   - 在 LINE 對話中發送特定指令（可能是 `/register` 或類似）
   - 系統會引導你完成配對流程

### 階段五：測試與驗證（5分鐘）
9. **發送測試訊息**
   - 在 LINE 對話框輸入簡單問題
   - 例如：「你好，蝦仁」
   - 確認蝦仁能正確回應
10. **檢查連接狀態**
    - 在 Cloud Shell 查看 connector 日誌
    - 在 OpenClaw Dashboard 的 Usage 頁面確認有 LINE 的訊息紀錄

### 階段六：（選用）設定與優化
11. **配置 dmPolicy**（如需要）
    - 設定誰可以與蝦仁對話
    - 調整訊息回覆策略
12. **監控用量**
    - 留意免費方案的每日 30 次回覆限制
    - 決定是否需要升級到 Pro 方案

***

## ⚠️ 注意事項
1. **GCP Cloud Shell 限制**
   - Cloud Shell 閒置會斷線
   - `openclaw-line connect` 可能需要在每次 Cloud Shell 重啟後重新執行
2. **免費方案限制**
   - 每日 30 次 AI 回覆
   - 僅支援文字訊息
   - 如果超過額度，蝦仁會暫時無法回應
3. **持久化方案**
   - 如果要長期使用，建議考慮：
     - 使用 GCP Compute Engine（小型 VM）
     - 或升級到付費的 Cloud Shell Boost
