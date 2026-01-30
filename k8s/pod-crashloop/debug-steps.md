<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps</h1>

<hr>

<h2>1️⃣ Check Pod Status</h2>
<pre>kubectl describe pod crashloop-app-xxx</pre>

<h2>2️⃣ Check Events Section (First!)</h2>

<pre>Events:
  Type     Reason     Age                From               Message
  ----     ------     ----               ----               -------
  Normal   Scheduled  84s                default-scheduler  Successfully assigned default/crashloop-app-64fbb7f6bb-4x6l9 to aks-nodepool1-40559519-vmss000000
  Normal   Pulled     84s                kubelet            Successfully pulled image "busybox" in 163ms
  Normal   Pulled     78s                kubelet            Successfully pulled image "busybox" in 157ms
  Normal   Pulled     60s                kubelet            Successfully pulled image "busybox" in 150ms
  Normal   Pulling    28s (x4 over 84s)  kubelet            Pulling image "busybox"
  Normal   Created    28s (x4 over 84s)  kubelet            Created container: app
  Normal   Started    28s (x4 over 84s)  kubelet            Started container app
  <strong>Warning  BackOff    8s (x5 over 72s)   kubelet  Back off restarting failed container app</strong></pre>

<p><strong>🔍 Key Finding:</strong> Container <em>starts successfully</em> but then fails → Issue is inside container</p>

<h2>3️⃣ Check Container Section</h2>

<pre>Command:
      sh
      -c
      echo $DB_HOST && sleep 5
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       Completed
      Exit Code:    0
      Started:      Fri, 30 Jan 2026 18:11:50 +0530
      Finished:     Fri, 30 Jan 2026 18:11:55 +0530</pre>

<h2>4️⃣ Found the Real Issue: Missing Variable</h2>

<p><strong>💡 Analysis:</strong></p>
<ul>
    <li>Container command: <code>echo $DB_HOST && sleep 5</code></li>
    <li>Exit code: <code>0</code> (success)</li>
    <li>But <code>$DB_HOST</code> is <strong>empty/missing</strong></li>
    <li>Container exits immediately → Kubernetes restarts → CrashLoopBackOff</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p>
    <a href="fix.md">How to Fix The Issue →</a>
</p>

<hr>

<p align="center">
    <a href="../pod-crashloop/overview.md">← Back to Pod CrashLoopBackOff</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
