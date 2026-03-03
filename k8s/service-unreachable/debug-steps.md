
---

# 📁 3️⃣ debug-steps.md

```markdown
# 🔍 Debugging Steps

## 1️⃣ Check Pods

kubectl get pods

Ensure pod is Running.

---

## 2️⃣ Check Service

kubectl get svc

Confirm service exists.

---

## 3️⃣ Check Endpoints (Very Important)

kubectl get endpoints nginx-service

If output shows:

NAME             ENDPOINTS   AGE
nginx-service    <none>

🚨 This means Service is not linked to any Pod.

---

## 4️⃣ Check Pod Labels

kubectl get pods --show-labels

You will see:

app=nginx-app

---

## 5️⃣ Check Service Selector

kubectl describe svc nginx-service

Selector will show:

app=wrong-label

🚨 Mismatch found.