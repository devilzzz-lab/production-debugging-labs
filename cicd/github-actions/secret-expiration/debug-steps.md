<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for Secret Expiration Issue</h1>

<hr>

<h2>1️⃣ Check Workflow Status</h2>

<pre>
CI Pipeline
❌ Failed
</pre>

<hr>

<h2>2️⃣ Identify Failed Step</h2>

<pre>
✔ Checkout Code
❌ Login to Docker
</pre>

<hr>

<h2>3️⃣ Check Error Logs</h2>

<pre>
docker login
Error response from daemon: unauthorized: incorrect username or password
</pre>

<p><strong>Observation:</strong> Authentication failed ❌</p>

<hr>

<h2>4️⃣ Verify Secrets Configuration</h2>

<p>Go to <strong>GitHub → Settings → Secrets</strong></p>

<pre>
DOCKER_USERNAME = correct
DOCKER_PASSWORD = ??? (hidden)
</pre>

<p><strong>Issue:</strong> Cannot directly see value → must verify manually</p>

<hr>

<h2>5️⃣ Validate Token Locally</h2>

<pre><code>
docker login -u username -p expired_token
</code></pre>

<p><strong>Result:</strong></p>

<pre>
unauthorized: incorrect username or password
</pre>

<hr>

<h2>6️⃣ Confirm Root Cause</h2>

<pre>
Root Cause: Expired / Invalid Secret Token
</pre>

<ul>
    <li><strong>Auth failed:</strong> Token no longer valid</li>
    <li><strong>Pipeline stopped:</strong> Cannot access external service</li>
    <li><strong>Deployment blocked:</strong> Login step failed</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.md">✅ How to Fix →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Secret Expiration</a> | 
    <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>