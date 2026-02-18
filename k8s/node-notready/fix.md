<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ How to Fix NodeNotReady</h1>

<hr>

<h2>1️⃣ Root Cause</h2>
<p>The node container (kubelet process) was stopped, causing the control plane to lose heartbeats and mark the node as NotReady.</p>

<h2>2️⃣ Fix: Restart Node Container</h2>
<pre>docker start debug-cluster-worker</pre>

<pre>debug-cluster-worker</pre>

<h2>3️⃣ Verify Node Recovery</h2>
<pre>kubectl get nodes --watch</pre>

<pre>NAME                          STATUS     ROLES           AGE   VERSION
debug-cluster-control-plane   Ready      control-plane   30m   v1.34.0
debug-cluster-worker          NotReady   <none>          30m   v1.34.0  ← Before
debug-cluster-worker          Ready      <none>          30m   v1.34.0  ← ✅ After 30s
debug-cluster-worker2         Ready      <none>          30m   v1.34.0</pre>

<h2>4️⃣ Check Taints Removed</h2>
<pre>kubectl describe node debug-cluster-worker | grep Taints</pre>

<pre>Taints: none  ← ✅ Clean</pre>

<h2>5️⃣ Verify Pods Rescheduled</h2>
<pre>kubectl get pods -o wide</pre>

<pre>NAME                           READY   STATUS    NODE                          AGE
app-pod-abc123                 1/1     Running   debug-cluster-worker         2m</pre>

<hr>

<h2>🧠 What Fixed It?</h2>
<ul>
    <li>❌ <strong>docker stop debug-cluster-worker:</strong> Kubelet stopped heartbeats</li>
    <li>✅ <strong>docker start debug-cluster-worker:</strong> Kubelet resumed reporting</li>
    <li>⏳ <strong>30s grace period:</strong> Control plane verified node health</li>
    <li>✅ <strong>Node Ready + Taints cleared + Pods rescheduled</strong></li>
</ul>

<pre><strong>Key Commands Used:</strong>
docker ps | grep debug-cluster-worker  ← Check container
docker start &lt;container&gt;              ← Fix
kubectl get nodes --watch             ← Verify
kubectl describe node                 ← Deep dive</pre>

<hr>

<p align="center">
    <a href="overview.html">← Back to Node NotReady</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
