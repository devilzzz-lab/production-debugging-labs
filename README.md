<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">My DevOps Lab</h1>
<h3 align="center">50+ Real Production Issues & Solutions</h3>
<h3 align="center">Progress: 10 Kubernetes Issues Completed</h3>

<p align="center">
<img src="https://img.shields.io/github/stars/devilzzz-lab/production-debugging-labs?style=social">
<img src="https://img.shields.io/github/forks/devilzzz-lab/production-debugging-labs?style=social">
<img src="https://img.shields.io/github/last-commit/devilzzz-lab/production-debugging-labs">
</p>

<p align="center">Real world production debugging scenarios with step by step solutions for DevOps Engineers</p>

<hr>

<h2>🚧 Project Progress</h2>

<ul>
<li>✅ Kubernetes Troubleshooting (10 Issues)</li>
<li>🔄 CI/CD Failures (Coming Next)</li>
<li>🔄 Cloud Production Incidents</li>
<li>🔄 Monitoring Failures</li>
<li>🔄 Automation Issues</li>
<li>🔄 SRE Incidents</li>
</ul>

<hr>

<h2>🎥 Demo Videos</h2>

<p>
Watch the demo to understand how to use this Kubernetes troubleshooting lab.
</p>

<p>
<a href="YOUR_VIDEO_LINK">▶ Watch Demo of the Kubernetes Lab</a>
</p>

<hr>

<h2>📜 Table of Contents</h2>
<ul>
    <li><a href="#what-youll-learn">What You'll Learn</a></li>
    <li><a href="#categories-covered">Categories Covered</a>
        <ul>
            <li><a href="#kubernetes">Kubernetes</a></li>
            <li><a href="#cicd">CI/CD</a></li>
            <li><a href="#cloud">Cloud (AWS & Azure)</a></li>
            <li><a href="#monitoring">Monitoring</a></li>
            <li><a href="#automation">Automation</a></li>
            <li><a href="#sre">SRE</a></li>
        </ul>
    </li>
    <li><a href="#repository-structure">Repository Structure</a></li>
    <li><a href="#technologies-covered">Technologies Covered</a></li>
    <li><a href="#how-to-use">How to Use This Repository</a></li>
    <li><a href="#who-is-this-for">Who Is This For?</a></li>
    <li><a href="#issue-structure">Issue Structure</a></li>
    <li><a href="#contact">Contact</a></li>
</ul>

<hr>

<h2 id="what-youll-learn">📚 What You'll Learn</h2>
<ul>
    <li><strong>Kubernetes troubleshooting</strong> - Pod crashes, network policies, resource limits</li>
    <li><strong>CI/CD pipeline debugging</strong> - Build failures, deployment rollbacks, automation</li>
    <li><strong>Monitoring & Observability</strong> - Metrics, logs, traces, alerts</li>
    <li><strong>Infrastructure as Code</strong> - Terraform</li>
    <li><strong>Security & Compliance</strong> - Secrets management, vulnerability scanning</li>
    <li><strong>Performance Optimization</strong> - Database tuning, caching strategies, load balancing</li>
</ul>

<hr>

<h2 id="categories-covered">🎯 Categories Covered</h2>
<p align="center"><em>👆 Click the links below to explore each category</em></p>

<h3 id="kubernetes">🔗 <u><a href="categories/k8s.md">Kubernetes</a></u></h3>
<h3 id="cicd">🔗 <u><a href="categories/cicd.md">CI/CD</a></u></h3>
<h3 id="cloud">🔗 <u><a href="categories/cloud.md">Cloud (AWS & Azure)</a></u></h3>
<h3 id="monitoring">🔗 <u><a href="categories/monitoring.md">Monitoring</a></u></h3>
<h3 id="automation">🔗 <u><a href="categories/automation.md">Automation</a></u></h3>
<h3 id="sre">🔗 <u><a href="categories/sre.md">SRE</a></u></h3>


<hr>

<h2 id="repository-structure">💡 Base Repository Design Structure</h2>

