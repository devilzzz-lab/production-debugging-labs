<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">✅ How I Triggered PVC Binding (WaitForFirstConsumer)</h1>

<hr>

<h2>📌 Scenario</h2>
<p>
PVC was stuck in <strong>Pending</strong> state because no Pod was consuming the claim.
The StorageClass uses <code>WaitForFirstConsumer</code>, which delays volume binding 
until a Pod references the PVC.
</p>

<hr>

<h2>🛠️ Fix: Create a Pod That Uses the PVC</h2>

<h3>1️⃣ Apply the YAML</h3>

<pre><code>kubectl apply -f pod.yaml</code></pre>

<hr>

<h3>3️⃣ Verify Pod Status</h3>

<pre><code>kubectl get pods</code></pre>

<p><strong>Expected Output:</strong></p>

<pre>
NAME            READY   STATUS    RESTARTS   AGE
pvc-test-pod    1/1     Running   0          30s
</pre>

<hr>

<h3>4️⃣ Verify PVC Binding</h3>

<pre><code>kubectl get pvc data-pvc</code></pre>

<p><strong>Expected Output:</strong></p>

<pre>
NAME       STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-pvc   Bound    pvc-339fc84d-2c23-4ecf-97aa-2b8279785343   1Gi        RWO            standard       5m37s
</pre>

<p>✅ PVC successfully bound to a dynamically created PersistentVolume.</p>

<hr>

<h2>🧠 What Happened Internally?</h2>
<ul>
    <li>Scheduler selected a node for the Pod</li>
    <li>Dynamic provisioner created a new PV</li>
    <li>PVC bound to the newly created PV</li>
    <li>Pod mounted the volume successfully</li>
</ul>

<hr>

<h2>⚠️ Common Mistakes</h2>
<ul>
    <li>Assuming <code>Pending</code> always means failure</li>
    <li>Forgetting that <code>WaitForFirstConsumer</code> delays binding</li>
    <li>Not checking <code>kubectl describe pvc</code> events</li>
    <li>Deleting StorageClass accidentally</li>
</ul>

<hr>

<h2>🚀 Final Result</h2>

<p>
✔ PVC moved from <strong>Pending → Bound</strong><br>
✔ PV created automatically by provisioner<br>
✔ Pod successfully mounted storage<br>
✔ Expected Kubernetes behavior confirmed
</p>

<hr>

<h2>✅ Next Steps</h2>
<p>
    <a href="debug-steps.md">Debug Steps →</a>
</p>

<p align="center">
    <a href="overview.md">← Back to WaitForFirstConsumer</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>