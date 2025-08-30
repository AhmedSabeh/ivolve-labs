# Lab 18: Containerized Node.js and MySQL Stack Using Docker Compose

This lab demonstrates how to containerize a simple **Node.js application** with a **MySQL database** using Docker Compose.  
The application requires a MySQL connection and must find a database named **`ivolve`** to start working.

---

## 🚀 Steps to Run

### 1. Clone the Repository
```bash
git clone https://github.com/IbrahimAdel15/kubernetes-app.git
cd kubernetes-app
2. Create docker-compose.yml
yaml
Copy code
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=db
      - DB_USER=root
      - DB_PASSWORD=mysecret
    depends_on:
      - db
    volumes:
      - ./app/logs:/app/logs

  db:
    image: mysql:8
    environment:
      - MYSQL_ROOT_PASSWORD=mysecret
      - MYSQL_DATABASE=ivolve
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
▶️ Running the Stack
Build and start containers
bash
Copy code
docker-compose build
docker-compose up -d
Check status
bash
Copy code
docker-compose ps
You should see both app and db services running.

🛠️ Verification
1. Database
Enter the MySQL container:

bash
Copy code
docker-compose exec db mysql -u root -p
# password: mysecret
SHOW DATABASES;
You should see the database ivolve.

2. Application
Test the app:

bash
Copy code
curl http://localhost:3000/
Health check:

bash
Copy code
curl http://localhost:3000/health
Readiness check:

bash
Copy code
curl http://localhost:3000/ready
3. Logs
Logs are mounted to the host at ./app/logs.

bash
Copy code
docker-compose exec app ls /app/logs
docker-compose exec app tail -f /app/logs/*.log
📦 Push Image to Docker Hub
Find the image ID:

bash
Copy code
docker images
Tag the image:

bash
Copy code
docker tag <image_id> yourdockerhubusername/lab18-app:latest
Login to Docker Hub:

bash
Copy code
docker login
Push the image:

bash
Copy code
docker push yourdockerhubusername/lab18-app:latest
