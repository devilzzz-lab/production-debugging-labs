<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">✅ How I Fixed Readiness & Liveness Probe Failure</h1>

<hr>

<h2>📌 Scenario</h2>

<p>
The Pod was running but failing health checks because the probe configuration was incorrect.
</p>

<ul>
<li>Readiness probe used wrong path <code>/healthz</code></li>
<li>Liveness probe checked incorrect port <code>9999</code></li>
<li>Kubernetes marked the container unhealthy</li>
<li>Pod never became <code>Ready</code> and kept restarting</li>
</ul>

<hr>

<h2>🛠️ Fix: Correct the Probe Configuration</h2>

<h3>1️⃣ Update Deployment YAML</h3>

<pre><code>apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-probe-test
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-probe
  template:
    metadata:
      labels:
        app: nginx-probe
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80

        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 5
          periodSeconds: 5

        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 10
          periodSeconds: 5
</code></pre>

<hr>

<h3>2️⃣ Apply the Updated Manifest</h3>

<pre><code>kubectl apply -f deployment.yaml</code></pre>

<hr>

<h3>3️⃣ Verify Pod Status</h3>

<pre><code>kubectl get pods</code></pre>

<p><strong>Expected Output:</strong></p>

<pre>
NAME                                READY   STATUS    RESTARTS   AGE
nginx-probe-test-6c8f9b7c8f-xyz12   1/1     Running   0          40s
</pre>

<p>✅ Pod is now healthy and fully ready.</p>

<hr>

<h2>🧠 What Happened Internally?</h2>

<ul>
<li>Readiness probe started returning <code>200 OK</code></li>
<li>Kubernetes marked the Pod as <strong>Ready</strong></li>
<li>Service began routing traffic to the Pod</li>
<li>Liveness probe succeeded and container restarts stopped</li>
</ul>

<hr>

<h2>⚠️ Common Mistakes</h2>

<ul>
<li>Using incorrect health check paths</li>
<li>Checking wrong container ports</li>
<li>Setting probes before application starts</li>
<li>Confusing readiness with liveness probes</li>
</ul>

<hr>

<h2>🚀 Final Result</h2>

<p>
✔ Pod moved from <strong>0/1 → 1/1 READY</strong><br>
✔ Container restarts stopped<br>
✔ Health checks passed successfully<br>
✔ Application became accessible
</p>

<hr>

<p align="center">
    <a href="debug-steps.md">← Debug Steps</a> | 
    <a href="overview.md">← Back to Probe Failure</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>