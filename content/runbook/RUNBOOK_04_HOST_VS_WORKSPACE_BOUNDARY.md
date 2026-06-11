# RUNBOOK_04_HOST_VS_WORKSPACE_BOUNDARY.md

## 權限邊界
- **Host 絕對路徑 (/home/...)**：僅限維運人員與 docker 指令。
- **Workspace 相對路徑**：子代理日常操作唯一合法路徑。

## 禁止事項
- 嚴禁在 Sandbox 內嘗試存取 /home/ 或 /root/。
- 嚴禁子代理修改 .openclaw/ 內的 config 檔案。
