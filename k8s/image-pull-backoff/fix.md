<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ImagePullBackOff - How to Fix</title>
</head>
<body>

<h1>✅ How to Fix ImagePullBackOff</h1>

<hr>

<h2>1️⃣ STEP 1: Edit Deployment</h2>

<pre>sujithg@Sujiths-MacBook-Pro manifest % kubectl edit deployment imagepull-error</pre>

<p><strong>Change this:</strong></p>
<pre>image: nginx:wrongtag</pre>

<p><strong>To this:</strong></p>
<pre>image: nginx:latest</pre>

<p><strong>Save & exit → deployment updates automatically</strong></p>

<h2>2️⃣ Check Rollout Status</h2>
<pre>kubectl rollout status deployment/imagepull-error
Waiting for deployment "imagepull-error" rollout to finish: 0 of 1 updated replicas are available...
deployment "imagepull-error" successfully rolled out</pre>

<h2>3️⃣ Verify Fix</h2>

<pre>kubectl get pods --watch
NAME                               READY   STATUS    RESTARTS   AGE
imagepull-error-5ff487869f-jmhrp   1/1     Running   0          15s</pre>

<pre>kubectl logs deployment/imagepull-error
# Container running successfully ✅</pre>

<hr>

<h2>🎯 What Fixed It?</h2>
<ul>
    <li>❌ <code>nginx:wrongtag</code> → Image doesn't exist</li>
    <li>✅ <code>nginx:latest</code> → Valid image available</li>
    <li>Kubernetes pulled new image → Pod running ✅</li>
</ul>

<hr>

<p align="center">
    <a href="index.html">← Back to ImagePullBackOff</a> | 
    <a href="../../categories/k8s.html">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
