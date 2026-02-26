<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">🔍 Debug Steps - DNS Failure</h1>

<hr>

<h2>1️⃣ Verify DNS Resolution Inside Pod</h2>
<pre><code>kubectl run dns-test --image=busybox -it --rm -- sh</code></pre>

<p>Enter pod terminal (all commands logged to container logs):</p>
<pre><code>/ # nslookup nginx-service</code></pre>

<h3>✅ Expected Output (Working DNS):</h3>
<pre><code>Server:    10.96.0.10
Address:  10.96.0.10:53

Name:      nginx-service.default.svc.cluster.local
Address:  10.96.235.145</code></pre>

<h3>❌ Problem Output (DNS Broken):</h3>
<pre><code>Server:    8.8.8.8
Address:  8.8.8.8:53

** server can't find nginx-service: NXDOMAIN</code></pre>

<hr>

<h2>2️⃣ Check Pod's DNS Configuration</h2>
<pre><code>/ # cat /etc/resolv.conf</code></pre>

<h3>✅ Expected (CoreDNS):</h3>
<pre><code>nameserver 10.96.0.10
search default.svc.cluster.local svc.cluster.local cluster.local
options ndots:5</code></pre>

<h3>❌ Problem (External DNS):</h3>
<pre><code>nameserver 8.8.8.8
# No search domains!</code></pre>

<hr>

<h2>3️⃣ Test HTTP Connectivity</h2>
<pre><code>/ # wget -qO- http://nginx-service</code></pre>

<h3>✅ Working:</h3>
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Welcome to nginx!&lt;/title&gt;
...
Welcome to nginx!
</code></pre>

<h3>❌ DNS Failure:</h3>
<pre><code>wget: can't resolve nginx-service: Name or service not known</code></pre>

<hr>

<h2>4️⃣ Verify Service & Endpoints</h2>
<pre><code># From outside pod
kubectl get svc nginx-service
kubectl get endpoints nginx-service</code></pre>

<h3>✅ Expected:</h3>
<pre><code>NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
nginx-service  ClusterIP   10.96.235.145   &lt;none&gt;        80/TCP    5m

NAME           ENDPOINTS          AGE
nginx-service  10.244.1.10:80     5m</code></pre>

<hr>

<h2>🔍 Root Cause Analysis</h2>

<table>
<tr><td><strong>Symptom</strong></td><td><strong>Problem</strong></td><td><strong>Cause</strong></td></tr>
<tr><td><code>nameserver 8.8.8.8</code></td><td>DNS Hijacked</td><td>Pod spec overrides <code>dnsPolicy</code> or <code>dnsConfig</code></td></tr>
<tr><td>No <code>search</code> domains</td><td>Short names fail</td><td>Custom <code>/etc/resolv.conf</code> missing search paths</td></tr>
<tr><td>NXDOMAIN errors</td><td>CoreDNS bypassed</td><td>Node DNS config leaked to pod</td></tr>
</table>

<hr>

<h2>✅ Next Steps</h2>
<p align="center">
  <a href="fix.md" style="font-size:1.5em">🔧 How to Fix →</a>
</p>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
