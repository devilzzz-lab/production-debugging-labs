<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🛠 How I Created Readiness & Liveness Probe Failure</h1>

<hr>

<h2>1️⃣ Create a Deployment with Incorrect Probes</h2>


<pre><code>manifest % kubectl apply -f deployment.yaml</code></pre>

<p><strong>Output:</strong></p>

<pre>
deployment.apps/nginx-probe-test created
</pre>

<hr>

<h2>2️⃣ Check Pod Status</h2>

<pre><code>kubectl get pods</code></pre>

<p><strong>Example Output:</strong></p>

<pre>
NAME                                READY   STATUS    RESTARTS   AGE
nginx-probe-test-768d578c6b-nn99j   0/1     Running   0          6s
nginx-probe-test-768d578c6b-nn99j   0/1     Running   1 (3s ago)   28s
nginx-probe-test-768d578c6b-nn99j   0/1     Running   2 (4s ago)   54s

</pre>

<p>
<strong>Observation:</strong>
</p>

<ul>
<li>Pod is running</li>
<li>But <code>READY = 0/1</code></li>
<li>Restart count is increasing</li>
</ul>

<hr>

<h2>➡️ Next Step</h2>

<p>Investigate why probes are failing using Kubernetes debugging commands.</p>

<p><a href="debug-steps.md">🔍 Continue Debugging →</a></p>

<hr>

<p align="center">
<a href="overview.md">← Back to Probe Failure</a> | 
<a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>