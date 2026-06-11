# OpenClaw Browser Automation Troubleshooting Guide

*Source: Perplexity & User Provided (2026-02-21)*

## Common Issues & Solutions

### 1. "Can't reach the OpenClaw browser control service" / "tab not found"
**Symptoms:** Agent cannot use the browser, timeouts.
**Solutions:**
- Restart Gateway: `openclaw gateway restart`
- Clear Browser State: `rm -rf ~/.openclaw/browser-data/`
- (Extension Mode): Ensure "Browser Relay" extension is attached.

### 2. "Connection refused: 127.0.0.1:18789"
**Symptoms:** Gateway unreachable.
**Solutions:**
- Ensure Gateway is running (`openclaw gateway start`).
- Check port usage: `lsof -i :18789`
- Check Firewall/GCP Security Groups (Allow 18789, 18791, 18792, 18800+).

### 3. Linux Snap Chromium Compatibility (CRITICAL)
**Symptoms:** Chromium installed via Snap on Ubuntu fails to launch.
**Solution (Recommended):** Install official Google Chrome `.deb`.
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt --fix-broken install -y
```

### 4. Profile Ignored
**Solution:** Use `defaultProfile` in `config.json` instead of just `profile`.

### 5. Extension Relay Running but No Tab
**Solution:** Click the OpenClaw extension icon and ensure the badge says "ON" or "Connected".

## Diagnostics

**Health Check:**
```bash
openclaw doctor --fix
```

**Port Check:**
```bash
netstat -tlnp | grep -E '18789|18791|18792|18800'
```

## GCP VM Specifics
- **Headless:** Must be `true` (no GUI).
- **NoSandbox:** Must be `true` (root/container).
- **Binding:** Use `loopback` for security unless behind VPN.
