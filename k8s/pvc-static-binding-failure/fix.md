<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ How I Fixed PVC Pending State</h1>

<hr>

<h2>📌 Scenario</h2>
<p>PVC was stuck in <strong>Pending</strong> state because no matching PersistentVolume (PV) or dynamic provisioner was available.</p>

<hr>

<h2>🛠️ Fix Method 1 — Static Provisioning (Manual PV Creation)</h2>

<h3>1️⃣ Create a PersistentVolume</h3>

<pre><code>
apiVersion: v1
kind: PersistentVolume
metadata:
  name: data-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data
</code></pre>

<h3>2️⃣ Apply the PV</h3>

<pre>kubectl apply -f pv.yaml</pre>

<h3>3️⃣ Verify Binding</h3>

<pre>kubectl get pvc</pre>

<p><strong>Expected Output:</strong></p>

<pre>
NAME       STATUS   VOLUME    RECLAIM POLICY  CAPACITY   ACCESS MODES   AGE   CLAIM        
data-pvc   Bound    data-pv   Retain          1Gi        RWO            30s   default/data-pvc
</pre>

<p>✅ PVC successfully bound to PV.</p>

<hr>

<h2>🛠️ Fix Method 2 — Dynamic Provisioning</h2>

<h3>1️⃣ Check StorageClass</h3>

<pre>kubectl get sc</pre>

<p>If no default StorageClass exists, create or configure one.</p>

<h3>2️⃣ Example StorageClass (Local Provisioner)</h3>

<pre><code>
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
</code></pre>

<h3>3️⃣ Ensure CSI / Provisioner Pod is Running</h3>

<pre>kubectl get pods -A | grep provisioner</pre>

<p>If provisioner is not running → install appropriate CSI driver.</p>

<h3>4️⃣ Recreate PVC</h3>

<pre>
kubectl delete pvc data-pvc
kubectl apply -f pvc.yaml
</pre>

<p>Expected Result: PVC automatically binds and creates PV.</p>

<hr>

<h2>⚠️ Common Mistakes</h2>
<ul>
    <li>Requested storage size larger than available PV</li>
    <li>Access mode mismatch (RWO vs RWX)</li>
    <li>Wrong StorageClass name</li>
    <li>No default StorageClass defined</li>
    <li>Provisioner pod not running</li>
</ul>

<hr>

<h2>🧠 Final Understanding</h2>

<p>PVC will move from <strong>Pending → Bound</strong> only when:</p>

<ul>
    <li>Matching PV exists (Static case)</li>
    <li>StorageClass + Provisioner is functioning (Dynamic case)</li>
    <li>Size, AccessMode, and StorageClass match correctly</li>
</ul>

<p><strong>Key Rule:</strong> PVC never binds randomly. Matching criteria must be satisfied.</p>

<hr>

<h2>🚀 Final Result</h2>

<p>✔ PVC successfully bound<br>
✔ Storage attached to Pod<br>
✔ Issue resolved</p>

<hr>

<p align="center">
    <a href="overview.md">← Back to PVC Pending</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>