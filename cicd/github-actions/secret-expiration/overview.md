<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔴 Secret Expiration Issue</h1>

<p align="center">
    <img src="https://img.shields.io/badge/Status-Failed-ff4444?logo=githubactions&logoColor=white" alt="Secret Expired">
</p>

<hr>

<h3>🚨 Issue Summary</h3>
<p><strong>Issue:</strong> CI/CD pipeline fails due to expired or invalid secret/token</p>
<p><strong>Impact:</strong> Authentication fails, deployment blocked</p>

<hr>

<h2>📂 All Resources</h2>

<p><em>👆 Click below to explore the complete debugging journey</em></p>

<table border="1" cellpadding="12" cellspacing="0">
    <tr>
        <td><strong><a href="creation.md">📌 How I Created Issue</a></strong></td>
        <td><strong><a href="debug-steps.md">🔍 How I Debug It</a></strong></td>
    </tr>
    <tr>
        <td><strong><a href="fix.md">✅ How I Fixed It</a></strong></td>
    </tr>
</table>

<hr>

<h2>🚀 Quick Actions</h2>
<pre>
gh secret list
gh secret set MY_SECRET
gh run list
gh run view --log
</pre>

<hr>

<h2>⚠️ Common Errors</h2>
<pre>
Authentication failed
Invalid token
Token expired
403 Forbidden
</pre>

<hr>

<p align="center">
    <a href="../../../categories/cicd.md">← Back to CI/CD Issues</a> | 
    <a href="../../../README.md">🏠 Back to Main README</a>
</p>

</body>
</html>