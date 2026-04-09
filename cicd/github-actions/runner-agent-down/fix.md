# ✅ Fix: Runner / Agent Down

## 🔧 Fix 1: Restart Runner

### GitHub Runner

```bash
./svc.sh start
```

### GitLab Runner

```bash
sudo systemctl restart gitlab-runner
```

---

## 🔧 Fix 2: Re-register Runner

```bash
./config.sh remove
./config.sh
```

---

## 🔧 Fix 3: Fix Network

```bash
sudo systemctl restart networking
```

---

## 🔧 Fix 4: Ensure Auto Start

```bash
sudo systemctl enable gitlab-runner
```

---

## 🔧 Fix 5: Increase Resources

* Add CPU/RAM
* Clean disk space

---

## 🔧 Fix 6: Restart Machine

```bash
sudo reboot
```

---

## 🎯 Final Verification

* Runner status = ✅ Online
* Pipeline executes successfully
* Jobs no longer stuck
