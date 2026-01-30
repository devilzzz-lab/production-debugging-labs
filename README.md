<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1 align="center">My DevOps Lab</h1>
<h3 align="center">50 Real Production Issues & Solutions</h3>

<p align="center">Real-world production debugging scenarios with step-by-step solutions for DevOps Engineers</p>

<hr>

<h2>📜 Table of Contents</h2>
<ul>
    <li><a href="#-what-youll-learn">What You'll Learn</a></li>
    <li><a href="#-categories-covered">Categories Covered</a>
        <ul>
            <li><a href="#kubernetes">Kubernetes</a></li>
            <li><a href="#cicd">CI/CD</a></li>
            <li><a href="#cloud">Cloud (AWS & Azure)</a></li>
            <li><a href="#monitoring">Monitoring</a></li>
            <li><a href="#automation">Automation</a></li>
            <li><a href="#sre">SRE</a></li>
        </ul>
    </li>
    <li><a href="#-repository-structure">Repository Structure</a></li>
    <li><a href="#-technologies-covered">Technologies Covered</a></li>
    <li><a href="#-how-to-use-this-repository">How to Use This Repository</a></li>
    <li><a href="#-who-is-this-for">Who Is This For?</a></li>
    <li><a href="#-issue-structure">Issue Structure</a></li>
    <li><a href="#-contact">Contact</a></li>
</ul>

<hr>

<h2 id="-what-youll-learn">📚 What You'll Learn</h2>

<ul>
    <li><strong>Kubernetes troubleshooting</strong> - Pod crashes, network policies, resource limits</li>
    <li><strong>CI/CD pipeline debugging</strong> - Build failures, deployment rollbacks, automation</li>
    <li><strong>Monitoring & Observability</strong> - Metrics, logs, traces, alerts</li>
    <li><strong>Infrastructure as Code</strong> - Terraform, Ansible, CloudFormation</li>
    <li><strong>Security & Compliance</strong> - Secrets management, vulnerability scanning</li>
    <li><strong>Performance Optimization</strong> - Database tuning, caching strategies, load balancing</li>
</ul>

<hr>

<h2 id="-categories-covered">🎯 Categories Covered</h2>

<p><em>👆 Click the links below to explore each category</em></p>

<h3 id="kubernetes">🔗 <u><a href="categories/k8s.md">Kubernetes</a></u></h3>
<h3 id="cicd">🔗 <u><a href="categories/cicd.md">CI/CD</a></u></h3>
<h3 id="cloud">🔗 <u><a href="categories/cloud.md">Cloud (AWS & Azure)</a></u></h3>
<h3 id="monitoring">🔗 <u><a href="categories/monitoring.md">Monitoring</a></u></h3>
<h3 id="automation">🔗 <u><a href="categories/automation.md">Automation</a></u></h3>
<h3 id="sre">🔗 <u><a href="categories/sre.md">SRE</a></u></h3>



<hr>

<h2 id="-repository-structure">💡 Base Repository Design Structure</h2>

<pre>
production-debugging-labs/
│
├── k8s/
│   ├── pod-crashloop/
│   ├── image-pull-backoff/
│   ├── node-notready/
│   ├── oom-killed/
│   ├── dns-failure/
│   ├── pvc-pending/
│   └── service-unreachable/
│
├── cloud/
│   │
│   ├── aws/
│   │   ├── ec2-high-cpu/
│   │   ├── alb-503/
│   │   ├── rds-latency/
│   │   └── disk-full/
│   │
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
</pre>

<hr>

<h2 id="-issue-structure">📦 Structure of Each Issue</h2>

<p>Every issue follows a consistent format for easy learning:</p>

<pre>
issue-name/
├── overview.md          # Problem description and context
├── debug-steps.md       # How to Debug it process
├── fix.md               # Solution implementation
├── prevention.md        # Best practices to avoid recurrence
</pre>

<p><strong>Example: pod-crashloop/</strong></p>
<ul>
    <li><strong>overview.md</strong> - What happened, symptoms, impact</li>
    <li><strong>debug-steps.md</strong> - How to Fix step-by-step</li>
    <li><strong>fix.md</strong> - Root cause analysis and solution</li>
    <li><strong>prevention.md</strong> - Health checks, resource limits, best practices</li>
</ul>

<hr>

<h2 id="-technologies-covered">🛠️ Technologies Covered</h2>

<p align="center">
    <img src="https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white" alt="Kubernetes">
    <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white" alt="Docker">
    <img src="https://img.shields.io/badge/Terraform-7B42BC?logo=terraform&logoColor=white" alt="Terraform">
    <img src="https://img.shields.io/badge/AWS-232F3E?logo=amazonaws&logoColor=white" alt="AWS">
    <img src="https://img.shields.io/badge/Azure-0078D4?logo=microsoftazure&logoColor=white" alt="Azure">
    <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white" alt="GitHub Actions">
    <img src="https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white" alt="Prometheus">
    <img src="https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white" alt="Grafana">
    <img src="https://img.shields.io/badge/Jenkins-D24939?logo=jenkins&logoColor=white" alt="Jenkins">
</p>

<hr>

<h2 id="-how-to-use-this-repository">📖 How to Use This Repository</h2>

<ol>
    <li><strong>Browse by Category</strong> - Navigate to folders organized by technology</li>
    <li><strong>Read the Issue</strong> - Each issue contains problem description, symptoms, and context</li>
    <li><strong>Try to Solve</strong> - Attempt the solution before looking at the answer</li>
    <li><strong>Learn the Solution</strong> - Detailed step-by-step resolution with explanations</li>
    <li><strong>Practice</strong> - Recreate the scenario in your own environment</li>
    <li><strong>Contribute</strong> - Share your own production debugging experiences</li>
</ol>

<hr>

<h2 id="-who-is-this-for">🎓 Who Is This For?</h2>

<ul>
    <li>Junior DevOps Engineers looking to level up</li>
    <li>Software Engineers transitioning to DevOps</li>
    <li>SREs preparing for on-call rotations</li>
    <li>Anyone preparing for DevOps interviews</li>
    <li>Teams building internal knowledge bases</li>
    <li>Platform Engineers debugging infrastructure issues</li>
</ul>

<hr>

<h2 id="-contact">📬 Contact</h2>

<p>Questions? Suggestions? Reach out:</p>

<ul>
    <li><strong>LinkedIn:</strong> <a href="https://www.linkedin.com/in/sriramg-s">Sriram G</a></li>
    <li><strong>Email:</strong> srisuji0814@gmail.com</li>
    <li><strong>GitHub:</strong> <a href="https://github.com/devilzzz-lab">@devilzzz-lab</a></li>
</ul>

<hr>

<p align="center">
    <strong>⭐ Star this repo if you find it helpful!</strong>
</p>

<p align="center">
    <em>"The only way to learn production debugging is to debug production issues."</em>
</p>

<p align="center">
    Made for DevOps Engineers
</p>

</body>
</html>
