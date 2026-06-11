# Firebase Studio / Tailscale 踩坑完全攻略與 SOP

Firebase Studio 的工作區是用 `.idx/dev.nix` 定義的，`packages`、`env`、`idx.workspace.onCreate`、`idx.workspace.onStart` 都能放進去，而 Tailscale 在這類無 `tun` 的容器環境要走 `userspace-networking`，並由 SOCKS5 / HTTP proxy 讓容器內程式連出去。

## 根因紀錄

這次的坑有兩層：
1. **Userspace Networking**: Firebase Studio 工作區本質上是 Nix 定義環境，常見於容器式開發工作區；在這種情境下，Tailscale 的 `--tun=userspace-networking` 不是一般 TUN 網卡，而是讓 `tailscaled` 充當 SOCKS5 / HTTP proxy。所以 `tailscale ping` 能通，不代表原生 `ssh` / `scp` 會自動通。必須透過 SOCKS5 代理。
2. **SHELL 變數異常**: Nix / NixOS 類環境若把 `SHELL` 設成單純的 `bash`，會觸發 `Shell "bash" is not executable: No such file or directory` 錯誤。必須將 `SHELL` 設為真實的 bash 絕對路徑（例如透過 `readlink -f "$(command -v bash)"` 取得），`ssh -o ProxyCommand=...` 才會正常。

## 檔案佈局建議

為了讓設定可以被版控，同時又保護私密金鑰，建議採用以下目錄結構：

| 檔案 | 作用 |
|---|---|
| `.idx/dev.nix` | 工作區主設定，放 packages、env、onCreate、onStart 等。可進 Git。 |
| `.idx/dev.local.nix` | 本機或私密設定，例如 `TS_AUTHKEY`；`dev.nix` 可用 `imports` 條件式載入。**不可進 Git**。 |
| `.idx/scripts/tailscale-up.sh` | 啟動 `tailscaled`，並開 `127.0.0.1:1055` SOCKS5 / HTTP proxy。 |
| `.idx/scripts/ssh-openclaw.sh` | 經由 `nc + ProxyCommand` 透過 1055 連到 `openclaw-1`。 |
| `.idx/scripts/scp-from-openclaw.sh` | 從 `openclaw-1` 透過 Proxy 抓檔。 |
| `.gitignore` | 必須包含 `.idx/dev.local.nix`，避免把 auth key 提交出去。 |

## 排錯快查心法

- `tailscale ping` 通，但 `ssh/scp` 不通：優先查 1055 代理是否真的在 listen (`ss -lntp | grep 1055`)。
- `nc` 可看到 `SSH-2.0-...`，但 `ssh -o ProxyCommand=...` 失敗：優先查 `echo $SHELL` 的值是否被設成了單純的 `bash`。
- 核心心法：**Firebase Studio 用 `.idx/dev.nix` 管環境，Tailscale 在這裡要當 proxy 用，SSH 要透過 `nc` 代理，而 `SHELL` 不能是裸的 `bash`。**
