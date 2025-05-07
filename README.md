# 🌐 Cloud Flask App with CI/CD

A minimal Flask application deployed using Docker and Jenkins with automated CI/CD to a remote server.

---

## 🧰 Tech Stack

- **Flask**: Lightweight Python web framework
- **Docker**: Containerize the app
- **Jenkins**: Automate build, test, and deployment
- **GitHub**: Source code hosting
- **Docker Hub**: Image registry
- **Remote Ubuntu Server**: Hosting environment

---

## 🗂 Project Structure
-├── app.py # Flask app
-├── Dockerfile # Docker build instructions
-├── requirements.txt # Python dependencies
-└── Jenkinsfile # Jenkins pipeline script


---

## 🔧 Jenkins Pipeline Stages

1. **Clone Repository** – Pulls source from GitHub
2. **Build Docker Image** – Builds image using `Dockerfile`
3. **Push to Docker Hub** – Uses stored credentials
4. **Deploy to Remote Server** – Pulls & runs container via SSH

---


