<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>📌 How I Created NodeNotReady Issue</h1>

<hr>

<h2>1️⃣ Create KIND Cluster</h2>

<pre><code>kind create cluster --name debug-cluster --config - &lt;&lt;EOF
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
EOF</code></pre>

<p><strong>Output:</strong></p>
<pre>Creating cluster "debug-cluster" ...
 ✓ Ensuring node image (kindest/node:v1.34.0) 🖼
 ✓ Preparing nodes 📦 📦 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
 ✓ Joining worker nodes 🚜 
Set kubectl context to "kind-debug-cluster"</pre>

<h2>2️⃣ Verify Healthy Cluster</h2>
<pre>kubectl get nodes
NAME                          STATUS   ROLES           AGE   VERSION
debug-cluster-control-plane   Ready    control-plane   53s   v1.34.0
debug-cluster-worker          Ready    <none>          38s   v1.34.0
debug-cluster-worker2         Ready    <none>          38s   v1.34.0</pre>

<h2>3️⃣ Trigger NodeNotReady</h2>
<pre>docker stop debug-cluster-worker</pre>

<h2>⏳ Watch Node Status Change:</h2>
<pre>kubectl get nodes --watch
NAME                          STATUS     ROLES           AGE     VERSION
debug-cluster-control-plane   Ready      control-plane   77s     v1.34.0
debug-cluster-worker          Ready      <none>          62s     v1.34.0
debug-cluster-worker2         Ready      <none>          62s     v1.34.0
debug-cluster-worker          <strong>NotReady</strong>   <none>          104s    v1.34.0
debug-cluster-worker          <strong>NotReady</strong>   <none>          104s    v1.34.0</pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>All nodes Ready initially</strong></li>
    <li><strong>docker stop worker:</strong> Node process stops</li>
    <li><strong>Node becomes NotReady</strong> (kubelet stops heartbeats)</li>
    <li><strong>Pods on node:</strong> Evicted or pending</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.html">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="index.html">← Back to NodeNotReady</a> | 
    <a href="../../categories/k8s.html">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
