<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🟡 PVC PENDING STATE</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-Pending-ffbb33?logo=kubernetes&logoColor=white" alt="PVC Pending">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> PersistentVolumeClaim (PVC) remains stuck in <code>Pending</code> state.</p>
<p><strong>Impact:</strong> Pod cannot start because requested storage is not provisioned or bound.</p>

<hr>

<h2>📂 All Resources</h2>

<p><em>👆 Click below to explore the complete debugging journey</em></p>

<table border="1" cellpadding="12" cellspacing="0">
    <tr>
        <td>
            <strong><a href="creation.md">📌 How I Created Issue</a></strong>
        </td>
        <td>
            <strong><a href="debug-steps.md">🔍 How I Debug It</a></strong>
        </td>
    </tr>
    <tr>
        <td>
            <strong><a href="fix.md">✅ How I Fixed It</a></strong>
        </td>
    </tr>
</table>

<hr>

<h2>🚀 Quick Actions</h2>
<pre>
kubectl get pvc
kubectl describe pvc &lt;pvc-name&gt;
kubectl get pv
kubectl get sc
kubectl get pods -A | grep provisioner
kubectl get events --sort-by=.lastTimestamp
</pre>

<hr>

<h2>🧠 Root Cause Categories</h2>
<ul>
    <li>No matching PersistentVolume available</li>
    <li>No default StorageClass defined</li>
    <li>Dynamic provisioner (CSI) not running</li>
    <li>Access mode / size mismatch</li>
</ul>

<hr>

<p align="center">
    <a href="../../categories/k8s.md">← Back to Kubernetes Issues</a> | 
    <a href="../../README.md">🏠 Back to Main README</a>
</p>

</body>
</html>