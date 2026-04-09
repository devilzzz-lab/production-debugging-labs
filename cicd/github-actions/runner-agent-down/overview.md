# 🚨 Runner / Agent Down Issue

## 📌 What is this issue?

In CI/CD pipelines, a **runner (GitHub Actions) or agent (Jenkins, GitLab Runner, Azure Agent)** is responsible for executing jobs.

Sometimes, pipelines fail with errors like:

* "No runner available"
* "Runner is offline"
* "Job stuck in queue"

## ⚠️ Symptoms

* Pipeline stuck in **pending state**
* Jobs not getting picked
* Runner shows **offline/inactive**
* Sudden pipeline failures without code issues

## 🎯 Root Cause

Common causes include:

* Runner service stopped
* Network connectivity issues
* Authentication/token expired
* Machine shutdown/crash
* Resource exhaustion (CPU/RAM)

## 🧠 Why this matters

Without a runner:

* CI/CD pipelines cannot execute
* Deployments are blocked
* Entire DevOps workflow stops

## 🏁 Goal

Diagnose why the runner is down and restore it to **active state**
