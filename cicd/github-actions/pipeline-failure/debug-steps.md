<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for Pipeline Failure</h1>

<hr>

<h2>1️⃣ Check Workflow Status</h2>
<pre>Go to GitHub → Actions → Select Workflow</pre>

<pre>
CI Pipeline Failure Demo
❌ Failed
</pre>

<h2>2️⃣ Identify Failed Step</h2>
<p>Open the workflow run and expand steps.</p>

<pre>
✔ Checkout Code
✔ Setup Node
❌ <strong>Install Dependencies</strong>
</pre>

<h2>3️⃣ Check Error Logs</h2>
<pre>Click on failed step → View logs</pre>

<pre>
Run npm install
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
Error: Process completed with exit code 254.
</pre>

<h2>4️⃣ Verify Repository Structure</h2>
<pre>Check project files in repository</pre>

<pre>
├── cicd
│   └── github-actions
│       └── pipeline-failure
│            └── index.js
</pre>

<p><strong>Observation:</strong> <code>package.json</code> is missing</p>

<h2>5️⃣ Validate Pipeline Configuration</h2>
<pre>Check workflow file (.github/workflows/pipeline-failure.yaml)</pre>

<pre>
- name: Install Dependencies
  run: npm install
</pre>

<p><strong>Issue:</strong> <code>npm install</code> requires <code>package.json</code></p>

<h2>6️⃣ Confirm Root Cause</h2>
<pre>
Error: ENOENT (Error NO ENTry)
Meaning: Required file does not exist
</pre>

<p><strong>🔍 Key Findings:</strong></p>
<ul>
    <li><strong>npm install failed:</strong> Missing <code>package.json</code></li>
    <li><strong>Pipeline stopped:</strong> Dependency installation step failed</li>
    <li><strong>Build not completed:</strong> Subsequent steps skipped</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.md">✅ How to Fix →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Pipeline Failure</a> | 
    <a href="../../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>