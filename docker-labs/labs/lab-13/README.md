# Lab 13: Managing Docker Environment Variables Across Build and Runtime

This lab demonstrates how to manage Docker environment variables in **three different ways** while running a Flask application.
-  Managing Docker Environment Variables Across Build and Runtime
-  Clone the Application Code https github.com/Ibrahim Adel15/Docker 3.git
-  Write Dockerfile
-  Use python image
-  Install flask
-  Expose port 9099
-  Run python command on app.py
-  Build Docker Image
-  Run container and set both environment variables (APP_MODE & APP_REGION ) as following:
   * i. (development, us east) as variables in the command when run docker container
   * ii. (staging, us west) in a separate file and pass the file name in the command
   * iii. (production, canada west) in the Dockerfile
---

## **1. Clone the Application Code**
```
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3
```
---
## **2. Dockerfile**
```
FROM python:3.10

# Set production environment variables (method 3: inside Dockerfile)
ENV APP_MODE=production \
    APP_REGION="canada west"

WORKDIR /app

# Copy application code
COPY Docker-3/ /app

# Install flask
RUN pip install flask

# Expose port 9099
EXPOSE 9099

# Run the app
CMD ["python", "app.py"]
```
---
3. Build the Docker Image
```
docker build -t flask-env-lab13 .
```
---
4. Run Methods
Method 1: Pass Environment Variables in Run Command
Example: development, us east
```
docker run -it --rm \
  -e APP_MODE=development \
  -e APP_REGION="us east" \
  -p 9099:9099 flask-env-lab13
```
Method 2: Pass Environment Variables from a File
Create staging.env:
```
APP_MODE=staging
APP_REGION=us west
```
Run:
```
docker run -it --rm \
  --env-file staging.env \
  -p 9099:9099 flask-env-lab13
```
Method 3: Use Environment Variables from Dockerfile
These are already set in the Dockerfile as:
```
APP_MODE=production
APP_REGION=canada west
```
Run:
```
docker run -it --rm \
  -p 9099:9099 flask-env-lab13
```
---
5. Verify Environment Variables Inside the Container
```
docker exec -it <container_id> env | grep APP_
```
---
6. Access the App
Open your browser:

http://localhost:9099
<img width="1264" height="202" alt="Screenshot (142)" src="https://github.com/user-attachments/assets/2a1df31d-b9f6-489b-89b8-6bebfaf6ba5c" />

<img width="1059" height="585" alt="Screenshot (130)" src="https://github.com/user-attachments/assets/4ae27889-005e-4539-b236-41bb477399a5" />
