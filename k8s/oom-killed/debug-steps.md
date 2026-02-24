<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for OOMKilled</h1>

<hr>

<h2>1️⃣ Check Pod Status</h2>
<pre>kubectl get pods</pre>

<pre>NAME       READY   STATUS      RESTARTS     AGE
oom-demo   0/1     <strong>OOMKilled</strong>   1 (4s ago)   6s
oom-demo   0/1     CrashLoopBackOff   1 (2s ago)   6s</pre>

<h2>2️⃣ Check Pod Describe</h2>
<pre>kubectl describe pod oom-demo</pre>

<pre>Last State:     Terminated
  <strong>Reason:       OOMKilled
  Exit Code:    137</strong></pre>

<h2>3️⃣ Check Events</h2>
<pre>kubectl get events --sort-by=.metadata.creationTimestamp | grep oom-demo</pre>

<pre>Warning  BackOff         5m22s  kubelet  Back-off restarting failed container memory-hog</pre>

<h2>4️⃣ Check Resource Configuration</h2>
<pre>kubectl describe pod oom-demo | grep -A5 -B5 "Limits\|Requests"</pre>

<pre>Resources:
  Limits:
    <strong>memory: 50Mi</strong>
  Requests:
    memory: 25Mi</pre>

<h2>5️⃣ Confirm OOMKilled</h2>
<pre>kubectl get pod oom-demo -o jsonpath='{.status.containerStatuses[0].lastState.terminated.reason}'</pre>

<pre><strong>OOMKilled</strong></pre>

<p><strong>🔍 Key Findings:</strong></p>
<ul>
    <li><strong>Exit Code 137:</strong> = 128 (SIGKILL) + 9 → Linux OOM Killer</li>
    <li><strong>50Mi memory limit:</strong> Too low for stress container workload</li>
    <li><strong>CrashLoopBackOff:</strong> Kubernetes restart cycle</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.html">✅ How to Fix →</a></p>

<hr>

<p align="center">
    <a href="index.html">← Back to OOMKilled</a> | 
    <a href="../../categories/k8s.html">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
