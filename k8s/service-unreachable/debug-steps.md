<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🔍 Debug Steps for Service Unreachable Issue</h1>

<hr>

<h2>1️⃣ Check Pod Status</h2>

<pre>kubectl get pods</pre>

<p><strong>Expected Output:</strong></p>

<pre>
NAME                            READY   STATUS    RESTARTS   AGE
nginx-deploy-xxxxxxx-abcde      1/1     Running   0          1m
</pre>

<p><strong>Observation:</strong> Pod is <code>Running</code>.</p>

<hr>

<h2>2️⃣ Check Service</h2>

<pre>kubectl get svc</pre>

<p><strong>Expected Output:</strong></p>

<pre>
NAME            TYPE        CLUSTER-IP      PORT(S)   AGE
nginx-service   ClusterIP   10.96.10.100    80/TCP    1m
</pre>

<p><strong>Observation:</strong> Service exists.</p>

<hr>

<h2>3️⃣ Check Endpoints (Very Important)</h2>

<pre>kubectl get endpoints nginx-service</pre>

<p><strong>If Output Shows:</strong></p>

<pre>
NAME            ENDPOINTS   AGE
nginx-service   &lt;none&gt;      1m
</pre>

<p><strong>🚨 Key Finding:</strong> No endpoints are attached to the Service.</p>

<p>
This means the Service is <strong>not linked to any Pod</strong>.
</p>

<hr>

<h2>4️⃣ Check Pod Labels</h2>

<pre>kubectl get pods --show-labels</pre>

<p><strong>Output:</strong></p>

<pre>
NAME                           READY   STATUS    RESTARTS   AGE   LABELS
nginx-deploy-xxxxxxx-abcde     1/1     Running   0          2m    app=nginx-app
</pre>

<p><strong>Observation:</strong> Pod label is <code>app=nginx-app</code>.</p>

<hr>

<h2>5️⃣ Check Service Selector</h2>

<pre>kubectl describe svc nginx-service</pre>

<p><strong>Selector Section:</strong></p>

<pre>
Selector:  app=wrong-label
</pre>

<p><strong>🚨 Root Cause Found:</strong> Label mismatch.</p>

<ul>
    <li>Pod Label → <code>app=nginx-app</code></li>
    <li>Service Selector → <code>app=wrong-label</code></li>
</ul>

<p>
Because of this mismatch, Kubernetes does not create endpoints.
</p>

<hr>

<h2>🧠 Root Cause Summary</h2>

<ul>
    <li>Service selector does not match Pod label</li>
    <li>No endpoints created</li>
    <li>Traffic cannot reach backend Pod</li>
</ul>

<hr>

<h2>➡️ Next Step</h2>

<p>Fix the selector so it matches the Pod label.</p>
<p><a href="fix.md">✅ Fix Guide →</a></p>

<hr>

<p align="center">
    <a href="creation.md">← Back to Creation</a> |
    <a href="overview.md">← Back to Service Unreachable</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>