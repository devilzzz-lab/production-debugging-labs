<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔴 Pod CrashLoopBackOff</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-CRASHLOOPBACKOFF-ff4444?logo=kubernetes&logoColor=white" alt="CrashLoopBackOff">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> Pod entering CrashLoopBackOff state after deployment</p>
<p><strong>Environment:</strong> EKS cluster</p>
<p><strong>Impact:</strong> Application unavailable</p>

<hr>

<h2>📂 All Resources</h2>

<p><em>👆 Click below to explore the complete debugging journey</em></p>

<table border="1" cellpadding="12" cellspacing="0">
    <tr>
        <td>
            <strong><a href="cheatsheet.md">📋 Cheatsheet</a></strong>
        </td>
        <td>
            <strong><a href="debug-steps.md">🔍 Debug Steps</a></strong>
        </td>
    </tr>
    <tr>
        <td>
            <strong><a href="fix.md">✅ Fix</a></strong>
        </td>
        <td>
            <strong><a href="logs.txt">📄 Logs</a></strong>
        </td>
    </tr>
    <tr>
        <td>
            <strong><a href="overview.md">📖 Overview</a></strong>
        </td>
        <td>
            <strong><a href="prevention.md">🛡️ Prevention</a></strong>
        </td>
    </tr>
    <tr>
        <td>
            <strong><a href="root-cause.md">🎯 Root Cause</a></strong>
        </td>
        <td>
            <strong><a href="symptoms.md">⚠️ Symptoms</a></strong>
        </td>
    </tr>
</table>

<hr>

<h2>🚀 Quick Actions</h2>
<pre>
kubectl get pods
kubectl describe pod &lt;pod-name&gt;
kubectl logs &lt;pod-name&gt; --previous
</pre>

<p align="center">
    <a href="../categories/k8s.html">← Back to Kubernetes Issues</a> | 
    <a href="../../README.html">🏠 Back to Main README</a>
</p>

</body>
</html>
