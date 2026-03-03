# ✅ Fixing Service Unreachable Issue

## Root Cause

Service selector label does not match Pod label.

Pod Label:
app=nginx-app

Service Selector:
app=wrong-label

---

## Fix Method 1: Edit Service

kubectl edit svc nginx-service

Change:

selector:
  app: nginx-app

Save and exit.

---

## Verify Fix

kubectl get endpoints nginx-service

Now you should see:

nginx-service   10.244.0.5:80

---

## Test Again

kubectl run test --rm -it --image=busybox -- sh

wget -qO- nginx-service

✅ NGINX welcome page appears.