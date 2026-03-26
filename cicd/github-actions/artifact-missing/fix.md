<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ Fix for Artifact Missing Issue</h1>

<hr>

<p><strong>Root Cause:</strong> Artifact upload step is missing in build stage</p>

<hr>

<h2>1️⃣ Enable Artifact Upload Step</h2>
<pre>Edit: .github/workflows/artifact-missing.yaml</pre>

<p>Go to the file and locate the commented section:</p>

<pre>
# - name: Upload Artifact
#   uses: actions/upload-artifact@v4
#   with:
#     name: app-build
#     path: dist/
</pre>

<p><strong>Fix:</strong> Uncomment this section using <code>command + /</code></p>

<pre>
- name: Upload Artifact
  uses: actions/upload-artifact@v4
  with:
    name: app-build
    path: dist/
</pre>

<hr>

<h2>3️⃣ Verify Artifact Name Consistency</h2>

<pre>
# Upload step
name: app-build

# Download step
name: app-build   ✔ must match exactly
</pre>

<p><strong>Issue:</strong> Name mismatch will cause failure ❌</p>

<hr>

<h2>4️⃣ Ensure Job Dependency</h2>

<pre>
deploy:
  needs: build
</pre>

<p><strong>Reason:</strong> Deploy must wait for build stage to complete</p>

<hr>

<h2>5️⃣ Re-run Pipeline</h2>

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
    <li><strong>Artifact upload step was missing</strong> in build stage ❌</li>
    <li><strong>Deploy stage expected artifact</strong></li>
    <li><strong>Pipeline failed due to missing artifact flow</strong></li>
</ul>

<hr>

<h2>🚀 Final Working Flow</h2>

<pre>
Build Stage → Upload Artifact → Deploy Stage → Download Artifact → Success ✔
</pre>

<hr>

<h2>🧠 Key Insight</h2>

<p>
Build stage success does NOT guarantee artifact availability.<br>
Artifacts must be explicitly uploaded to be used in later stages.
</p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Artifact Missing</a> | 
    <a href="../../categories/cicd.md">🏠 CI/CD Issues</a>
</p>

</body>
</html>