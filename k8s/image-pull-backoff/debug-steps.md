<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ImagePullBackOff - Debug Steps</title>
</head>
<body>

<h1>🔍 Debug Steps for ImagePullBackOff</h1>

<hr>

<h2>1️⃣ Check Pod Status</h2>
<pre>kubectl describe pod imagepull-error-xxx</pre>

<h2>2️⃣ Check Events Section (First!)</h2>

<pre>Events:
  Type     Reason          Age                  From               Message
  ----     ------          ----                 ----               -------
  Normal   Scheduled       16h                  default-scheduler  Successfully assigned default/imagepull-error-7fc95d565f-m99s6 to cloudops-control-plane
  Normal   Pulling         16h (x5 over 16h)    kubelet            Pulling image "nginx:wrongtag"
  <strong>Warning  Failed     16h (x5 over 16h)    kubelet            Failed to pull image "nginx:wrongtag": rpc error: code = NotFound</strong>
  Warning  Failed          16h (x5 over 16h)    kubelet            Error: ErrImagePull
  Normal   BackOff         16h (x64 over 16h)   kubelet            Back-off pulling image "nginx:wrongtag"
  <strong>Warning  Failed     16h (x64 over 16h)   kubelet            Error: ImagePullBackOff</strong></pre>

<p><strong>🔍 Key Finding:</strong> <code>"nginx:wrongtag" not found</code> → <strong>Wrong image tag!</strong></p>

<h2>3️⃣ Check All Events</h2>
<pre>kubectl get events --sort-by=.metadata.creationTimestamp</pre>

<pre>6m37s     Warning   Failed      pod/imagepull-error-7fc95d565f-m99s6    Failed to pull image "nginx:wrongtag": rpc error: code = NotFound
4m30s     Normal    BackOff     pod/imagepull-error-7fc95d565f-m99s6    Back-off pulling image "nginx:wrongtag"
4m30s     Warning   Failed      pod/imagepull-error-7fc95d565f-m99s6    Error: ImagePullBackOff</pre>

<h2>🧠 What You Should Observe</h2>
<ul>
    <li><strong><code>Failed to pull image "nginx:wrongtag"</code></strong></li>
    <li><strong><code>rpc error: code = NotFound</code></strong></li>
    <li><strong><code>manifest unknown</code></strong></li>
</ul>

<p><strong>Root cause:</strong> Image tag <code>wrongtag</code> does not exist!</p>

<pre><strong>Look for these keywords:</strong>
- "Failed to pull image"
- "rpc error" 
- "manifest not found"
- "not found" 👈 This is key!</pre>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="fix.html">✅ How to Fix The Issue →</a></p>

<hr>

<p align="center">
    <a href="index.html">← Back to ImagePullBackOff</a> | 
    <a href="../../categories/k8s.html">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
