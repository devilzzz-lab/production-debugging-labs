<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>🛠️ STEP 1: Setup AKS (Simple Way)</h1>

<p><em>If you already have AKS → skip. If not, do this:</em></p>

<hr>

<h2>1️⃣ Install Azure CLI</h2>
<p><a href="https://learn.microsoft.com/en-us/cli/azure/install-azure-cli">Azure CLI Install Guide</a></p>

<h2>2️⃣ Login</h2>
<pre>az login</pre>

<h2>3️⃣ Create Resource Group</h2>
<pre>az group create \
  --name devops-lab-rg \
  --location eastus</pre>

<h2>4️⃣ Create AKS (Free Tier Friendly)</h2>
<pre>az aks create \
  --resource-group devops-lab-rg \
  --name devops-lab-aks-new \
  --node-count 1 \
  --node-vm-size Standard_DC2s_v3 \
  --enable-managed-identity \
  --generate-ssh-keys \
  --no-wait</pre>

<h2>5️⃣ Connect kubectl</h2>
<pre>az aks get-credentials \
  --resource-group devops-lab-rg \
  --name devops-lab-aks</pre>

<hr>

<h2>✅ Verify Setup</h2>

<h3>Check Namespaces:</h3>
<pre>kubectl get ns
NAME              STATUS   AGE
default           Active   2m53s
kube-node-lease   Active   2m53s
kube-public       Active   2m53s
kube-system       Active   2m53s</pre>

<h3>Check Nodes:</h3>
<pre>kubectl get nodes
NAME                                STATUS   ROLES    AGE     VERSION
aks-nodepool1-xxxxxx-vmss000000   Ready    <none>   3m53s   v1.33.6</pre>

<hr>

<h2>🚀 Deploy CrashLoop App</h2>

<pre>cd k8s/pod-crashloop/manifest
kubectl apply -f crashloop.yaml
deployment.apps/crashloop-app created</pre>

<h2>⏳ Wait 10sec & Watch:</h2>
<pre>kubectl get pods --watch
NAME                             READY   STATUS    RESTARTS      AGE
crashloop-app-64fbb7f6bb-r4svl   1/1     Running   2 (17s ago)   29s
crashloop-app-64fbb7f6bb-r4svl   0/1     Completed   2 (17s ago)   29s
crashloop-app-64fbb7f6bb-r4svl   0/1     CrashLoopBackOff   2 (14s ago)   43s
crashloop-app-64fbb7f6bb-r4svl   1/1     Running            3 (27s ago)   56s
crashloop-app-64fbb7f6bb-r4svl   0/1     Completed          3 (32s ago)   61s
crashloop-app-64fbb7f6bb-r4svl   0/1     CrashLoopBackOff   3 (16s ago)   77s</pre>

<hr>

<p align="center">
    <a href="../pod-crashloop/overview.md">← Back to Pod CrashLoopBackOff</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
