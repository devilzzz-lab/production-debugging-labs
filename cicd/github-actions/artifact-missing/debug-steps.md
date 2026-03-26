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
<pre>Go to GitHub → Actions → Select Artifact Missing Demo Workflow</pre>

<pre>
Latest Run:
trigger artifact missing issue
❌ Failed
</pre>

<hr>

<h2>2️⃣ Identify Failed Job</h2>
<p>Open the workflow run.</p>

<pre>
✔ build job → SUCCESS
❌ deploy job → FAILED
</pre>

<p><strong>🧠 Important Insight:</strong> Pipeline does not fail in build stage.  
Failure happens only in deploy stage.</p>

<hr>

<h2>3️⃣ Identify Failed Step</h2>
<p>Expand the <strong>deploy job</strong></p>

<pre>
✔ Set up job
❌ <strong>Download Artifact</strong>
</pre>

<hr>

<h2>4️⃣ Check Error Logs</h2>
<pre>Click on failed step → View logs</pre>

<pre>
Run actions/download-artifact@v4
Downloading single artifact
Error: Unable to download artifact(s): Artifact not found for name: app-build
Please ensure that your artifact is not expired and the artifact was uploaded using a compatible version.
Error: Process completed with exit code 1.
</pre>

<p><strong>Observation:</strong> Deploy stage is trying to download an artifact that does not exist</p>

<hr>

<h2>5️⃣ Verify Build Stage Output</h2>
<pre>Go to build job → Check logs</pre>

<pre>
✔ Build step executed
✔ Files created in dist/
❌ No artifact upload step found
</pre>

<p><strong>🧠 Important Insight:</strong>  
Build stage is successful, but success does NOT mean artifact is available.</p>

<hr>

<h2>6️⃣ Validate Workflow Configuration</h2>
<pre>Check workflow file (.github/workflows/artifact-missing.yaml)</pre>

<pre>
# ❌ Missing this step

- name: Upload Artifact
  uses: actions/upload-artifact@v4
  with:
    name: app-build
    path: dist/
</pre>

<p><strong>Issue:</strong> Build stage never uploads artifact</p>

<hr>

<h2>7️⃣ Check Artifact Name Consistency</h2>

<pre>
# Deploy step expects
name: app-build
</pre>

<p><strong>Check:</strong> Is same name used in upload step?</p>

<pre>
❌ No upload step → No artifact exists
</pre>

<hr>

<h2>8️⃣ Confirm Root Cause</h2>
<pre>
Error: Artifact not found
Meaning: Expected artifact was never uploaded
</pre>

<p><strong>🔍 Key Findings:</strong></p>
<ul>
    <li><strong>Build succeeded:</strong> But no artifact uploaded ❌</li>
    <li><strong>Deploy failed:</strong> Artifact not found ❌</li>
    <li><strong>Pipeline broke:</strong> Due to missing artifact flow ❌</li>
</ul>

<hr>

<h2>🎯 Final Understanding</h2>

<pre>
Build Stage → (No Upload) → Deploy Stage → Download Fails ❌
</pre>

<p><strong>🧠 Key Insight:</strong>  
Pipeline success in one stage does not guarantee data availability in next stage.</p>

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