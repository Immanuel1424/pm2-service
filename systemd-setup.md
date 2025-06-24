Here's a complete `README.md` template for setting up and managing a **systemd service** in a Linux environment. This is ideal for apps like Node.js, Python scripts, or any long-running background service.

---

```markdown
# systemd Service Setup

This guide explains how to create and manage a systemd service for this application, enabling it to start on boot, restart on failure, and run in the background like a native system service.

---

## 🛠 Prerequisites

- Linux system with `systemd` (Ubuntu 16.04+, CentOS 7+, Debian 8+, etc.)
- Application executable or script (Node.js, Python, binary, etc.)
- `sudo` access

---

## 📁 Directory Structure (Example)

```

/home/ubuntu/my-app/
│
├── start.sh                # Your startup script
├── backend.service         # Example systemd unit file
└── other files...

````

---

## 📄 Step 1: Create systemd Service File

Create a new service file in `/etc/systemd/system/`.

```bash
sudo nano /etc/systemd/system/backend.service
````

### Example: Node.js/Express Backend

```ini
[Unit]
Description=My Backend Service
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/my-app/server
ExecStart=/usr/bin/node index.js
Restart=always
RestartSec=5
Environment=PORT=5000
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```

> Replace paths and environment variables based on your project.

---

## 🔄 Step 2: Reload systemd and Enable Service

```bash
sudo systemctl daemon-reexec       # optional, full reload
sudo systemctl daemon-reload       # reload systemd manager config
sudo systemctl enable backend.service
sudo systemctl start backend.service
```

---

## ✅ Step 3: Manage the Service

| Command                          | Description         |
| -------------------------------- | ------------------- |
| `sudo systemctl start backend`   | Start the service   |
| `sudo systemctl stop backend`    | Stop the service    |
| `sudo systemctl restart backend` | Restart the service |
| `sudo systemctl status backend`  | View service status |
| `journalctl -u backend -f`       | View real-time logs |

---

## 🧪 Validation

Make sure the service is running:

```bash
sudo systemctl status backend.service
```

Check if it starts on reboot:

```bash
sudo reboot
```

Then verify with:

```bash
sudo systemctl status backend.service
```

---

## 🧼 Optional: Clean Up

To disable and remove the service:

```bash
sudo systemctl disable backend.service
sudo rm /etc/systemd/system/backend.service
sudo systemctl daemon-reload
```

---

## 📝 Notes

* Ensure `ExecStart` uses full paths (e.g., `/usr/bin/node`, not just `node`).
* Use `chmod +x` for custom startup scripts.
* For frontend services (e.g., React), replace `ExecStart` with your start command (e.g., `serve -s build`).

---