<pre><code>production-debugging-labs/
│
├── k8s/
│   ├── aks-cluster-setup/
│   ├── pod-crashloop/
│   ├── image-pull-backoff/
│   ├── node-notready/
│   ├── oom-killed/
│   ├── dns-failure/
│   ├── pvc-static-binding-failure/
│   ├── pvc-waitforfirstconsumer-behavior/
│   ├── service-unreachable/
│   └── readiness-liveness-probe-failure/
│
├── cloud/
│   ├── aws/
│   │   ├── ec2-high-cpu/
│   │   ├── alb-503/
│   │   ├── rds-latency/
│   │   └── disk-full/
│   └── azure/
│       ├── vm-high-cpu/
│       ├── appgw-502/
│       ├── sql-latency/
│       └── storage-full/
│
├── cicd/
│   ├── pipeline-fail/
│   ├── artifact-missing/
│   ├── runner-down/
│   └── secret-expired/
│
├── monitoring/
│   ├── alert-fatigue/
│   ├── missing-metrics/
│   ├── false-alerts/
│   └── dashboard-broken/
│
├── automation/
│   ├── terraform-state-lock/
│   ├── ansible-failed/
│   └── config-drift/
│
├── sre/
│   ├── slo-breach/
│   ├── latency-spike/
│   └── traffic-surge/
│
├── runbooks/
│   ├── k8s.md
│   ├── aws.md
│   ├── azure.md
│   ├── cicd.md
│   └── oncall.md
│
└── README.md
</code></pre>

<hr>

<h2 id="issue-structure">📦 Structure of Each Issue</h2>

<p>Every issue follows a consistent format for easy learning:</p>

<pre><code>issue-name/  
├── overview.md
├── creation.md
├── debug-steps.md
├── fix.md
</code></pre>

<p><strong>Example: pod-crashloop/</strong></p>
<ul>
    <li><strong>overview.md</strong> - What happened, symptoms, impact</li>
    <li><strong>creation.md</strong> - How to create the scenario</li>
    <li><strong>debug-steps.md</strong> - Step-by-step debugging</li>
    <li><strong>fix.md</strong> - Root cause analysis and solution</li>
</ul>

<hr>

<h2 id="technologies-covered">🛠️ Technologies Covered</h2>

<p align="center">
    <img src="https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white">
    <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white">
    <img src="https://img.shields.io/badge/Terraform-7B42BC?logo=terraform&logoColor=white">
    <img src="https://img.shields.io/badge/AWS-232F3E?logo=amazonaws&logoColor=white">
    <img src="https://img.shields.io/badge/Azure-0078D4?logo=microsoftazure&logoColor=white">
    <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white">
    <img src="https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white">
    <img src="https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white">
    <img src="https://img.shields.io/badge/Jenkins-D24939?logo=jenkins&logoColor=white">
</p>

<hr>

<h2 id="how-to-use">📖 How to Use This Repository</h2>

<ol>
    <li><strong>Browse by Category</strong> - Navigate through folders organized by technology</li>
    <li><strong>Read the Issue</strong> - Understand the problem, symptoms, and context</li>
    <li><strong>Practice</strong> - Recreate the scenario in your own environment</li>
    <li><strong>Try to Solve</strong> - Attempt to solve the issue yourself before checking the solution</li>
    <li><strong>Learn the Solution</strong> - Follow the step-by-step resolution guide</li>
    <li><strong>Contribute</strong> - Share your own production debugging experiences</li>
</ol>

<hr>

<h2 id="who-is-this-for">🎓 Who Is This For?</h2>

<ul>
    <li>Junior DevOps Engineers looking to level up</li>
    <li>Software Engineers transitioning to DevOps</li>
    <li>SREs preparing for on-call rotations</li>
    <li>Anyone preparing for DevOps interviews</li>
    <li>Teams building internal knowledge bases</li>
    <li>Platform Engineers debugging infrastructure issues</li>
</ul>

<hr>

<h2 id="contact">📬 Contact</h2>

<ul>
    <li><strong>LinkedIn:</strong> <a href="https://www.linkedin.com/in/sriramg-s">Sriram G</a></li>
    <li><strong>Email:</strong> srisuji0814@gmail.com</li>
    <li><strong>GitHub:</strong> <a href="https://github.com/devilzzz-lab">@devilzzz-lab</a></li>
</ul>

<hr>

<p align="center"><strong>⭐ Star this repo if you find it helpful!</strong></p>

<p align="center"><em>"The only way to learn production debugging is to debug production issues."</em></p>

<p align="center">Made for DevOps Engineers 🚀</p>

</body>
</html>