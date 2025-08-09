# Flask CI/CD Demo

This project demonstrates a simple Flask application with a full CI/CD pipeline using GitHub Actions, Docker, and Kubernetes.

---

## 🏃‍♂️ How to Run Locally

### 1. Clone the Repository

```bash
git clone https://github.com/s-brian1/flask-cicd-demo.git
cd flask-cicd-demo
```

### 2. Install Dependencies

Make sure you have Python 3.11+ and pip installed.

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 3. Run the Application

```bash
python app.py
```

By default, the app will run on `http://localhost:8080`.

---

## 🐳 Run with Docker

Make sure you have Docker installed.

```bash
docker build -t my-app:latest .
docker run -p 8080:8080 my-app:latest
```
The app will be accessible at `http://localhost:8080`.

---

## 🚀 CI/CD Pipeline

This project uses GitHub Actions for CI/CD. Each push to the `main` branch will:

1. Run Python tests.
2. Build and push a Docker image to DockerHub.
3. Deploy the new image to your Kubernetes cluster.

### Environment Variables & Secrets

- `DOCKER_USERNAME` and `DOCKER_PASSWORD`: Used by GitHub Actions to push to DockerHub.
- `KUBECONFIG`: Base64-encoded kubeconfig for cluster access.

Set these as GitHub repository secrets.

---

## ☸️ Deploy to Kubernetes

1. **Update the image name** in `k8s/deployment.yaml` to match your DockerHub repo.
2. **Apply manifests**:

```bash
kubectl apply -f k8s/
```

The service will be created in the `my-namespace` namespace.

---

## 🔗 Useful Commands

- **Check deployment status**:
  ```bash
  kubectl get deployments -n my-namespace
  kubectl rollout status deployment/my-app -n my-namespace
  ```
- **Port-forward for local testing**:
  ```bash
  kubectl port-forward svc/my-app-service 8080:80 -n my-namespace
  ```

---

## 📝 Notes

- You can modify the workflow in `.github/workflows/ci-cd.yml` to fit your environment.
- Make sure to replace `<your-dockerhub-username>` in the manifests and workflows.
- For production, review and tighten security, resource requests, and secrets management.

---

## ❤️ Contributions

Feel free to open issues and PRs to improve this demo!
