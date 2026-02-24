<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OOMKilled - Creation Steps</title>
</head>
<body>

<h1>📌 How I Created OOMKilled Issue</h1>

<hr>

<h2>1️⃣ Apply the YAML file</h2>

<pre><code>manifest % kubectl apply -f oom.yaml 
pod/oom-demo created</code></pre>

<h2>2️⃣ Watch Pod Status Change</h2>

<pre>manifest % kubectl get pods --watch</pre>

<p><strong>Output:</strong></p>

<pre>NAME       READY   STATUS      RESTARTS     AGE
oom-demo   0/1     OOMKilled   1 (4s ago)   6s
oom-demo   0/1     CrashLoopBackOff   1 (2s ago)   6s
oom-demo   0/1     OOMKilled          2 (16s ago)   20s
oom-demo   0/1     CrashLoopBackOff   2 (16s ago)   35s</pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>Pod starts with excessive memory request</strong> (no limits set)</li>
    <li><strong>Container consumes all node memory</strong> → Kernel kills process</li>
    <li><strong>OOMKilled:</strong> Out-Of-Memory kill by Linux kernel</li>
    <li><strong>CrashLoopBackOff:</strong> Kubernetes restarts → repeats cycle</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.html">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to OOMKilled</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
