<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">✅ How I Fixed Service Unreachable Issue</h1>

<hr>

<h2>📌 Scenario</h2>
<p>
Service was created successfully, and the Pod was running.
However, the Service was <strong>not reachable</strong> because
its selector did not match the Pod label.
</p>

<hr>

<h2>🛠️ Fix: Correct the Service Selector</h2>

<h3>1️⃣ Edit the Service</h3>

<pre><code>kubectl edit svc nginx-service</code></pre>

<p><strong>Change this:</strong></p>

<pre>
selector:
  app: wrong-label
</pre>

<p><strong>To this:</strong></p>

<pre>
selector:
  app: nginx-app
</pre>

<hr>

<h3>2️⃣ Verify Endpoints</h3>

<pre><code>kubectl get endpoints nginx-service</code></pre>

<p><strong>Expected Output:</strong></p>

<pre>
NAME            ENDPOINTS          AGE
nginx-service   10.244.0.5:80      2m
</pre>

<p>✅ Endpoints are now created successfully.</p>

<hr>

<h3>3️⃣ Test the Service Again</h3>

<pre><code>kubectl run test --rm -it --image=busybox -- sh</code></pre>

<p><strong>Inside the Pod:</strong></p>

<pre><code>wget -qO- nginx-service</code></pre>

<p><strong>Expected Result:</strong></p>

<pre>
&lt;html&gt;
&lt;head&gt;&lt;title&gt;Welcome to nginx!&lt;/title&gt;&lt;/head&gt;
&lt;body&gt;
&lt;h1&gt;Welcome to nginx!&lt;/h1&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

<p>✅ Service is now routing traffic to the Pod successfully.</p>

<hr>

<h2>🧠 What Happened Internally?</h2>
<ul>
    <li>Kubernetes matched Service selector with Pod label</li>
    <li>Endpoint object was automatically created</li>
    <li>Service started routing traffic to Pod IP</li>
    <li>Internal DNS resolution worked correctly</li>
</ul>

<hr>

<h2>⚠️ Common Mistakes</h2>
<ul>
    <li>Ignoring <code>kubectl get endpoints</code></li>
    <li>Not verifying Pod labels</li>
    <li>Assuming Service creation means connectivity</li>
    <li>Forgetting that Service works purely on label matching</li>
</ul>

<hr>

<h2>🚀 Final Result</h2>

<p>
✔ Endpoints created successfully<br>
✔ Service now linked to backend Pod<br>
✔ Traffic routed properly<br>
✔ Issue resolved by fixing selector mismatch
</p>

<hr>

<p align="center">
    <a href="debug-steps.md">← Debug Steps</a>
    <a href="overview.md">← Back to Service Unreachable</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>