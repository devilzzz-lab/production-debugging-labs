 # ❌ Kubernetes Service Unreachable Issue

## 📌 Scenario

A Pod is running successfully, but the Service created to expose it is **not reachable**.

Even though:
- Pod status = Running
- Service is created
- No obvious crash

Still:
- curl <service-name>
- nslookup <service-name>
- Browser access

Fails.

---

## 🎯 Objective

Learn how to:
- Identify why Service is unreachable
- Debug selector issues
- Verify endpoints
- Fix label mismatches