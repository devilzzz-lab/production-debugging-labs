<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">📌 How I Created PVC Pending State Issue</h1>

<hr>

<h2>1️⃣ Create Broken PVC (No StorageClass)</h2>

<pre><code>manifest % kubectl apply -f pvc.yaml</code></pre>

<p><strong>✅ Output:</strong></p>
<pre><code>persistentvolumeclaim/data-pvc created</code></pre>

<hr>

<h2>2️⃣ Check PVC Stuck in Pending</h2>
<pre><code>kubectl get pvc</code></pre>

<p><strong>❌ Pending Forever:</strong></p>
<pre><code>
NAME        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-pvc    Pending  pvc-339fc84d-2c23-4ecf-97aa-2b8279785343   1Gi        RWO            standard       32m</code></pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>PVC created successfully</strong> ✅</li>
    <li><strong>No matching PV found</strong> ❌</li>
    <li><strong>No StorageClass</strong> → <strong>No dynamic provisioning</strong> ❌</li>
    <li><strong>PVC stays Pending indefinitely</strong> 🚫</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Pod CrashLoopBackOff</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
