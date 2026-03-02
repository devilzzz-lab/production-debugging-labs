<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for PVC Pending State</h1>

<hr>

<h2>1️⃣ Check PVC Status</h2>
<pre>kubectl get pvc</pre>

<p><strong>Output:</strong></p>

<pre>
NAME       STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-pvc   Pending                                      standard       20s
</pre>

<p><strong>🔍 Key Finding:</strong> PVC is stuck in <code>Pending</code></p>

<hr>

<h2>2️⃣ Describe the PVC (First Step Always!)</h2>

<pre>kubectl describe pvc data-pvc</pre>

<pre>
Events:
  Type     Reason              Age    From                         Message
  ----     ------              ----   ----                         -------
  Warning  ProvisioningFailed  15s    persistentvolume-controller  no persistent volumes available for this claim
</pre>

<p><strong>🔍 Key Finding:</strong> <code>no persistent volumes available for this claim</code></p>

<hr>

<h2>3️⃣ Check Available PersistentVolumes</h2>

<pre>kubectl get pv</pre>

<p><strong>If Output is Empty:</strong></p>

<pre>No resources found</pre>

<p><strong>Meaning:</strong> No PV exists to satisfy the claim.</p>

<hr>

<h2>4️⃣ Check StorageClass</h2>

<pre>kubectl get sc</pre>

<p><strong>Check if Default StorageClass Exists:</strong></p>

<pre>
NAME                 PROVISIONER                RECLAIMPOLICY   VOLUMEBINDINGMODE   AGE
standard (default)   kubernetes.io/no-provisioner   Delete          Immediate           2d
</pre>

<p><strong>If no default StorageClass:</strong> Dynamic provisioning will fail.</p>

<hr>

<h2>5️⃣ Check Provisioner Pods (Dynamic Case)</h2>

<pre>kubectl get pods -A | grep provisioner</pre>

<p>If no CSI provisioner is running → PVC cannot be dynamically created.</p>

<hr>

<h2>🧠 What You Should Observe</h2>
<ul>
    <li><strong><code>STATUS: Pending</code></strong></li>
    <li><strong><code>ProvisioningFailed</code> event</strong></li>
    <li><strong>No matching PV available</strong></li>
    <li><strong>Missing or misconfigured StorageClass</strong></li>
</ul>

<p><strong>Root cause:</strong> No PersistentVolume or Dynamic Provisioner available to satisfy the claim.</p>

<pre><strong>Look for these keywords:</strong>
- "Pending"
- "ProvisioningFailed"
- "no persistent volumes available"
- "storageclass not found"
- "failed to provision volume"</pre>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.md">✅ How to Fix The Issue →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to PVC Pending</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>