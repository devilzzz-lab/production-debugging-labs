<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ Fix for Artifact Missing Issue</h1>

<hr>

<h2>1️⃣ Identify Missing Artifact Upload</h2>
<pre>Check build stage in workflow file</pre>

<pre>
✔ Build step exists
❌ Upload Artifact step missing
</pre>

<p><strong>Fix:</strong> Add artifact upload step</p>

<hr>

<h2>2️⃣ Add Upload Artifact Step</h2>
<pre>Edit: .github/workflows/artifact-missing.yaml</pre>

<pre>
- name: Upload Artifact
  uses: actions/upload-artifact@v3
  with:
    name: app-build
    path: dist/
</pre>

<hr>

<h2>3️⃣ Ensure Artifact Name Matches</h2>

<pre>
# Upload
name: app-build

# Download
name: app-build   ✔ must match exactly
</pre>

<p><strong>Issue:</strong> Name mismatch will cause failure ❌</p>

<hr>

<h2>4️⃣ Verify Artifact Path</h2>

<pre>
path: dist/
</pre>

<p><strong>Check:</strong></p>

<pre>
ls dist/
</pre>

<p><strong>Fix:</strong> Ensure files exist before upload</p>

<hr>

<h2>5️⃣ Validate Job Dependency</h2>

<pre>
deploy:
  needs: build
</pre>

<p><strong>Reason:</strong> Deploy must wait for build to complete</p>

<hr>

<h2>6️⃣ Re-run Pipeline</h2>

<pre>
git add .
git commit -m "fix artifact missing issue"
git push origin main
</pre>

<hr>

<h2>🔍 Expected Result</h2>

<pre>
✔ Build stage uploads artifact
✔ Deploy stage downloads artifact
✔ Pipeline runs successfully
</pre>

<hr>

<h2>🎯 Root Cause Summary</h2>

<ul>
    <li><strong>Artifact not uploaded</strong> in build stage ❌</li>
    <li><strong>Deploy stage expected artifact</strong></li>
    <li><strong>Mismatch caused failure</strong></li>
</ul>

<hr>

<h2>🚀 Final Working Flow</h2>

<pre>
Build Stage → Upload Artifact → Deploy Stage → Download Artifact → Success ✔
</pre>


<hr>

<p align="center">
    <a href="overview.md">← Back to Artifact Missing</a> | 
    <a href="../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>