<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CrashLoopBackOff - Creation Steps</title>
</head>
<body>

<h1>📌 How I Created CrashLoopBackOff Issue</h1>

<hr>

<h2>🚀 Deploy CrashLoop App</h2>

<pre>cd k8s/pod-crashloop/manifest
kubectl apply -f crashloop.yaml
deployment.apps/crashloop-app created</pre>

<h2>⏳ Wait 10sec & Watch:</h2>
<pre>kubectl get pods --watch
NAME                             READY   STATUS    RESTARTS      AGE
crashloop-app-64fbb7f6bb-r4svl   1/1     Running   2 (17s ago)   29s
crashloop-app-64fbb7f6bb-r4svl   0/1     Completed   2 (17s ago)   29s
crashloop-app-64fbb7f6bb-r4svl   0/1     CrashLoopBackOff   2 (14s ago)   43s
crashloop-app-64fbb7f6bb-r4svl   1/1     Running            3 (27s ago)   56s
crashloop-app-64fbb7f6bb-r4svl   0/1     Completed          3 (32s ago)   61s
crashloop-app-64fbb7f6bb-r4svl   0/1     CrashLoopBackOff   3 (16s ago)   77s</pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>Running:</strong> Container starts successfully</li>
    <li><strong>Completed:</strong> Container exits (Exit Code: 0)</li>
    <li><strong>CrashLoopBackOff:</strong> Kubernetes restarts with increasing backoff delays</li>
    <li><strong>Cycle continues:</strong> Running → Completed → CrashLoopBackOff → repeat</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.html">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="index.html">← Back to Pod CrashLoopBackOff</a> | 
    <a href="../../categories/k8s.html">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
