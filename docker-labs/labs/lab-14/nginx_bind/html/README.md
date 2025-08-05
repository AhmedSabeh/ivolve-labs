# Lab 14: Docker Volume and Bind Mount with Nginx
-  Create nginx_logs volume to persist Nginx logs and verify it in the default volumes path.
-  Create a directory nginx bind/html to serve a custom HTML file from your host machine
-  Create index.html file with “ Hello from Bind Mount ” syntax in nginx bind/html directory.
-  **Run Nginx container with the following:**
   *  Volume for var / nginx
   *  Bind Mount for usr / nginx /html
-  Verify Nginx page by running curl command from your local machine.
-  Change in the index.html file in your local machine then verify Nginx page again.
-  Verify logs is stored in the nginx_logs volume.
-  Delete the volume.
---

## Steps

### 1️⃣ Create a Docker Volume for Nginx Logs
```
docker volume create nginx_logs
```
*  Verify volume details:
```
docker volume inspect nginx_logs
```
2️⃣ Create a Directory for the Bind Mount HTML
```
mkdir -p nginx_bind/html
```
3️⃣ Create a Custom HTML File
```
echo "Hello from Bind Mount" > nginx_bind/html/index.html
```
4️⃣ Run the Nginx Container
*  Volume: Mount nginx_logs to /var/log/nginx

*  Bind Mount: Mount nginx_bind/html to /usr/share/nginx/html
```
docker run -d \
  --name mynginx \
  -p 5000:80 \
  -v nginx_logs:/var/log/nginx \
  -v $(pwd)/nginx_bind/html:/usr/share/nginx/html \
  nginx
```
5️⃣ Verify the Nginx Page
```
curl http://localhost:5000
```
Expected output:
```
Hello from Bind Mount
```
<img width="1061" height="589" alt="Screenshot (131)" src="https://github.com/user-attachments/assets/364546eb-9803-472f-8cc8-b3ce03693698" />

6️⃣ Update HTML and Verify Again
Edit the local HTML file:
```
echo "Hello from Bind Mount - Updated!" > nginx_bind/html/index.html
```
Check again:
```
curl http://localhost:5000
```
Expected output:
```
Hello from Bind Mount - Updated!
```
<img width="1069" height="586" alt="Screenshot (132)" src="https://github.com/user-attachments/assets/fd2db655-03e4-4012-9f23-80b804982362" />

7️⃣ Verify Logs in the Volume
Find the volume path:
```
docker volume inspect nginx_logs
```
Check logs:
```
sudo ls /var/lib/docker/volumes/nginx_logs/_data
```
You should see files like:
```
access.log
error.log
```
8️⃣ Delete the Volume
Stop and remove the container:
```
docker rm -f mynginx
```
Remove the volume:
```
docker volume rm nginx_logs
```
