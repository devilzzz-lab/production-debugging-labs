<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔄 KUBERNETES READINESS & LIVENESS PROBE FAILURE</h1>

<p align="center">
<img src="https://img.shields.io/badge/Status-Probe%20Failure-orange?logo=kubernetes&logoColor=white">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> Pod is running but failing health probes.</p>
<p><strong>Impact:</strong> Pod either receives no traffic or keeps restarting.</p>

<hr>

<h3>📌 Scenario</h3>

<p>
Kubernetes uses <strong>health probes</strong> to monitor container health.
If probes are misconfigured, the Pod may behave unexpectedly.
</p>

<ul>
<li>Pod may stay in <code>0/1 READY</code> state</li>
<li>Service may not route traffic</li>
<li>Container may restart continuously</li>
</ul>

<p><strong>Common Symptoms:</strong></p>

<ul>
<li>❌ Pod shows <code>0/1 READY</code></li>
<li>❌ Service has no endpoints</li>
<li>❌ Pod restart count keeps increasing</li>
</ul>

<hr>

<h3>🔍 Types of Probe Failures</h3>

<ul>
<li><strong>Readiness Probe Failure</strong> — Pod runs but is not ready to accept traffic</li>
<li><strong>Liveness Probe Failure</strong> — Kubernetes restarts the container</li>
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