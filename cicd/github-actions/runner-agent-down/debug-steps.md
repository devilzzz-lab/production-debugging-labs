<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for Runner / Agent Down</h1>

<hr>

<h2>1️⃣ Check Workflow Status</h2>
<pre>Go to GitHub → Actions → Select Workflow</pre>

<pre>
CI Pipeline
⏳ Waiting / Queued
</pre>

<p><strong>Observation:</strong> Job is not starting</p>

<hr>

<h2>2️⃣ Check Runner Availability</h2>
<pre>Go to GitHub → Settings → Actions → Runners</pre>

<pre>
Self-hosted Runner
❌ Offline
</pre>

<p><strong>Issue:</strong> No active runner available</p>

<hr>

<h2>3️⃣ Check Job Logs</h2>
<pre>Open workflow run → View logs</pre>

<pre>
Waiting for a runner to pick up this job...
No runner available
</pre>

<hr>

<h2>4️⃣ Check Runner Service Status</h2>

<p><strong>GitHub Runner:</strong></p>

<pre><code>cd actions-runner
./svc.sh status
</code></pre>

<p><strong>GitLab Runner:</strong></p>

<pre><code>sudo systemctl status gitlab-runner
</code></pre>

<p><strong>Observation:</strong> Service is not running ❌</p>

<hr>

<h2>5️⃣ Check Running Processes</h2>

<pre><code>ps aux | grep runner
</code></pre>

<p><strong>Observation:</strong> No runner process found ❌</p>

<hr>

<h2>6️⃣ Check Network Connectivity</h2>

<pre><code>ping github.com
</code></pre>

<p><strong>Possible Issue:</strong> Runner cannot reach GitHub</p>

<hr>

<h2>7️⃣ Check Runner Logs</h2>

<p><strong>GitHub Runner:</strong></p>

<pre><code>cd actions-runner/_diag
cat Runner_*.log
</code></pre>

<p><strong>GitLab Runner:</strong></p>

<pre><code>sudo journalctl -u gitlab-runner
</code></pre>

<p><strong>Look for:</strong></p>
<ul>
    <li>Authentication errors</li>
    <li>Connection failures</li>
    <li>Unexpected shutdown</li>
</ul>

<hr>

<h2>8️⃣ Confirm Root Cause</h2>

<pre>
Root Cause: Runner service is stopped / offline
</pre>

<p><strong>🔍 Key Findings:</strong></p>
<ul>
    <li><strong>No runner available:</strong> Jobs not assigned</li>
    <li><strong>Runner offline:</strong> Service not running</li>
    <li><strong>Pipeline stuck:</strong> Execution never starts</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.md">✅ How to Fix →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Runner / Agent Down</a> | 
    <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>