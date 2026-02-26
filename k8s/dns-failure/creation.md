<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>📌 How I Created OOMKilled Issue</h1>

<hr>

<h2>1️⃣ Apply the YAML file</h2>

<pre><code>manifest % kubectl apply -f .
pod/nginx-test created 
pod/dns-failure created
</code></pre>


<h2>2️⃣ Watch Pod Status Change</h2>

<pre>manifest % kubectl get pods --watch</pre>

<p><strong>Output:</strong></p>

<pre>NAME       READY   STATUS      RESTARTS     AGE
dns-failure   1/1     Running   0             12m
dns-test      1/1     Running   0             19m
nginx-test    1/1     Running   1 (23m ago)   16h</pre>
<hr>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to OOMKilled</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
