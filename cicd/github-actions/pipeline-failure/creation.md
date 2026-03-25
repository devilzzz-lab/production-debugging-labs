<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">📌 How I Created Pipeline Failure (npm install error)</h1>

<hr>

<h2>1️⃣ Comment Out GitHub Actions Workflow File</h2>

<p><strong>Edit:</strong> <code>.github/workflows/pipeline-failure.yaml</code></p>

<pre><code>command + A
</code></pre>

<pre><code>command + /
</code></pre>

<hr>

<h2>2️⃣ Trigger Pipeline</h2>

<pre><code>git add .
git commit -m "trigger pipeline failure - missing npm install"
git push origin main</code></pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>Pipeline triggers successfully</strong></li>
    <li><strong>npm install step executes</strong></li>
    <li><strong>package.json missing</strong> ❌</li>
    <li><strong>Exit code 254</strong> → Pipeline fails</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Pipeline Failure</a> | 
    <a href="../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>
