# RUNBOOK_03_SANDBOX_TOOL_FALLBACKS.md

## 工具失敗降級順序
1. **優先級 1**：edit/write（Sandbox 內相對路徑）
2. **優先級 2**：exec "cat > path" <<EOF ... EOF（降級純文字）
3. **優先級 3**：print 到 session（最後手段，由人工補救）

## 常見錯誤
- **Path escapes sandbox root**：改用相對路徑。
- **python3 not found**：改用 exec cat。
