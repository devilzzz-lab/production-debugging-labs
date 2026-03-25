<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>📌 How I Created Pipeline Failure (npm install error)</h1>

<hr>

<h2>1️⃣ Create GitHub Actions Workflow</h2>

<pre><code>.github/workflows/pipeline-failure.yaml</code></pre>

<hr>

<h2>2️⃣ Create Application WITHOUT package.json</h2>

<pre><code>cicd/pipeline-failure/index.js</code></pre>

<pre><code>console.log("CI/CD Demo");</code></pre>

<p><strong>Important:</strong> Do NOT create <code>package.json</code></p>

<hr>

<h2>3️⃣ Push Code to GitHub</h2>

<pre><code>git add .
git commit -m "trigger pipeline failure"
git push main</code></pre>

<hr>

<h2>4️⃣ Observe Pipeline Failure</h2>

<p>Go to <strong>GitHub → Actions</strong> and open the workflow run.</p>

<p><strong>Output:</strong></p>

<pre>Run npm install
npm install
shell: /usr/bin/bash -e {0}
npm error code ENOENT
npm error syscall open
npm error path /home/runner/work/production-debugging-labs/production-debugging-labs/package.json
npm error errno -2
npm error enoent Could not read package.json: Error: ENOENT: no such file or directory, open '/home/runner/work/production-debugging-labs/production-debugging-labs/package.json'
npm error enoent This is related to npm not being able to find a file.
npm error enoent
npm error A complete log of this run can be found in: /home/runner/.npm/_logs/2026-03-25T07_14_15_452Z-debug-0.log
Error: Process completed with exit code 254.</pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>Pipeline runs npm install</strong></li>
    <li><strong>package.json is missing</strong></li>
    <li><strong>npm cannot install dependencies</strong></li>
    <li><strong>Pipeline fails immediately</strong></li>
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