<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Debug - WaitForFirstConsumer</title>
</head>
<body>

<h1>🔍 Debug Steps for WaitForFirstConsumer Behavior</h1>

<hr>

<h2>1️⃣ Check PVC Status</h2>
<pre>kubectl get pvc</pre>

<p><strong>Output:</strong></p>

<pre>
NAME       STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-pvc   Pending                                      standard       20s
</pre>

<p><strong>Observation:</strong> PVC is in <code>Pending</code> state.</p>

<hr>

<h2>2️⃣ Describe the PVC (Always First Step)</h2>

<pre>kubectl describe pvc data-pvc</pre>

<pre>
Events:
  Type    Reason                Age               From                         Message
  ----    ------                ----              ----                         -------
  Normal  WaitForFirstConsumer  2s (x3 over 18s)  persistentvolume-controller  
  waiting for first consumer to be created before binding
</pre>

<p><strong>Key Finding:</strong> <code>WaitForFirstConsumer</code></p>

<hr>

<h2>3️⃣ Verify StorageClass Configuration</h2>

<pre>kubectl get sc</pre>

<pre>
standard (default)   rancher.io/local-path   Delete   WaitForFirstConsumer
</pre>

<p>
The StorageClass uses <code>WaitForFirstConsumer</code>, 
which delays volume binding until a Pod references the PVC.
</p>

<hr>

<h2>4️⃣ Verify Provisioner is Running</h2>

<pre>kubectl get pods -A | grep provisioner</pre>

<p>
Ensure the dynamic provisioner pod is <code>Running</code>.
</p>

<hr>

<h2>🧠 Root Cause</h2>
<ul>
    <li>VolumeBindingMode = <code>WaitForFirstConsumer</code></li>
    <li>No Pod is currently using this PVC</li>
    <li>Kubernetes intentionally delays binding</li>
</ul>

<hr>

<h2>🔎 Important Clarification</h2>

<p>
This is <strong>NOT a failure</strong>.  
Dynamic provisioning will occur automatically once a Pod consumes the PVC.
</p>

<pre><strong>Look for these keywords:</strong>
- "WaitForFirstConsumer"
- "waiting for first consumer"
- "Pending"
</pre>

<hr>

<h2>➡️ Next Step</h2>

<p>Create a Pod that uses this PVC to trigger binding.</p>
<p><a href="fix.md">✅ Trigger Binding →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to WaitForFirstConsumer</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>