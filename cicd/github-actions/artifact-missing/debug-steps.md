<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for Artifact Missing Issue</h1>

<hr>

<h2>1️⃣ Check Workflow Status</h2>
<pre>Go to GitHub → Actions → Select Workflow</pre>

<pre>
Artifact Missing Demo
❌ Failed
</pre>

<h2>2️⃣ Identify Failed Step</h2>
<p>Open the workflow run and expand steps.</p>

<pre>
✔ Checkout Code
✔ Build Application
❌ <strong>Download Artifact</strong>
</pre>

<h2>3️⃣ Check Error Logs</h2>
<pre>Click on failed step → View logs</pre>

<pre>
Run actions/download-artifact@v3
Error: Artifact not found for name: app-build
Error: Process completed with exit code 1.
</pre>

<h2>4️⃣ Verify Build Stage Output</h2>
<pre>Check build job logs</pre>

<pre>
✔ Build step executed
✔ Files created in dist/
❌ No artifact upload step found
</pre>

<p><strong>Observation:</strong> Artifact was never uploaded</p>

<h2>5️⃣ Validate Workflow Configuration</h2>
<pre>Check workflow file (.github/workflows/artifact-missing.yaml)</pre>

<pre>
# ❌ Missing this step

- name: Upload Artifact
  uses: actions/upload-artifact@v3
</pre>

<p><strong>Issue:</strong> Deploy stage expects artifact but build never uploaded it</p>

<h2>6️⃣ Check Artifact Name Consistency</h2>

<pre>
# Download step
name: app-build
</pre>

<p><strong>Check:</strong> Does upload step use same name?</p>

<pre>
❌ No matching upload step found
</pre>

<h2>7️⃣ Confirm Root Cause</h2>
<pre>
Error: Artifact not found
Meaning: Expected file was never created or uploaded
</pre>

<p><strong>🔍 Key Findings:</strong></p>
<ul>
    <li><strong>Artifact upload missing:</strong> No upload step in build stage</li>
    <li><strong>Download step failed:</strong> Artifact does not exist</li>
    <li><strong>Pipeline stopped:</strong> Deploy stage failed</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.md">✅ How to Fix →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Artifact Missing</a> | 
    <a href="../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>