<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ How to Fix Pipeline Failure (npm install error)</h1>
<hr>

<h2>1️⃣ Fix: Add package.json</h2>

<pre>cicd/github-actions/pipeline-failure % npm init -y</pre>

<p><strong>This creates:</strong></p>

<pre>{
  "name": "pipeline-failure",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs"
}</pre>

<p><strong>Problem Before:</strong></p>
<pre>npm install
npm ERR! enoent ENOENT: no such file or directory, open 'package.json'</pre>

<p><strong>After Fix:</strong></p>
<pre>npm install
added 0 packages, and audited 1 package</pre>

<hr>

<h2>3️⃣ Commit and Push Fix</h2>

<pre>git add package.json
git commit -m "fix: add package.json"
git push origin main</pre>

<hr>

<h2>4️⃣ Verify Pipeline Success</h2>

<p>Go to <strong>GitHub → Actions</strong></p>

<pre>
✔ Checkout Code
✔ Setup Node
✔ Install Dependencies
✔ Run App

✅ <strong>Workflow Succeeded</strong>
</pre>

<hr>

<h2>🧠 What Fixed It?</h2>

<ul>
    <li>❌ <strong>Missing package.json:</strong> npm install failed (ENOENT error)</li>
    <li>✅ <strong>Added package.json:</strong> npm can now resolve dependencies</li>
    <li>⏳ <strong>Pipeline re-triggered:</strong> New commit triggered workflow</li>
    <li>✅ <strong>All steps passed:</strong> Build completed successfully</li>
</ul>

<pre><strong>Key Commands Used:</strong>
npm init -y                         ← Create package.json
git add package.json               ← Stage fix
git commit -m "fix: add package.json"
git push origin main               ← Trigger pipeline
gh run list                        ← View runs
gh run view --log                  ← Check logs</pre>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="debug-steps.md">🔍 Debug Steps</a> | 
  <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>