<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔴 KUBERNETES SERVICE UNREACHABLE ISSUE</h1>

<p align="center">
<img src="https://img.shields.io/badge/Status-Service%20Not%20Reachable-red?logo=kubernetes&logoColor=white">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> Service exists but is not reachable.</p>
<p><strong>Impact:</strong> Application cannot be accessed via Service.</p>

<hr>

<h3>📌 Scenario</h3>

<p>
A Pod is running successfully, but the Service created to expose it is <strong>not reachable</strong>.
</p>

<ul>
    <li>✅ Pod status = Running</li>
    <li>✅ Service is created</li>
    <li>✅ No crash or error in Pod</li>
</ul>

<p><strong>Still:</strong></p>

<ul>
    <li>❌ <code>curl &lt;service-name&gt;</code> fails</li>
    <li>❌ <code>nslookup &lt;service-name&gt;</code> fails</li>
    <li>❌ Browser access fails</li>
</ul>

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