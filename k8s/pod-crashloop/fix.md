<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>✅ How to Fix CrashLoopBackOff</h1>

<hr>

<h2>1️⃣ Comment Out Error YAML and Apply Fixed YAML</h2>

<pre>sujithg@Sujiths-MacBook-Pro manifest % kubectl apply -f crashloop.yaml
deployment.apps/crashloop-app created</pre>

<h2>2️⃣ Check Rollout Status</h2>
<pre>kubectl rollout status deployment/crashloop-app
Waiting for deployment "crashloop-app" rollout to finish: 0 of 1 updated replicas are available...
deployment "crashloop-app" successfully rolled out</pre>

<h2>3️⃣ Verify Fix</h2>
<pre>kubectl logs deployment/crashloop-app
<strong>postgres-service</strong></pre>

<pre>kubectl get pods --watch
NAME                             READY   STATUS    RESTARTS   AGE
crashloop-app-566b9c79d4-6rz2j   1/1     Running   0          15s</pre>

<hr>

<h2>🤔 Why sleep 5 vs sleep 3600?</h2>

<p><strong>BY DESIGN:</strong></p>

<pre>command: ["sh", "-c", "echo $DB_HOST && sleep 5"]</pre>

<h3>Flow:</h3>
<ul>
    <li>✅ <code>echo $DB_HOST</code> → prints <code>postgres-service</code></li>
    <li>✅ <code>sleep 5</code> → waits 5 seconds</li>
    <li>✅ Container exits normally (Exit Code: 0)</li>
    <li>🔄 Kubernetes restarts → CrashLoopBackOff → repeat</li>
</ul>

<h3>Key Observations:</h3>
<pre>deployment "crashloop-app" successfully rolled out  ← Deployment healthy
kubectl logs → postgres-service                   ← ENV VAR working!</pre>

<hr>

<h2>🎯 Lab Learning Points</h2>

<table border="1" cellpadding="8">
    <tr>
        <td><strong>❌ ERROR State:</strong></td>
        <td>Missing <code>DB_HOST</code> → empty logs → CrashLoopBackOff</td>
    </tr>
    <tr>
        <td><strong>✅ FIXED State:</strong></td>
        <td>Add env var → <code>postgres-service</code> in logs → CrashLoop continues (normal)</td>
    </tr>
</table>

<h3>Optional: Stable Running Pods</h3>
<pre>command: ["sh", "-c", "echo $DB_HOST && sleep 3600"]  
# Sleep 1hr = won't restart (for re-checking/debugging)</pre>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="debug-steps.md">🔍 Debug Steps</a> | 
  <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
