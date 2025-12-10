# 3-Tier Application Deployment with Docker & Ansible

This repository contains a **3-tier application** (Frontend, Backend, Database) with automated deployment using **Docker** and **Ansible**.

> **Note:** I contributed only to the **Dockerization and Ansible automation**. The frontend and backend code was provided as part of the original project.

---

## 📁 Project Structure

```
Docker-Ansible-Project/
├── DotNet-Backend/           # Backend source code (ASP.NET Core)
│   └── Dockerfile            # Backend Dockerfile
├── React-Frontend/           # Frontend source code (Vite + React)
│   └── Dockerfile            # Frontend Dockerfile
├── docker-compose.yml        # Compose file defining multi-container app
├── playbook.yml              # Ansible playbook for automated deployment
├── vars/
│   ├── main.yml              # Variables (Docker usernames, image info)
│   └── secrets.yml           # Vault-encrypted secrets (DB_PASSWORD, DOCKER_PASSWORD)
├── screenshots/              # Screenshots demonstrating app & DB connectivity
└── README.md                 # Project documentation
```

---

## 🐳 Docker & Docker Compose

* **Backend**: .NET 8 API
* **Frontend**: React + Vite served via Nginx
* **Database**: MySQL 8.0
* **Secrets Management**: Database password handled securely via Docker secrets

### Run Locally (Manual)

```bash
# Start all services
docker compose up

# Stop all services
docker compose down
```

---

## ⚡ Ansible Automation

The deployment is automated using **Ansible** (`playbook.yml`), which performs the following tasks:

1. Installs Docker and required plugins on CentOS 10
2. Starts and enables Docker service
3. Logs in to Docker Hub
4. Builds and pushes backend & frontend Docker images
5. Dynamically creates a `db_password.txt` for MySQL secret
6. Runs Docker Compose to deploy the full application
7. Cleans up temporary files after deployment

**Run the playbook:**

```bash
ansible-playbook playbook.yml --ask-vault-pass --ask-become-pass
```

---

## 🌐 Access the Application

* **Frontend:** [http://localhost:8080](http://localhost:8080)
* **Database Verification:** Create a product via the UI and confirm it is stored in MySQL

---

## 🔐 Security

* Database and Docker Hub passwords are encrypted using **Ansible Vault**
* Temporary secrets file (`db_password.txt`) is automatically deleted after deployment

---

## 📸 Screenshots

* **App Running:** `screenshots/app_running.png`
* **Database Verification:** `screenshots/add_product.png`

---

## 📌 Notes

* I worked **only on Docker and Ansible automation**
* Frontend and Backend were pre-existing
* This project demonstrates:

  * Multi-stage Docker builds
  * Docker Compose networking and secrets
  * Ansible automation for deployment
  * Secure credentials handling with Ansible Vault
