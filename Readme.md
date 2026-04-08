# bridge-release

Prebuilt **XUI bridge** binaries for integrating a panel with **UCS** 

**Requirements on the XUI host:** `curl`, `wget`, MySQL client libraries for `bridge_send`, UCS-reachable API URL as configured in the bridge source. Config is read from **`/home/xui/config/new_config.ini`** (database section).

---

**Public repo, run as root** (paths under `/home/xui/bin`):

```bash
latest_version=$(curl -s https://api.github.com/repos/hserver71/bridge-release/releases/latest | grep '"tag_name":' | cut -d '"' -f 4) && mkdir -p /home/xui/bin && wget -q -O /home/xui/bin/bridge_fetch "https://github.com/hserver71/bridge-release/releases/download/${latest_version}/bridge_fetch" && wget -q -O /home/xui/bin/bridge_send "https://github.com/hserver71/bridge-release/releases/download/${latest_version}/bridge_send" && chmod +x /home/xui/bin/bridge_fetch /home/xui/bin/bridge_send && chown xui:xui /home/xui/bin/bridge_fetch /home/xui/bin/bridge_send && { pkill -f /home/xui/bin/bridge_fetch 2>/dev/null || true; pkill -f /home/xui/bin/bridge_send 2>/dev/null || true; rm -f /tmp/app.sock /tmp/app_send.sock; }; sudo -u xui /home/xui/bin/bridge_fetch >/dev/null 2>&1 & sudo -u xui /home/xui/bin/bridge_send >/dev/null 2>&1 &
```

---

## Source and building yourself

Build scripts and C sources live in the **`Bridge`** project. Publishing a release uses **`/home/Bridge/install build`** with **`GITHUB_TOKEN`**. This repo only stores **release binaries** on [Releases](https://github.com/hserver71/bridge-release/releases).
