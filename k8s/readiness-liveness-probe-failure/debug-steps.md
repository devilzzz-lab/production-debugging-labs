<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for Readiness & Liveness Probe Failure</h1>

<hr>

<h2>1️⃣ Check Pod Status</h2>

<pre>kubectl get pods</pre>

<p><strong>Example Output:</strong></p>

<pre>
NAME                                READY   STATUS    RESTARTS   AGE
nginx-probe-test-768d578c6b-nn99j   0/1     Running   2 (4s ago)   54s
nginx-probe-test-768d578c6b-nn99j   0/1     Running   3 (3s ago)   78s
</pre>

<p><strong>Observation:</strong></p>

<ul>
<li>Pod is <code>Running</code></li>
<li>But <code>READY = 0/1</code></li>
<li>Restart count keeps increasing</li>
</ul>

<hr>

<h2>2️⃣ Describe the Pod (Most Important Step)</h2>

<pre>kubectl describe pod nginx-probe-test-xxxx</pre>

<p><strong>Events Section:</strong></p>

<pre>
Events:
  Type     Reason     Age                 From     Message
  ----     ------     ----                ----     -------
  Normal   Pulled     4m15s                   kubelet            Successfully pulled image "nginx" in 2.953s (2.953s including waiting). Image size: 61269871 bytes.
  Warning  Unhealthy  3m53s (x9 over 4m53s)   kubelet            Liveness probe failed: Get "http://10.244.0.20:9999/": dial tcp 10.244.0.20:9999: connect: connection refused
  Normal   Pulled     3m51s                   kubelet            Successfully pulled image "nginx" in 2.154s (2.154s including waiting). Image size: 61269871 bytes.
  Warning  Unhealthy  3m39s (x16 over 4m59s)  kubelet            Readiness probe failed: HTTP probe failed with statuscode: 404
</pre>

<p><strong>Key Findings:</strong></p>

<ul>
<li>Readiness probe returned <code>404</code></li>
<li>Liveness probe cannot connect to port <code>9999</code></li>
</ul>

<hr>

<h2>3️⃣ Check Pod Logs</h2>

<pre>kubectl logs nginx-probe-test-xxxx</pre>

<p><strong>Observation:</strong></p>

<p>
Logs show normal nginx startup with no application error.
This confirms the issue is related to probe configuration, not the container itself.
</p>

<hr>

<h2>4️⃣ Verify Container Port</h2>

<pre>kubectl describe pod nginx-probe-test-xxxx | grep Port</pre>

<p><strong>Output:</strong></p>

<pre>
Port: 80/TCP
Host Port: 0/TCP
</pre>

<p>
But the liveness probe is checking port <code>9999</code>, which does not exist.
</p>

<hr>

<h2>🧠 Root Cause</h2>

<ul>
<li>Readiness probe uses incorrect path <code>/healthz</code></li>
<li>Liveness probe checks incorrect port <code>9999</code></li>
<li>Kubelet marks container unhealthy</li>
<li>Container gets restarted repeatedly</li>
</ul>

<hr>

<h2>🔎 Important Indicators</h2>

<pre>
Look for keywords in describe output:

- Readiness probe failed
- Liveness probe failed
- connection refused
- HTTP probe failed
</pre>

<hr>

<h2>➡️ Next Step</h2>

<p>Fix the probe configuration to match the actual container behavior.</p>

<p><a href="fix.md">✅ Fix Guide →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Probe Failure</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>