<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ How to Fix OOMKilled</h1>
<hr>

<h2>2️⃣ Fix: Increase Memory Limit</h2>
<pre>kubectl edit pod oom-demo</pre>

<p><strong>Change:</strong></p>
<pre>limits:
  memory: "50Mi"     ← ❌ Too low (stress needs 200M)</pre>

<p><strong>To:</strong></p>
<pre>limits:
  <strong>memory: "300Mi"</strong>  ← ✅ Fixed</pre>

<h2>3️⃣ Verify Pod Recovery</h2>
<pre>kubectl get pods --watch</pre>

<pre>NAME       READY   STATUS      RESTARTS   AGE
oom-demo   0/1     OOMKilled     2         45s  ← Before
oom-demo   1/1     <strong>Running</strong>   2         60s  ← ✅ Fixed</pre>

<h2>4️⃣ Check Logs (Stable Now)</h2>
<pre>kubectl logs oom-demo</pre>

<pre>stress: info: [1] dispatching hogs (1, 1 vm, 1 io, 1 cpu, 1 hdd)
stress: info: [1] successful run completed in 60s  ← ✅ Healthy</pre>

<hr>

<h2>🧠 What Fixed It?</h2>
<ul>
    <li>❌ <strong>50Mi memory limit:</strong> Stress container needs 200M → OOMKilled (Exit 137)</li>
    <li>✅ <strong>300Mi memory limit:</strong> Container runs without kernel termination</li>
    <li>⏳ <strong>Pod recreated:</strong> Kubernetes detected resource change → restarted</li>
    <li>✅ <strong>Running + Stable logs + No restarts</strong></li>
</ul>

<pre><strong>Key Commands Used:</strong>
kubectl edit pod oom-demo              ← Fix resources
kubectl get pods --watch              ← Verify status
kubectl logs oom-demo                 ← Check application
kubectl describe pod oom-demo         ← Deep dive</pre>

<hr>

<p align="center">
    <a href="overview.md">← Back to OOMKilled</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
