# 🔍 Debug Steps for Runner / Agent Down

## ✅ Step 1: Check Runner Status

### GitHub

Go to:
Settings → Actions → Runners

Check:

* Online / Offline status

---

## ✅ Step 2: Check Service Status

### Linux

```bash
sudo systemctl status gitlab-runner
```

or

```bash
./svc.sh status
```

---

## ✅ Step 3: Check Running Processes

```bash
ps aux | grep runner
```

---

## ✅ Step 4: Check Logs

### GitHub Runner

```bash
cd _diag
cat Runner_*.log
```

### GitLab Runner

```bash
sudo journalctl -u gitlab-runner
```

---

## ✅ Step 5: Check Network Connectivity

```bash
ping github.com
```

or

```bash
curl -I https://github.com
```

---

## ✅ Step 6: Check Disk & Memory

```bash
df -h
free -m
```

---

## ✅ Step 7: Verify Token/Auth

* Re-check registration token
* Validate runner config

---

## 🚨 Common Findings

* Service not running ❌
* Runner process missing ❌
* Network unreachable ❌
* Token expired ❌
