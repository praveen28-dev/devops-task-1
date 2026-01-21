The README.md File

Create a file named README.md in your folder and paste this content. It highlights all the bonus features you implemented.
Markdown

# DevOps Task 1: Scalable Hasura & PostgreSQL Deployment

## 🚀 Project Overview
This project deploys a production-ready, containerized stack containing **PostgreSQL** and the **Hasura GraphQL Engine**. It utilizes an **Nginx Reverse Proxy** to manage traffic and ensure secure access.

The setup is designed to be:
* **Resilient:** Auto-restart policies and data persistence are enabled.
* **Secure:** The database is isolated in a private network; Hasura is accessed only via the Nginx proxy.
* **Configurable:** All sensitive credentials are managed via environment variables.

## 🛠️ Tech Stack
* **Containerization:** Docker & Docker Compose
* **Database:** PostgreSQL 15
* **API Engine:** Hasura GraphQL Engine (v2.38.0)
* **Reverse Proxy:** Nginx (Latest)
* **OS:** Ubuntu Linux

## ⚙️ Setup Instructions

### 1. Clone the Repository

git clone [<YOUR_REPO_URL>](https://github.com/praveen28-dev/devops-task-1.git)
cd devops-task-1


2. Configure Secrets

Copy the example environment file to create your local secrets configuration:
Bash

cp .env.example .env

Modify .env and set a strong HASURA_GRAPHQL_ADMIN_SECRET.

3. Start the Application

Run the stack in detached mode:
Bash

docker-compose up -d

🔍 How to Access

Once the containers are running, the application is accessible via the Nginx proxy on Port 80:

    Hasura Console: http://<SERVER_IP>/console

    API Endpoint: http://<SERVER_IP>/v1/graphql

(No port number like :8080 is required).
🏗️ Architecture & Design Decisions
Networking & Security

    Private Backend: The postgres container runs on a private internal network (backend). Port 5432 is not exposed to the host machine, preventing unauthorized external access.

    Reverse Proxy: nginx listens on Port 80 and forwards traffic to hasura (which is also hidden from the public). This creates a single, secure entry point.

    Firewall: UFW is configured to allow only SSH (22) and HTTP (80).

Data Persistence

    A named Docker volume (postgres_data) is used. This ensures that even if the containers are destroyed (docker-compose down), the database records remain intact.

Bonus Features Implemented ✅

    Environment Variables: Decoupled configuration using .env.

    Reverse Proxy: Nginx configured for cleaner URL access.

    Firewall: UFW rules implemented to restrict ports.

    Restart Policies: restart: always added to ensure high availability.

    Monitoring: Standard Docker logging enabled.

📋 Management Commands

    Stop Stack: docker-compose down

    View Logs: docker-compose logs -f

    Check Status: docker-compose ps

