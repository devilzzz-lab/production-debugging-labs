<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">✅ How to Fix DNS Failure</h1>

<hr>

<h2>1️⃣ Delete Broken Pod</h2>
<pre><code>kubectl delete pod dns-failure --force</code></pre>

<p><strong>✅ Output:</strong></p>
<pre><code>pod "dns-failure" deleted</code></pre>

<hr>

<h2>2️⃣ Fix Pod YAML</h2>

<p><strong>❌ Remove these broken settings from <code>dns-failure-pod.yaml</code>:</strong></p>

<pre><code># ❌ DELETE THESE LINES:
  dnsPolicy: None                    # Bypasses K8s DNS
  dnsConfig:
    nameservers:
    - 8.8.8.8                       # External DNS breaks service discovery</code></pre>

<p><strong>✅ Fixed YAML:</strong></p>
<pre><code>apiVersion: v1
kind: Pod
metadata:
  name: dns-failure
spec:
  containers:
  - name: busybox
    image: busybox:1.28
    command: ['sh', '-c', 'while true; do sleep 30; done']
  # ✅ No dnsPolicy = Default ClusterFirst (CoreDNS)
  # ✅ No dnsConfig = Default K8s search domains</code></pre>

<hr>

<h2>3️⃣ Deploy Fixed Pod</h2>
<pre><code>kubectl apply -f dns-failure-pod.yaml</code></pre>

<p><strong>✅ Output:</strong></p>
<pre><code>pod/dns-failure created</code></pre>

<hr>

<h2>4️⃣ Verify DNS Fixed</h2>
<pre><code>kubectl exec -it dns-failure -- sh</code></pre>

<p><strong>✅ Before Fix (Broken):</strong></p>
<pre><code>/ # cat /etc/resolv.conf
nameserver 8.8.8.8
# ❌ No search domains!

/ # nslookup nginx-service
Server:  8.8.8.8
** server can't find nginx-service: NXDOMAIN ❌</code></pre>

<p><strong>✅ After Fix (Working):</strong></p>
<pre><code>/ # cat /etc/resolv.conf
nameserver 10.96.0.10
search default.svc.cluster.local svc.cluster.local cluster.local
options ndots:5 ✅

/ # nslookup nginx-service
Server:    10.96.0.10
Name:      nginx-service.default.svc.cluster.local
Address:   10.96.235.145 ✅</code></pre>

<hr>

<h2>5️⃣ Test Service Connectivity</h2>
<pre><code>/ # wget -qO- http://nginx-service</code></pre>

<p><strong>✅ Success:</strong></p>
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;title&gt;Welcome to nginx!&lt;/title&gt;
...
Welcome to nginx! ✅</code></pre>

<hr>

<h2>🧠 What Fixed It?</h2>

<table>
<tr><th>Problem</th><th>Root Cause</th><th>Solution</th></tr>
<tr><td>External DNS (8.8.8.8)</td><td><code>dnsPolicy: None</code></td><td>Remove → Default <code>ClusterFirst</code></td></tr>
<tr><td>No search domains</td><td>Custom <code>dnsConfig</code></td><td>Remove → K8s auto-config</td></tr>
<tr><td>NXDOMAIN errors</td><td>Google DNS can't resolve K8s services</td><td>Use CoreDNS (10.96.0.10)</td></tr>
</table>

<hr>

<h2>🔑 Key Commands Used</h2>
<pre><code>kubectl delete pod dns-failure --force     # Clean slate
kubectl apply -f dns-failure-pod.yaml      # Deploy fix
kubectl exec -it dns-failure -- nslookup   # Verify DNS
kubectl exec -it dns-failure -- wget       # Test connectivity</code></pre>

<hr>

<p align="center">
  <a href="overview.md">← Back to Overview</a> | 
  <a href="debug-steps.md">🔍 Debug Steps</a> | 
  <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
