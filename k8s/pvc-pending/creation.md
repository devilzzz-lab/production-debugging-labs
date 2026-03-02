<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>📌 How I Created PVC Pending State Issue</h1>

<hr>

<h2>1️⃣ Apply the PVC YAML (Without PV or StorageClass)</h2>

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
  Type     Reason              Age    From                         Message
  ----     ------              ----   ----                         -------
  Warning  ProvisioningFailed  10s    persistentvolume-controller  no persistent volumes available for this claim
</pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>PVC created successfully</strong></li>
    <li><strong>No matching PersistentVolume found</strong></li>
    <li><strong>No dynamic provisioner available</strong> (or not configured)</li>
    <li><strong>PVC remains in Pending state</strong></li>
</ul>

<hr>

<h2>🧠 Why It Stays Pending?</h2>
<ul>
    <li>No PV exists that matches requested storage</li>
    <li>StorageClass may not exist</li>
    <li>Provisioner pod not running</li>
    <li>Access mode or size mismatch</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to PVC Pending</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>