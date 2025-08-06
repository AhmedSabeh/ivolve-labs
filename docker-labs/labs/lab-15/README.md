# Lab 15: Custom Docker Network for Microservices
-  Clone the frontend and backend Code https://github.com/Ibrahim-Adel15/Docker5.git
-  Write Dockerfile for frontend and create image.
   *  Use python image
   *  Install packages in requirements.txt file
   *  Expose port 5000
   *  Run python command on app.py
-  Write Dockerfile for backend and create image.
   *  Use python image
   *  Install flask
   *  Expose port 5000
   *  Run python command on app.py
-  Create a new network called ivolve network.
-  Run backend container using ivolve network
-  Run frontend container (frontend1) using ivolve network.
-  Run another frontend container ( frontend2) using default network.
-  Verify the communication between containers.
-  Delete ivolve network.
---

## **1️⃣ Clone the Application Code**
```
git clone https://github.com/Ibrahim-Adel15/Docker5.git
cd Docker5
```
## 2️⃣ Build Frontend Image
Dockerfile: frontend/Dockerfile
```
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```
Build the image:
```
cd frontend
docker build -t frontend-app .
```
## 3️⃣ Build Backend Image
Dockerfile: backend/Dockerfile
```
FROM python:3.9-slim

WORKDIR /app

RUN pip install flask

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```
Build the image:
```
cd ../backend
docker build -t backend-app .
```
## 4️⃣ Create a Custom Docker Network
```
docker network create ivolve-network
```
## 5️⃣ Run Containers
Run Backend (internal only, no -p)
```
docker run -d --name backend --network ivolve-network backend-app
```
Run Frontend1 (same network as backend)
```
docker run -d --name frontend1 --network ivolve-network -p 5001:5000 frontend-app
```
Run Frontend2 (default network, isolated from backend)
```
docker run -d --name frontend2 -p 5002:5000 frontend-app
```
## 6️⃣ Test Communication
Frontend1 → Backend (✅ should work):
```
docker exec -it frontend1 ping backend
```
Frontend2 → Backend (❌ should fail):
```
docker exec -it frontend2 ping backend
```
<img width="795" height="443" alt="Screenshot (133)" src="https://github.com/user-attachments/assets/08ec189c-936a-40c0-a6d1-52ffc9d29ae2" />

## 7️⃣ Remove the Custom Network
```
docker network rm ivolve-network
```
-  Security Best Practice
   * Do NOT expose backend ports (-p) unless external access is required.

   * Keep backend accessible only through the frontend or trusted services on the same network.

   * Only expose (-p) the public-facing services like frontend or API gateways.

Network Diagram
```
[ivolve-network]
   ├── backend   (No public access)
   └── frontend1 (Public: http://localhost:5001 → talks to backend)
[default bridge network]
   └── frontend2 (Public: http://localhost:5002 → CANNOT talk to backend)
```
