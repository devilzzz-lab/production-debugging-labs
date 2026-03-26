<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">📌 How I Created Artifact Missing Issue</h1>

<hr>

<h2>1️⃣ Remove Artifact Upload Step</h2>

<p><strong>Edit:</strong> <code>.github/workflows/artifact-missing.yaml</code></p>

<pre><code># ❌ Remove or comment this section

- name: Upload Artifact
  uses: actions/upload-artifact@v3
  with:
    name: app-build
    path: dist/
</code></pre>

<hr>

<h2>2️⃣ Keep Download Step in Deploy Stage</h2>

<pre><code>- name: Download Artifact
  uses: actions/download-artifact@v3
  with:
    name: app-build   # ❌ This artifact will not exist
</code></pre>

<hr>

<h2>3️⃣ Trigger Pipeline</h2>

<pre><code>git add .
git commit -m "trigger artifact missing issue"
git push origin main</code></pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>Pipeline triggers successfully</strong></li>
    <li><strong>Build stage runs</strong></li>
    <li><strong>No artifact is uploaded</strong> ❌</li>
    <li><strong>Deploy stage tries to download artifact</strong></li>
    <li><strong>Artifact not found error</strong> → Pipeline fails</li>
</ul>

<hr>

<h2>💥 Expected Error</h2>

<pre><code>Artifact not found for name: app-build
</code></pre>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Artifact Missing</a> | 
    <a href="../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>