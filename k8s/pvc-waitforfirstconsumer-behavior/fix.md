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
<p>PVC was stuck in <strong>Pending</strong> state because no matching Pod is availabe for pvc claim (PV) or dynamic provisioner was available.</p>

<hr>

<h2>🛠️ Fix Method </h2>

<h3>1️⃣ Create a Pod</h3>

<h3>2️⃣ Apply the Yaml</h3>

<pre>kubectl apply -f pod.yaml</pre>

<h3>3️⃣ Verify Binding</h3>

<pre>kubectl get pod</pre>

<p><strong>Expected Output:</strong></p>

<pre>     
pvc-test-pod   1/1     Running   0              30s
</pre>

<p>✅ PVC successfully bound to PV.</p>

kubectl get pvc data-pvc 
NAME       STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
data-pvc   Bound    pvc-339fc84d-2c23-4ecf-97aa-2b8279785343   1Gi        RWO            standard       <unset>                 5m37s


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