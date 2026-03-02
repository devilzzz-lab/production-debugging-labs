<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">🔍 Debug Steps - PVC Pending State</h1>

<hr>

<h2>1️⃣ Check PVC Status</h2>
<pre><code>kubectl get pvc</code></pre>

<p><strong>❌ Symptom:</strong></p>
<pre><code>NAME      STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-pvc  Pending                      RWO   &lt;unset&gt;        20s</code></pre>

<p><strong>🔍 Key:</strong> <code>Pending</code> + <code>&lt;unset&gt;</code> StorageClass</p>

<hr>

<h2>2️⃣ Describe PVC (ALWAYS FIRST!)</h2>
<pre><code>kubectl describe pvc data-pvc</code></pre>

<p><strong>❌ Root Cause Event:</strong></p>
<pre><code>Events:
  Type    Reason         Age               From                         Message
  ----    ------         ----              ----                         -------
  Normal  FailedBinding  6s (x3 over 26s)  persistentvolume-controller  no persistent volumes available for this claim and no storage class is set</code></pre>

<p><strong>🔍 Keywords:</strong> <code>"no storage class is set"</code></p>

<hr>

<h2>3️⃣ List Available PVs</h2>
<pre><code>kubectl get pv</code></pre>

<p><strong>❌ No Matching PV:</strong></p>
<pre><code>No resources found</code></pre>

<p><strong>🔍 Meaning:</strong> No static PV matches 1Gi ReadWriteOnce</p>

<hr>

<h2>4️⃣ Check StorageClasses (TRICKY!)</h2>
<pre><code>kubectl get sc</code></pre>

<p><strong>✅ StorageClass EXISTS:</strong></p>
<pre><code>NAME                 PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
standard (default)   rancher.io/local-path   Delete          WaitForFirstConsumer   false                  77d</code></pre>

<p><strong>❌ BUT PVC YAML has:</strong></p>
<pre><code>spec:
  storageClassName: ""  # ❌ EMPTY STRING = DISABLES DYNAMIC PROVISIONING!</code></pre>

<p><strong>🔍 Key Insight:</strong></p>
<ul>
  <li>StorageClass <code>standard</code> exists ✅</li>
  <li><code>storageClassName: ""</code> = <strong>EXPLICITLY DISABLES dynamic provisioning</strong> ❌</li>
  <li>Only matches PVs with <strong>NO StorageClass</strong> (none exist)</li>
  <li><code>&lt;unset&gt;</code> in table confirms empty class requested</li>
</ul>

<hr>

<h2>5️⃣ Verify Pod Waiting</h2>
<pre><code>kubectl get pods</code></pre>

<p><strong>❌ Pod Stuck:</strong></p>
<pre><code>NAME      READY   STATUS             RESTARTS   AGE
app-pod   0/1     Pending            0          2m</code></pre>

<hr>

<h2>🧠 Diagnosis Summary</h2>

<table>
<tr><th>Command</th><th>What You See</th><th>Root Cause</th></tr>
<tr><td><code>get pvc</code></td><td><code>Pending</code> + <code>&lt;unset&gt;</code></td><td><code>storageClassName: ""</code></td></tr>
<tr><td><code>describe pvc</code></td><td><code>"no storage class is set"</code></td><td>Dynamic provisioning disabled</td></tr>
<tr><td><code>get sc</code></td><td><code>standard (default)</code> exists</td><td>PVC ignores it due to empty class</td></tr>
<tr><td><code>get pv</code></td><td>Empty list</td><td>No no-class PVs available</td></tr>
</table>

<hr>

<h2>✅ Next Steps</h2>
<p align="center">
  <a href="fix.md" style="font-size:1.5em">🔧 How to Fix →</a>
</p>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
