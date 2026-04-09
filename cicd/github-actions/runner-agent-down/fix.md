<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ How to Fix Runner / Agent Down</h1>
<hr>

<h2>1️⃣ Fix: Start Runner Service</h2>

<p><strong>GitHub Self-Hosted Runner:</strong></p>

<pre>cd actions-runner
./svc.sh start</pre>

<p><strong>GitLab Runner:</strong></p>

<pre>sudo systemctl start gitlab-runner</pre>

<p><strong>Problem Before:</strong></p>
<pre>
Runner is offline
No runner available
Job stuck in queue
</pre>

<p><strong>After Fix:</strong></p>
<pre>
Runner is online
Job picked by runner
</pre>

<hr>

<h2>2️⃣ Ensure Auto-Start on Boot</h2>

<pre>sudo systemctl enable gitlab-runner</pre>

<p><strong>Why:</strong> Prevent runner from going down after system restart</p>

<hr>

<h2>3️⃣ (Optional) Re-register Runner</h2>

<pre>cd actions-runner
./config.sh remove
./config.sh</pre>

<p><strong>Use Case:</strong> Token expired or runner misconfigured</p>

<hr>

<h2>4️⃣ Restart System (if needed)</h2>

<pre>sudo reboot</pre>

<hr>

<h2>5️⃣ Verify Pipeline Success</h2>

<p>Go to <strong>GitHub → Actions</strong></p>

<pre>
✔ Workflow triggered
✔ Runner assigned
✔ Job started
✔ Steps executing

✅ <strong>Pipeline Running Successfully</strong>
</pre>

<hr>

<h2>🧠 What Fixed It?</h2>

<ul>
    <li>❌ <strong>Runner stopped:</strong> No execution environment available</li>
    <li>✅ <strong>Runner started:</strong> Jobs can now be executed</li>
    <li>⏳ <strong>Pipeline resumed:</strong> Jobs picked from queue</li>
    <li>✅ <strong>Execution successful:</strong> CI/CD flow restored</li>
</ul>

<pre><strong>Key Commands Used:</strong>
./svc.sh start                     ← Start GitHub runner
sudo systemctl start gitlab-runner ← Start GitLab runner
sudo systemctl enable gitlab-runner← Enable auto-start
./config.sh                       ← Re-register runner
gh run list                       ← View runs
gh run rerun &lt;run-id&gt;             ← Re-run pipeline</pre>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="debug-steps.md">🔍 Debug Steps</a> | 
  <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>