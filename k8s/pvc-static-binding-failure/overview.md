<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔴 PVC STATIC BINDING FAILURE</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-FailedBinding-ff4444?logo=kubernetes&logoColor=white" alt="PVC FailedBinding">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> PVC stuck in <code>Pending</code> due to no matching PersistentVolume.</p>
<p><strong>Impact:</strong> Pod cannot start because storage is not available.</p>

<hr>

<h2>📂 All Resources</h2>

<table border="1" cellpadding="12" cellspacing="0">
    <tr>
        <td><strong><a href="creation.md">📌 How I Created Issue</a></strong></td>
        <td><strong><a href="debug-steps.md">🔍 How I Debug It</a></strong></td>
    </tr>
    <tr>
        <td><strong><a href="fix.md">✅ How I Fixed It</a></strong></td>
    </tr>
</table>

<hr>

<p align="center">
    <a href="../../categories/k8s.md">← Back to Kubernetes Issues</a>
</p>

</body>
</html>