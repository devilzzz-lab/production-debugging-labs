<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ How to Fix Secret Expiration Issue</h1>

<hr>

<h2>1️⃣ Generate New Token</h2>

<p><strong>Docker:</strong></p>
<pre><code>
docker logout
docker login
</code></pre>

<p><strong>GitHub PAT:</strong></p>
<p>Go to <strong>GitHub → Settings → Developer Settings → Personal Access Tokens</strong></p>

<hr>

<h2>2️⃣ Update Secret in GitHub</h2>

<p>Go to <strong>Settings → Secrets → Actions</strong></p>

<pre><code>
DOCKER_PASSWORD = new_valid_token
</code></pre>

<hr>

<h2>3️⃣ Commit and Trigger Pipeline</h2>

<pre><code>
git add .
git commit -m "fix: update expired secret"
git push origin main
</code></pre>

<hr>

<h2>4️⃣ Verify Pipeline Success</h2>

<pre>
✔ Checkout Code
✔ Login to Docker
✔ Build Image
✔ Push Image

✅ Workflow Succeeded
</pre>

<hr>

<h2>🧠 What Fixed It?</h2>

<ul>
    <li>❌ <strong>Expired token:</strong> Authentication failed</li>
    <li>✅ <strong>New token generated:</strong> Access restored</li>
    <li>🔄 <strong>Secret updated:</strong> Pipeline uses valid credentials</li>
    <li>✅ <strong>Pipeline success:</strong> All steps executed</li>
</ul>

<pre><strong>Key Commands Used:</strong>
docker login                     ← Generate new token
gh secret set DOCKER_PASSWORD   ← Update secret
git push origin main            ← Trigger pipeline
gh run list                     ← View runs
gh run view --log               ← Debug logs</pre>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="debug-steps.md">🔍 Debug Steps</a> | 
  <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>