<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔴 Runner / Agent Down</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-Offline-ff4444?logo=githubactions&logoColor=white" alt="Runner Down">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> CI/CD pipeline is stuck because no runner/agent is available to execute jobs</p>
<p><strong>Impact:</strong> Jobs remain in queue, builds do not start, deployment is blocked</p>

<hr>

<h2>📂 All Resources</h2>

<p><em>👆 Click below to explore the complete debugging journey</em></p>

<table border="1" cellpadding="12" cellspacing="0">
    <tr>
        <td>
            <strong><a href="creation.md">📌 How I Created Issue</a></strong>
        </td>
        <td>
            <strong><a href="debug-steps.md">🔍 How I Debug It</a></strong>
        </td>
    </tr>
    <tr>
        <td>
            <strong><a href="fix.md">✅ How I Fixed It</a></strong>
        </td>
    </tr>
</table>

<hr>

<h2>🚀 Quick Actions</h2>
<pre>
# Check runners
gh api repos/{owner}/{repo}/actions/runners

# View workflow runs
gh run list

# Inspect run
gh run view &lt;run-id&gt;

# View logs
gh run view --log

# Re-run pipeline
gh run rerun &lt;run-id&gt;
</pre>

<hr>

<h2>⚠️ Common Errors</h2>
<pre>
No runner available
Runner is offline
Waiting for a runner to pick up this job
Job stuck in queue
</pre>

<hr>

<p align="center">
    <a href="../../../categories/cicd.md">← Back to CI/CD Issues</a> | 
    <a href="../../../README.md">🏠 Back to Main README</a>
</p>

</body>
</html>