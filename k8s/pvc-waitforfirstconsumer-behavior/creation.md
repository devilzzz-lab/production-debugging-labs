<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>📌 How I Observed WaitForFirstConsumer Behavior</h1>

<hr>

<h2>1️⃣ Apply the PVC YAML</h2>

<pre><code>manifest % kubectl apply -f pvc.yaml
persistentvolumeclaim/data-pvc created</code></pre>

<h2>2️⃣ Check PVC Status</h2>

<pre><code>manifest % kubectl get pvc</code></pre>

<p><strong>Output:</strong></p>

<pre>
NAME       STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-pvc   Pending                                      standard       5s
</pre>

<hr>

<h2>3️⃣ Describe the PVC</h2>

<pre><code>manifest % kubectl describe pvc data-pvc</code></pre>

<p><strong>Events Output:</strong></p>

<pre>
Events:
  Type    Reason                Age               From                         Message
  ----    ------                ----              ----                         -------
  Normal  WaitForFirstConsumer  2s (x3 over 18s)  persistentvolume-controller  waiting for first consumer to be created before binding
</pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>PVC created successfully</strong></li>
    <li><strong>Default StorageClass is configured</strong></li>
    <li><strong>Provisioner is running</strong></li>
    <li><strong>VolumeBindingMode = WaitForFirstConsumer</strong></li>
    <li><strong>PVC waits until a Pod consumes it</strong></li>
</ul>

<hr>

<h2>🧠 Why It Stays Pending?</h2>
<ul>
    <li>StorageClass uses <code>WaitForFirstConsumer</code></li>
    <li>Kubernetes delays volume creation until Pod scheduling</li>
    <li>This prevents wrong-node volume allocation</li>
</ul>

<hr>

<h2>🎯 Important Clarification</h2>

<p>
This is <strong>NOT a failure</strong>.  
This is expected behavior in modern Kubernetes clusters.
</p>

<hr>

<h2>✅ Next Steps</h2>
<p>Create a Pod that uses this PVC to trigger binding.</p>
<p><a href="debug-steps.md">🔍 Continue Debugging →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to WaitForFirstConsumer</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>