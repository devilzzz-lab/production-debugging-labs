<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔴 DNS FAILURE</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-OOMKilled-ff4444?logo=kubernetes&logoColor=white" alt="OOMKilled">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> While testing Kubernetes internal DNS resolution, THE DNS failed</p>
<p><strong>Impact:</strong> the pod is not using coredns ip , it is using google dns whichis already defined in yaml file , to </p>

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
kubectl get pods
kubectl describe pod &lt;oom-pod&gt;
kubectl logs &lt;oom-pod&gt; --previous
kubectl get events --sort-by=.lastTimestamp
kubectl top pod &lt;oom-pod&gt;
</pre>

<hr>

<p align="center">
    <a href="../../categories/k8s.md">← Back to Kubernetes Issues</a> | 
    <a href="../../README.md">🏠 Back to Main README</a>
</p>

</body>
</html>
