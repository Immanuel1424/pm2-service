# pm2-service
**PM2 Setup for Fullstack App (React + Node.js)**

---

### ✅ 1. Install PM2 globally

```bash
sudo npm install -g pm2
```

---

### ✅ 2. Navigate to your project directory

```bash
cd /opt/fullstack
```

---

### ✅ 3. Make sure your folder structure looks like:

```
/opt/fullstack/
├── server/
│   └── index.js           # Backend entry
└── client/
    └── build/             # React build output
```

---

### ✅ 4. Build your React frontend

> Only if you haven't already done this

```bash
cd /opt/fullstack/client
npm install
npm run build
```

---

### ✅ 5. Create `ecosystem.config.js`

```bash
vim ecosystem.config.js
```

Paste this content:

```js
module.exports = {
  apps: [
    {
      name: "backend",
      script: "/opt/fullstack/server/index.js",
      cwd: "/opt/fullstack/server",
      interpreter: "node",
      watch: false,
      env: {
        NODE_ENV: "production",
        PORT: 5000
      }
    },
    {
      name: "frontend",
      script: "serve",
      args: "-s build -l 3000",
      cwd: "/opt/fullstack/client",
      interpreter: "none",
      watch: false,
      env: {
        NODE_ENV: "production"
      }
    }
  ]
};
```

---

### ✅ 6. Install `serve` for frontend

```bash
sudo npm install -g serve
```

---

### ✅ 7. Start apps using PM2

```bash
pm2 start ecosystem.config.js
```

---

### ✅ 8. Save the PM2 process list

```bash
pm2 save
```

---

### ✅ 9. Set up PM2 to restart on reboot

```bash
pm2 startup
```

> It will output a command. Copy and run it with `sudo`.

---

### ✅ 10. Verify everything is running

```bash
pm2 ls
curl http://localhost:5000/api/users     # Test backend
curl http://localhost:3000               # Test frontend
```

---


