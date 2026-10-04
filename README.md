# Cloud Computing - Experiment 2: Dockerize Python Web Application

**Author:** Nupur Bagave  
**USN:** 01FE24BCI029 | **Division:** A | **Roll No:** 125  
**Repository:** [cloudcomputing_exp02](https://github.com/Nupur922/cloudcomputing_exp02)

---

## 📌 Overview

This experiment demonstrates containerization of a Python Flask web application using **Docker**. The repository contains the source code (`app.py`), dependency configuration (`requirements.txt`), image specification (`Dockerfile`), and complete report documentation.

---

## 📁 Repository Structure

```
cloudcomputing_exp02/
├── app.py                                              # Flask Web Application code
├── Dockerfile                                          # Docker build configuration instructions
├── requirements.txt                                    # Python dependencies
├── Experiment_1_Dockerize_Python_Web_Application_Report.docx  # Execution report with screenshots
└── README.md                                          # Setup and execution documentation
```

---

## 🎯 Learning Outcomes & Objectives

1. Understand the core principles of application containerization with Docker.
2. Develop a Python Flask web application.
3. Write and understand a multi-stage/slim `Dockerfile`.
4. Build a lightweight Docker image (`python:3.12-slim`).
5. Run Docker containers in detached mode (`-d`) with port forwarding (`-p 5000:5000`).
6. Verify container runtime, inspect logs, and test application endpoints in the browser.

---

## 💻 Source Files & Configuration

### `app.py`
```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello! My first Docker application is running."

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

### `requirements.txt`
```text
flask
```

### `Dockerfile`
```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

---

## 🚀 Step-by-Step Execution Guide

### Step 1: Verify Docker Installation
Verify that Docker Desktop / Docker Engine is running:
```bash
docker --version
docker run hello-world
```

### Step 2: Build the Docker Image
Build the Docker image tagged as `my-python-app`:
```bash
docker build -t my-python-app .
```

### Step 3: Inspect Local Docker Images
List images to verify `my-python-app` is built:
```bash
docker images
```

### Step 4: Run the Docker Container
Run the container in detached background mode with host port `5000` mapped to container port `5000`:
```bash
docker run -d -p 5000:5000 --name my-python-container my-python-app
```

### Step 5: Check Running Container & Logs
Confirm that the container is running and check application logs:
```bash
docker ps
docker logs my-python-container
```

### Step 6: Test Application in Browser
Open your browser or run curl to access:
```
http://localhost:5000
```
**Expected Response:** `Hello! My first Docker application is running.`

---

## ⚙️ Container Management Commands

| Command | Purpose |
| :--- | :--- |
| `docker --version` | Displays installed Docker version |
| `docker build -t my-python-app .` | Builds Docker image from `Dockerfile` |
| `docker run -d -p 5000:5000 --name my-python-container my-python-app` | Starts container in detached mode with port mapping |
| `docker ps` | Displays active running containers |
| `docker logs my-python-container` | Displays stdout/stderr logs from the container |
| `docker stop my-python-container` | Gracefully stops the container |
| `docker start my-python-container` | Restarts a stopped container |
| `docker rm my-python-container` | Removes the container instance |
| `docker rmi my-python-app` | Deletes the built image |

---

## 📖 Report Reference

For complete experimental screenshots, step-by-step output figures, and detailed verification, refer to `Experiment_1_Dockerize_Python_Web_Application_Report.docx`.
