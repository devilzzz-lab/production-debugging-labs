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

<pre><code>.github/workflows/ci-cd.yaml</code></pre>

<pre><code>name: CI Pipeline Failure Demo

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install Dependencies
        run: npm install

      - name: Run App
        run: node index.js
</code></pre>

<hr>

<h2>2️⃣ Create Application WITHOUT package.json</h2>

<pre><code>index.js</code></pre>

<pre><code>console.log("CI/CD Demo");</code></pre>

<p><strong>Important:</strong> Do NOT create <code>package.json</code></p>

<hr>

<h2>3️⃣ Push Code to GitHub</h2>

<pre><code>git add .
git commit -m "trigger pipeline failure"
git push origin main</code></pre>

<hr>

<h2>4️⃣ Observe Pipeline Failure</h2>

<p>Go to <strong>GitHub → Actions</strong> and open the workflow run.</p>

<p><strong>Output:</strong></p>

<pre>Run npm install
npm ERR! code ENOENT
npm ERR! syscall open
npm ERR! path /home/runner/work/.../package.json
npm ERR! enoent ENOENT: no such file or directory, open 'package.json'
npm ERR! enoent This is related to npm not being able to find a file</pre>

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