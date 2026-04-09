# 🛠️ How to Reproduce Runner Down Issue

## 🧪 Scenario 1: Stop Runner Service

### GitHub Actions (Self-hosted runner)

```bash
./svc.sh stop
```

### GitLab Runner

```bash
sudo gitlab-runner stop
```

---

## 🧪 Scenario 2: Kill Runner Process

```bash
ps aux | grep runner
kill -9 <pid>
```

---

## 🧪 Scenario 3: Disconnect Network

```bash
sudo ifconfig eth0 down
```

---

## 🧪 Scenario 4: Expire Token

* Remove runner config
* Or invalidate token from dashboard

---

## 🧪 Expected Result

* Runner shows **offline**
* Pipeline stuck in queue
* Jobs fail with:
  "No runner available"
