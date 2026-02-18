<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔴 Node NotReady</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-NotReady-ff4444?logo=kubernetes&logoColor=white" alt="NodeNotReady">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> Node entering NotReady state after worker node process stops</p>
<p><strong>Environment:</strong> KIND Cluster (Multi-node)</p>
<p><strong>Impact:</strong> Pods evicted, workloads disrupted</p>

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
kubectl get nodes
kubectl describe node &lt;notready-node&gt;
kubectl get pods -o wide
journalctl -u kubelet -f
docker ps | grep &lt;node-name&gt;
</pre>

<hr>

<p align="center">
    <a href="../../categories/k8s.md">← Back to Kubernetes Issues</a> | 
    <a href="../../README.md">🏠 Back to Main README</a>
</p>

</body>
</html>
