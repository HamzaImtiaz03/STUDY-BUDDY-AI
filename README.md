# Study Buddy AI: Intelligent Quiz Generation for Enhanced Learning

![Study Buddy AI Banner](https://github.com/HamzaImtiaz03/STUDY-BUDDY-AI/blob/main/Project%20Tech%20Stacks%20Image.png?raw=true) <!-- Replace with actual image URL or embed if available -->

[![GitHub Repo](https://img.shields.io/badge/GitHub-Repo-blue?logo=github)](https://github.com/HamzaImtiaz03/STUDY-BUDDY-AI)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue?logo=docker)](https://www.docker.com/)
[![Kubernetes Deployed](https://img.shields.io/badge/Deployed-Kubernetes-orange?logo=kubernetes)](https://kubernetes.io/)
[![GCP Hosted](https://img.shields.io/badge/Hosted-GCP-brightgreen?logo=google-cloud)](https://cloud.google.com/)
[![Jenkins CI/CD](https://img.shields.io/badge/CI%2FCD-Jenkins-blue?logo=jenkins)](https://www.jenkins.io/)
[![ArgoCD GitOps](https://img.shields.io/badge/GitOps-ArgoCD-purple?logo=argo)](https://argoproj.github.io/cd/)

## Overview

**Study Buddy AI** is an innovative AI-driven platform designed to revolutionize studying by generating personalized quizzes tailored to user-specified topics, question types, difficulty levels, and quantities. Powered by advanced language models, it creates engaging multiple-choice or fill-in-the-blank questions, evaluates responses, and provides detailed results to foster effective learning and retention.

This project exemplifies modern MLOps and GitOps practices, integrating AI development with automated CI/CD pipelines. From local Streamlit-based interactions to scalable deployments on Google Cloud Platform (GCP) using Kubernetes (via Minikube), Jenkins for continuous integration/delivery, and ArgoCD for declarative GitOps synchronization, it ensures seamless updates and high availability. Ideal for students, educators, and e-learning platforms, Study Buddy AI combines educational AI with enterprise-grade infrastructure for reliable, efficient deployment.

## Key Features

- **Dynamic Quiz Generation**: Leverages LangChain and Groq for creating customized quizzes on any topic, with options for question types (Multiple Choice, Fill-in-the-Blank), difficulty (Easy, Medium, Hard), and count (1-10).
- **Interactive User Interface**: Streamlit frontend for intuitive quiz settings, real-time generation, submission, evaluation, and result visualization, including score percentages and correct/incorrect breakdowns.
- **Session Management**: Stateful quiz handling with Streamlit session states for tracking generation, attempts, submissions, and results.
- **Result Export**: Save and download quiz results as CSV for record-keeping or analysis.
- **Automated CI/CD Pipeline**: Jenkins pipeline for building Docker images, pushing to DockerHub, updating Kubernetes manifests, and committing changes to trigger ArgoCD syncs.
- **GitOps Workflow**: ArgoCD monitors GitHub for manifest changes and auto-deploys to Kubernetes, ensuring declarative infrastructure.
- **Containerization & Orchestration**: Docker for packaging, Kubernetes Deployments/Services for scaling (e.g., 2 replicas), and secrets for secure API key management.
- **Cloud-Native Deployment**: Hosted on GCP VM with Minikube, supporting automated builds and webhook-triggered updates.

## Architecture

The project is organized into development, application, versioning/containerization, infrastructure/deployment, and CI/CD phases, as illustrated below:

![Project Architecture Flowchart](https://github.com/HamzaImtiaz03/STUDY-BUDDY-AI/blob/main/81%20-%20Introduction%20to%20the%20Project%20-%20Study+Buddy+AI+Workflow.png?raw=true) <!-- Replace with actual image URL or embed -->

### High-Level Breakdown:
1. **Development & Setup**: Project initialization with Groq API, configuration, question schemas/models, prompt templates, Groq client setup, question generator, and helper classes.
2. **Main Application**: Streamlit app for UI, quiz management (generation, attempts, evaluation, results).
3. **Versioning & Containerization**: GitHub for code versioning, Dockerfile for image building.
4. **Infrastructure & Deployment**: Kubernetes manifests (deployment.yaml, service.yaml), GCP VM setup with Minikube.
5. **CI/CD Pipeline**: Jenkins setup/integration, Docker image build/push, YAML updates, Git commits, ArgoCD sync via webhooks.

This architecture promotes automation, scalability, and consistency from code to production.

## Technologies Used

- **AI/ML Frameworks**: LangChain (core, Groq integration), Pandas (data handling).
- **Frontend**: Streamlit (interactive web apps).
- **Environment Management**: Python-dotenv (secrets handling).
- **Containerization & Orchestration**: Docker (containerization), Kubernetes (via Minikube), Kubectl (management).
- **CI/CD & GitOps**: Jenkins (pipelines), ArgoCD (declarative deployments), GitHub Webhooks (triggers).
- **Cloud Platform**: Google Cloud Platform (GCP VM).
- **Version Control**: GitHub.
- **Packaging**: Setuptools (via setup.py).

Full dependencies are listed in `requirements.txt`.

## Installation

### Prerequisites
- Python 3.10+
- Git
- Docker (for containerization)
- Google Cloud Platform Account (for deployment)
- API Keys: Groq (stored in `.env`)
- Optional: Minikube, Kubectl, Jenkins, ArgoCD for full pipeline

### Steps
1. **Clone the Repository**:
   ```
   git clone https://github.com/HamzaImtiaz03/STUDY-BUDDY-AI.git
   cd STUDY-BUDDY-AI
   ```

2. **Set Up Virtual Environment** (Recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Unix/Mac
   # Or on Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```
   pip install -e .
   ```

4. **Configure Environment Variables**:
   Create a `.env` file in the root directory:
   ```
   GROQ_API_KEY=your_groq_api_key
   # Add other variables as needed
   ```

## Usage

1. **Run the Application Locally**:
   ```
   streamlit run application.py
   ```
   - Access the app at `http://localhost:8501`.
   - Select quiz settings in the sidebar (topic, type, difficulty, number), generate, attempt, submit, and review results.

2. **Query Examples**:
   - Topic: "Indian History", Type: Multiple Choice, Difficulty: Medium, Questions: 5 → Generates history quiz.
   - Submit answers, view scores, and download CSV results.

3. **Customization**:
   - Extend question types or topics in `question_generator.py`.
   - Modify UI elements in `application.py`.

## Deployment

This project features a GitOps-driven deployment on GCP with automated CI/CD.

### Prerequisites
- GCP VM Instance (configured as per `FULL_DOCUMENTATION.md`).
- Minikube, Docker, Kubectl, Jenkins, ArgoCD installed on VM.
- Credentials: DockerHub, GitHub Token, Kubeconfig.

### Pipeline Overview (via Jenkinsfile)
1. **Checkout GitHub**: Pull code.
2. **Build Docker Image**: Build and tag.
3. **Push to DockerHub**: Upload image.
4. **Update YAML**: Modify deployment.yaml with new tag.
5. **Commit Changes**: Push updated YAML to GitHub.
6. **Install Tools & Sync**: Install Kubectl/ArgoCD CLI, login, and sync app.

### Detailed Steps
- Follow `FULL_DOCUMENTATION.md` for GCP VM setup, Docker/Minikube/Jenkins/ArgoCD installation, namespace creation, secrets (e.g., GROQ_API_KEY), manifests application, and webhook configuration.
- Build and run Docker image locally:
  ```
  docker build -t study-buddy-ai .
  docker run -p 8501:8501 study-buddy-ai
  ```
- Deploy to GCP Kubernetes:
  ```
  kubectl create secret generic groq-api-secret --from-literal=GROQ_API_KEY=your_key
  kubectl apply -f manifests/deployment.yaml
  kubectl apply -f manifests/service.yaml
  minikube tunnel  # For LoadBalancer
  kubectl port-forward svc/llmops-service 8501:80 --address 0.0.0.0
  ```
- Trigger pipeline via GitHub push/webhook; ArgoCD auto-syncs changes.
- Access ArgoCD UI at `http://<VM-IP>:31704` (default: admin/initial-password).

Once deployed, access the app via external IP on port 8501.

## Contributing

Contributions are encouraged to improve quiz algorithms, add features, or enhance pipelines! To contribute:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/YourFeature`).
3. Commit changes (`git commit -m 'Add YourFeature'`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Open a Pull Request.

Ensure changes align with GitOps practices and include tests/documentation.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Frameworks: LangChain, Groq, Streamlit, Pandas.
- Tools: Docker, Kubernetes, Minikube, Jenkins, ArgoCD, GCP.
- Inspired by AI tools for personalized education and GitOps for modern DevOps.

For inquiries or support, open an issue on GitHub or contact [Hamza Imtiaz](mailto:hamzaimtiaz8668@gmail.com).

---

*Built by Hamza Imtiaz | Your AI Companion for Smarter Studying*