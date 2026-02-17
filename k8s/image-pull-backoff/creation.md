<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>📌 How I Created ImagePullBackOff Issue</h1>

<hr>

<h2>🚀 Deploy ImagePullBackOff App</h2>

<pre>cd k8s/image-pull-backoff/manifest
kubectl apply -f imagepull.yaml
deployment.apps/imagepull-error created</pre>

<h2>⏳ Wait 10sec & Watch:</h2>
<pre>kubectl get pods --watch
NAME                               READY   STATUS             RESTARTS   AGE
imagepull-error-7fc95d565f-m99s6   0/1     ImagePullBackOff   0          20s
imagepull-error-7fc95d565f-m99s6   0/1     ErrImagePull       0          29s
imagepull-error-7fc95d565f-m99s6   0/1     ImagePullBackOff   0          44s
imagepull-error-7fc95d565f-m99s6   0/1     ErrImagePull       0          58s
imagepull-error-7fc95d565f-m99s6   0/1     ImagePullBackOff   0          72s
imagepull-error-7fc95d565f-m99s6   0/1     ErrImagePull       0          108s</pre>

<hr>

<h2>🔍 What's Happening?</h2>
<ul>
    <li><strong>ErrImagePull:</strong> Kubernetes tries to pull the image and fails</li>
    <li><strong>ImagePullBackOff:</strong> Kubernetes backs off and retries with increasing delays</li>
    <li><strong>Cycle continues:</strong> ErrImagePull → ImagePullBackOff → repeat</li>
</ul>

<hr>

<h2>✅ Next Steps</h2>
<p><a href="debug-steps.md">🔍 How I Debug It →</a></p>

<hr>

<p align="center">
    <a href="index.html">← Back to ImagePullBackOff</a> | 
    <a href="../../categories/k8s.md">🏠 Kubernetes Issues</a>
</p>

</body>
</html>
