# Day 48: GitHub Actions Capstone CI/CD Project

## 🏗️ Architecture Flow

[Developer]
│
├───> (Opens PR to main) ────> [PR Pipeline]
│                                 └──> Reusable Build & Test Workflow
│                                 └──> Log PR Pass Summary
│
└───> (Merges to main)  ────> [Main Pipeline]
├──> Step 1: Reusable Build & Test Workflow
├──> Step 2: Reusable Docker Build & Push -> Docker Hub
└──> Step 3: Deploy to Production (Approval Gated)

[Cron Timer / Dispatch] ──────────> [Health Check Workflow]
└──> Pull Docker Image -> Run -> Curl Test -> Summary Report

## 🔐 Reusable Workflows Breakdown
1. **`reusable-build-test.yml`**: Modular runner setup, requirement installations, and pytest enforcement.
2. **`reusable-docker.yml`**: Centralized Docker authentication, build context processing, and registry pushing.

## 🚀 Future Improvements
- **Security Scanning:** Integrate Trivy vulnerability scanner before pushing images to Docker Hub.
- **ChatOps Notifications:** Route deployment outcomes to a Slack/Discord webhook channel.
- **Automated Rollback:** Trigger an automated rollback pipeline if post-deployment health check fails.