# Node.js CI/CD Pipeline using GitHub Actions and Docker
## Task-1
---
This project demonstrates a CI/CD pipeline to automatically build, test, push, and deploy a Dockerized Node.js application using:

- **Node.js** – simple HTTP server
- **GitHub Actions** – for CI/CD automation
- **Docker & DockerHub** – for containerization and registry
- **Amazon EC2 (localhost)** – for deployment

---

## Folder Structure

nodejs-demo-app/ <br>
├── .github/ <br>
│   └── workflows/ <br>
│       └── main.yml <br>
├── screenshots/ <br>
│  ├── github-actions-success.png <br>
│  ├── browser-response.png <br>
│  ├── dockerhub-image.png <br>
│  └── curl-response.png <br>
├── Dockerfile <br>
├── index.js <br>
├── README.md <br>
└── package.json <br>

---

## CI/CD Pipeline Flow

1. Push code to **`main`** branch.
2. GitHub Actions builds and pushes Docker image to DockerHub.
3. EC2 instance pulls the image and deploys the app via Docker.

---

## Screenshots

### 1. GitHub Actions Workflow – Success ###
This shows a successful CI/CD run triggered by a push to the **`main`** branch.

![CI/CD Success](screenshots/github-actions-success.png)

---

### 2. App Output – Via Browser
This confirms the app is running successfully on Browser at port **3000**.

![App Output](screenshots/browser-response.png)

---

### 3. DockerHub – Image Successfully Pushed
The Docker image is available on **DockerHub** after CI/CD completion.

![DockerHub Image](screenshots/dockerhub-image.png)

---

### 4. App Output – Via Curl
This confirms the app is running successfully on EC2 at port **3000**.

![App Output](screenshots/curl-response.png)

---


## Test Locally
```bash
docker build -t mukundp2001/demo-app:latest .
docker run -p 3000:3000 mukundp2001/demo-app:latest
curl http://localhost:3000
```

## Live on EC2
**Access via**: `http://<your-ec2-public-ip>:3000`

# 📘 Interview Questions & Answers – CI/CD with GitHub Actions

## 1. What is CI/CD?
**CI/CD** stands for **Continuous Integration** and **Continuous Deployment** (or **Delivery**).

- **CI (Continuous Integration):** Developers frequently push code to a shared repository. Automated builds and tests are triggered to catch bugs early.
- **CD (Continuous Deployment/Delivery):** After successful CI, the changes are automatically (Deployment) or manually (Delivery) pushed to production or staging environments.

---

## 2. How do GitHub Actions work?
GitHub Actions is a CI/CD platform integrated into GitHub that lets you automate workflows like build, test, and deployment.

- It works by defining workflows using `.yml` files inside `.github/workflows/`.
- These workflows run in response to events such as `push`, `pull_request`, etc.

---

## 3. What are runners?
**Runners** are servers that execute the jobs defined in a GitHub Actions workflow.

- **Hosted runners:** Provided by GitHub (e.g., Ubuntu, Windows, macOS).
- **Self-hosted runners:** You can configure your own infrastructure to run workflows.

---

## 4. Difference between jobs and steps
- **Jobs:** A job is a collection of steps that run on the same runner. Each job runs in its own virtual environment.
- **Steps:** Steps are individual tasks within a job, such as checking out code or running a build command. Steps run sequentially within a job.

---

## 5. How to secure secrets in GitHub Actions?
Secrets like API keys or credentials can be stored in **GitHub Repository Settings → Secrets**.

These are encrypted and can be accessed in workflows using the `secrets` context:

```yaml
env:
  DOCKER_PASSWORD: ${{ secrets.DOCKER_PASSWORD }}
```
## 6. How to handle deployment errors?
To handle deployment errors:
- Use `continue-on-error: false` to fail fast.
- Add fallback/rollback scripts in case deployment fails.
- Use try-catch-like logic with shell scripting or error-handling steps.
- Log all errors for debugging with `set -x` or `echo` for visibility.

## 7. Explain the Docker build-push workflow.
Typical Docker build-push steps in CI/CD:
```bash
docker build -t <image-name>:<tag> .
docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
docker push <image-name>:<tag>
```
## 8. How can you test a CI/CD pipeline locally?
You can test CI/CD workflows locally using tools like:
- act: Run GitHub Actions locally.
- Manual script testing: Break down the steps and test them individually in your shell/terminal.
- Use Docker locally to simulate build/test steps.
