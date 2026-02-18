<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps</h1>

<hr>

<h2>1️⃣ Check Node Status</h2>
<pre>kubectl get nodes</pre>

<pre>NAME                          STATUS     ROLES           AGE   VERSION
debug-cluster-control-plane   Ready      control-plane   19m   v1.34.0
debug-cluster-worker          <strong>NotReady</strong>   <none>          18m   v1.34.0
debug-cluster-worker2         Ready      <none>          18m   v1.34.0</pre>

<h2>2️⃣ Check Node Describe (First!)</h2>
<pre>kubectl describe node debug-cluster-worker</pre>

<pre>Conditions:
  Type             Status    LastHeartbeatTime                 LastTransitionTime                Reason              Message
  ----             ------    -----------------                 ------------------                ------              -------
  MemoryPressure   Unknown   Wed, 18 Feb 2026 11:36:12 +0530   Wed, 18 Feb 2026 11:37:16 +0530   NodeStatusUnknown   <strong>Kubelet stopped posting node status.</strong>
  DiskPressure     Unknown   Wed, 18 Feb 2026 11:36:12 +0530   Wed, 18 Feb 2026 11:37:16 +0530   NodeStatusUnknown   <strong>Kubelet stopped posting node status.</strong>
  PIDPressure      Unknown   Wed, 18 Feb 2026 11:36:12 +0530   Wed, 18 Feb 2026 11:37:16 +0530   NodeStatusUnknown   <strong>Kubelet stopped posting node status.</strong>
  <strong>Ready            Unknown   Wed, 18 Feb 2026 11:36:12 +0530   Wed, 18 Feb 2026 11:37:16 +0530   NodeStatusUnknown   Kubelet stopped posting node status.</strong></pre>

<p><strong>🔍 Key Finding:</strong> <code>Kubelet stopped posting node status</code> → <strong>Node process down!</strong></p>

<h2>3️⃣ Check Events</h2>
<pre>kubectl get events --sort-by=.metadata.creationTimestamp</pre>

<pre>18m         Normal   NodeNotReady              node/debug-cluster-worker          <strong>Node debug-cluster-worker status is now: NodeNotReady</strong></pre>

<h2>4️⃣ Check Docker Containers</h2>

<pre>docker ps | grep debug-cluster-worker</pre>

<pre>CONTAINER ID   IMAGE                  STATUS          NAMES
b09ad1d0abab   kindest/node:v1.34.0   Up 20 minutes   debug-cluster-control-plane
d04426a555e4   kindest/node:v1.34.0   Up 20 minutes   debug-cluster-worker2
# debug-cluster-worker MISSING 👈</pre>

<p><strong>💡 Analysis:</strong></p>
<ul>
    <li><strong>Kubelet heartbeat missing</strong> → Node NotReady</li>
    <li><strong>Docker container stopped</strong> → Node process down</li>
    <li><strong>Taints added:</strong> NoExecute + NoSchedule</li>
    <li><strong>Pods evicted</strong> from node</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.md">How to Fix The Issue →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Node NotReady</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
