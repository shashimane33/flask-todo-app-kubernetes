Flask-Express Todo Application
==============================

This is a full-stack application consisting of a Node.js (Express) frontend and a Python (Flask) backend. This repository is structured as a monorepo to demonstrate automated CI/CD pipelines and container orchestration.

🌿 Branch Strategy
------------------

-   jenkins (Current Branch): Contains the application code and the specific Jenkinsfile scripts for automated deployment to an AWS EC2 instance using Jenkins and PM2.

-   main: Contains the production-ready Kubernetes (K8s) configuration files (backend.yaml, frontend.yaml, etc.) for containerized orchestration.

📂 Project Structure
--------------------

.\


├── frontend/             # Express.js Application\
│   ├── index.js\
│   ├── package.json\
│   └── Jenkinsfile       # Pipeline for Frontend Deployment\
├── backend/              # Flask Application\
│   ├── app.py\
│   ├── requirements.txt\
│   └── Jenkinsfile       # Pipeline for Backend Deployment\
└── README.md

🚀 CI/CD Deployment (Jenkins + PM2)
-----------------------------------

The jenkins branch is configured for continuous deployment to a single AWS EC2 instance.

### 1\. Prerequisites on EC2

-   Instance Type: t3.small (or higher)

-   Tools: Java (for Jenkins), Node.js 25, Python 3.12, and Git.

-   Process Manager: PM2 installed globally (npm install -g pm2).

-   Permissions: Jenkins user added to sudoers (jenkins ALL=(ALL) NOPASSWD: ALL).

### 2\. Jenkins Setup

Create two Pipeline jobs in Jenkins:

1.  Frontend-Pipeline:

-   Definition: Pipeline script from SCM.

-   Repository URL: https://github.com/shashimane33/flask-todo-app-kubernetes.git

-   Branch: */jenkins.

-   Script Path: frontend/Jenkinsfile.

1.  Backend-Pipeline:

-   Definition: Pipeline script from SCM.

-   Repository URL: https://github.com/shashimane33/flask-todo-app-kubernetes.git

-   Branch: */jenkins.

-   Script Path: backend/Jenkinsfile.

🛠️ Operational Commands
------------------------

If you need to monitor the deployment manually via SSH:

# View all running apps (run as ubuntu user)\
sudo -u ubuntu pm2 list

# View live application logs\
sudo -u ubuntu pm2 logs

# Check Jenkins service status\
sudo systemctl status jenkins

# Monitor Webhook arrivals\
sudo journalctl -u jenkins -f

🌐 Application Access
---------------------

Once the Jenkins pipelines show a Success status, you can access the apps:

-   Frontend UI: http://<EC2_PUBLIC_IP>:3000

-   Backend API: http://<EC2_PUBLIC_IP>:5000

-   Jenkins UI: http://<EC2_PUBLIC_IP>:8080

☸️ Kubernetes Orchestration
---------------------------

To see the containerized version of this project, switch to the main branch. It contains the Dockerfiles and Kubernetes manifests needed to deploy this stack onto a K8s cluster.
