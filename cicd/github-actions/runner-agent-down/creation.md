<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">📌 How I Created Runner / Agent Down Issue</h1>

<hr>

<h2>1️⃣ Stop Runner Service</h2>

<p><strong>GitHub Self-Hosted Runner:</strong></p>

<pre><code>cd actions-runner
./svc.sh stop
</code></pre>

<p><strong>GitLab Runner:</strong></p>

<pre><code>sudo systemctl stop gitlab-runner
</code></pre>

<hr>

<h2>2️⃣ (Optional) Kill Runner Process</h2>

<pre><code>ps aux | grep runner
kill -9 &lt;pid&gt;
</code></pre>

<hr>

<h2>3️⃣ Trigger Pipeline</h2>

<pre><code>git add .
git commit -m "trigger pipeline - runner down issue"
git push origin main
</code></pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>Pipeline triggers successfully</strong></li>
    <li><strong>No runner is available</strong> ❌</li>
    <li><strong>Job remains in queued state</strong></li>
    <li><strong>Runner shows offline/inactive</strong></li>
</ul>

<hr>

<h2>⚠️ Expected Errors</h2>
<pre><code>No runner available
Runner is offline
Waiting for a runner to pick up this job
</code></pre>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Runner / Agent Down</a> | 
    <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>