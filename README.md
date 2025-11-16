Flask Kubernetes CI/CD Pipeline
===============================

Project Overview
----------------

This project demonstrates a **complete Continuous Integration (CI) and Continuous Delivery (CD) pipeline** for a Python Flask application using **Kubernetes orchestration**. It simulates a real-world software development workflow with **automated testing, building, and deployment**. The project leverages **GitHub Actions** for CI, **Jenkins** for CD, and **Minikube/Kubernetes** for container orchestration.

### Key Features

*   **CI/CD Pipeline:** Automatic testing, building, and deployment of the Flask application
    
*   **Kubernetes Orchestration:** Deployment with rolling updates, scaling, and load balancing
    
*   **Dockerized Application:** Containerized Flask app for consistent environments
    
*   **Automation:** GitHub Actions triggers builds on code push; Jenkins handles deployment to Kubernetes
    
*   **Monitoring & Rollbacks:** Kubernetes allows controlled rollouts and easy rollback of deployments
    

CI/CD Workflow
--------------

### Continuous Integration (GitHub Actions)

*   Triggered on every push to any branch
    
*   **Workflow steps:**
    
    1.  Setup Python environment
        
    2.  Install dependencies from requirements.txt
        
    3.  Run **flake8** linting (max line length: 90 characters)
        
    4.  Run **pytest** unit tests
        
    5.  Build Docker image
        

### Continuous Delivery (Jenkins)

*   Jenkins pipeline linked to the main branch
    
*   **Pipeline stages:**
    
    1.  **Build Docker Image:** Using Dockerfile from the repo
        
    2.  **Deploy to Kubernetes:** Apply Kubernetes manifests (kubectl apply -f kubernetes/)
        
    3.  **Verify Deployment:** Check pods, services, and rollout status
        

Building and Running Locally (Docker)
-------------------------------------

### Build Docker Image
`   docker build -t flask-app:latest .   `

### Run the Container Locally
`   docker run -p 5000:5000 flask-app:latest   `

### Access the Application
`   http://localhost:8081   `

Deploying to Kubernetes via Jenkins
-----------------------------------

### Start Minikube Cluster
`   minikube start   `

### Deploy Application via Jenkins Pipeline

*   Pipeline pulls latest code from main branch
    
*   **Stages:**
    
    *   Build Docker image
        
    *   Deploy manifests with kubectl apply -f kubernetes/
        
    *   Verify pods, services, and rollout
        

### Verify Kubernetes Deployment
`   kubectl get pods,services,deployments  kubectl rollout status deployment/   `

Kubernetes Features
-------------------

### Rolling Updates

*   Deploys new versions without downtime
    
*   Controlled by maxSurge and maxUnavailable in the deployment manifest
    

### Scaling

*   Multiple replicas allow the app to handle higher load
    
*   Adjust replicas dynamically:
`   kubectl scale deployment flask-app-deployment --replicas=3   `

### Load Balancing

*   NodePort service exposes the app to external traffic
    
*   Automatically distributes requests across replicas
    

### Resource Management

*   Requests and limits ensure pods do not consume excessive CPU/memory
    
*   Example manifest snippet:
`   resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"   `

How to Test the Pipeline
------------------------

1.  Push code changes to GitHub → triggers GitHub Actions workflow
    
2.  Create a Pull Request to develop → Admin reviews and merges
    
3.  Jenkins automatically deploys the merged code to Kubernetes
    
4.  Verify deployment via:
kubectl get pods,services   `

Best Practices Implemented
--------------------------

*   **Branch Protection:** main branch requires PR approval before merge
    
*   **Milestones & Issues:** GitHub Issues track tasks, bugs, and improvements
    
*   **Code Quality:** Linting and unit tests ensure code correctness
    
*   **Containerization:** Docker provides consistent build environments
    
*   **Kubernetes Deployment Strategies:** Rolling updates, scaling, and load balancing for reliability
    


Conclusion
----------

This project demonstrates a complete end-to-end CI/CD workflow for a Python Flask application using industry-standard tools. From local development, through automated testing, to deployment on Kubernetes, this assignment simulates a production-ready software delivery pipeline.