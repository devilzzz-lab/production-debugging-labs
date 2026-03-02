<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">✅ How to Fix PVC Pending State</h1>

<hr>

<h2>📌 Scenario</h2>
<p>PVC stuck in <strong>Pending</strong> because <code>storageClassName: ""</code> disabled dynamic provisioning + no matching PV exists.</p>

<hr>

<h2>🛠️ Fix Method 1: Enable Dynamic Provisioning (SIMPLEST)</h2>

<h3>1️⃣ Edit PVC YAML</h3>
<p><strong>❌ Remove this line from <code>pvc.yaml</code>:</strong></p>
<pre><code># ❌ DELETE THIS:
# storageClassName: ""</code></pre>

<p><strong>✅ Fixed PVC:</strong></p>
<pre><code>apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: data-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
</code></pre>

<h3>2️⃣ Recreate PVC</h3>
<pre><code>kubectl delete pvc data-pvc --force
kubectl apply -f pvc.yaml</code></pre>

<h3>3️⃣ Verify Dynamic Provisioning</h3>
<pre><code>kubectl get pvc</code></pre>

<p><strong>✅ Auto-bound:</strong></p>
<pre><code>
NAME      STATUS   VOLUME       CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-pvc  Bound    pvc-xxx-yyy  1Gi        RWO            standard       10s</code></pre>

<hr>

<h2>🛠️ Fix Method 2: Static Provisioning (Manual PV)</h2>

<h3>1️⃣ Apply PV yaml</h3>
<pre><code>kubectl apply -f pv.yaml</code></pre>

<h3>2️⃣ Verify Static Binding</h3>
<pre><code>kubectl get pv,pvc</code></pre>

<p><strong>✅ Manual binding:</strong></p>
<pre><code>NAME                     CAPACITY   ACCESS MODES   STATUS   CLAIM              STORAGECLASS   AGE
pv/data-pv               1Gi        RWO            Bound    default/data-pvc   &lt;unset&gt;        15s
pvc/data-pvc             1Gi        RWO            Bound    data-pv            &lt;unset&gt;        20s</code></pre>

<hr>

<h2>🧠 What Fixed It?</h2>

<table>
<tr><th>Problem</th><th>Solution</th><th>Result</th></tr>
<tr><td><code>storageClassName: ""</code></td><td>Remove line → Use default</td><td>Dynamic provisioning ✅</td></tr>
<tr><td>No matching PV</td><td>Create exact PV match</td><td>Static binding ✅</td></tr>
<tr><td><code>&lt;unset&gt;</code> StorageClass</td><td>Default <code>standard</code></td><td>Auto-provisioned PV</td></tr>
</table>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="debug-steps.md">🔍 Debug Steps</a> | 
  <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
