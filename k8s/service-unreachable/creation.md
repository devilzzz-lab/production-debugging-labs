<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🛠 How I Created Service Unreachable Issue</h1>

<hr>

<h2>1️⃣ Create Deployment</h2>

<pre><code>manifest % kubectl apply -f deployment.yaml</code></pre>

<p><strong>deployment.apps/nginx-deploy created</strong></p>

<hr>

<h2>2️⃣ Create Service (With Wrong Selector)</h2>

<pre><code>manifest % kubectl apply -f service.yaml</code></pre>

<p><strong>service/nginx-service created</strong></p>

<hr>

<h2>3️⃣ Test the Service</h2>

<pre><code>manifest % kubectl run test --rm -it --image=busybox -- sh</code></pre>

<p><strong>Inside the Pod:</strong></p>

<pre><code>wget -qO- nginx-service</code></pre>

<p><strong>Result:</strong></p>

<pre>
wget: bad address 'nginx-service'
</pre>

<hr>

<h2>🔍 What Is Happening?</h2>

<ul>
    <li>✅ Deployment created successfully</li>
    <li>✅ Pod is running</li>
    <li>✅ Service is created</li>
    <li>❌ Service is not routing traffic to Pod</li>
</ul>

<hr>

<h2>🚨 Why It Fails?</h2>

<ul>
    <li>Service selector does not match Pod labels</li>
    <li>No endpoints are created for the Service</li>
    <li>Traffic cannot reach backend Pod</li>
</ul>

<hr>

<h2>➡️ Next Step</h2>

<p>Debug the Service to identify why endpoints are missing.</p>
<p><a href="debug-steps.md">🔍 Continue Debugging →</a></p>

<hr>

<p align="center">
    <a href="overview.md">← Back to Service Unreachable</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>