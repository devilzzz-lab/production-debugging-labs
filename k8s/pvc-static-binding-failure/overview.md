<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">🔴 PVC Static Binding Failure</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-FailedBinding-ff4444?logo=kubernetes&logoColor=white" alt="PVC FailedBinding">
</p>

<hr>

<h2 align="center">🚨 Issue Summary</h2>
<p align="center"><strong>Issue:</strong> PVC stuck in <code>Pending</code> due to no matching PersistentVolume.</p>
<p align="center"><strong>Impact:</strong> Pod cannot start because storage is not available.</p>

<hr>

<h2 align="center">📂 All Resources</h2>

<table align="center" border="1" cellpadding="12" cellspacing="0" style="margin: 0 auto;">
    <tr>
        <td align="center"><a href="creation.md"><strong>📌 How I Created Issue</strong></a></td>
        <td align="center"><a href="debug-steps.md"><strong>🔍 How I Debug It</strong></a></td>
    </tr>
    <tr>
        <td align="center"><a href="fix.md"><strong>✅ How I Fixed It</strong></a></td>
        <td align="center"></td>
    </tr>
</table>

<hr>

<p align="center">
    <a href="../../categories/k8s.md">← Back to Kubernetes Issues</a>
</p>

</body>
</html>
