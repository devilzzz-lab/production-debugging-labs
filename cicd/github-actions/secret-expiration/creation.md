<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">📌 How I Created Secret Expiration Issue (Expired Token)</h1>

<hr>

<h2>1️⃣ Use Expired / Invalid Token</h2>

<p><strong>Example: Docker Login using expired token</strong></p>

<pre><code>
docker login -u username -p expired_token
</code></pre>

<p><strong>OR GitHub PAT:</strong></p>

<pre><code>
export GH_TOKEN=expired_token
</code></pre>

<hr>

<h2>2️⃣ Add Secret to GitHub</h2>

<p>Go to <strong>GitHub → Settings → Secrets → Actions</strong></p>

<p>Add:</p>

<pre><code>
DOCKER_PASSWORD = expired_token
</code></pre>

<hr>

<h2>3️⃣ Use Secret in Workflow</h2>

<pre><code>
- name: Login to Docker
  run: docker login -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
</code></pre>

<hr>

<h2>4️⃣ Trigger Pipeline</h2>

<pre><code>
git add .
git commit -m "trigger secret expiration issue"
git push origin main
</code></pre>

<hr>

<h2>🔍 What's Happening?</h2>

<ul>
    <li><strong>Pipeline starts successfully</strong></li>
    <li><strong>Authentication step executes</strong></li>
    <li><strong>Token is invalid/expired</strong> ❌</li>
    <li><strong>Login fails</strong> → Pipeline fails</li>
</ul>

<hr>

<h2>⚠️ Expected Errors</h2>

<pre><code>
Error response from daemon: unauthorized: incorrect username or password
authentication failed
denied: access forbidden
</code></pre>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Secret Expiration</a> | 
    <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>