# Lab 5: Automated Web Server Configuration Using Ansible Playbooks
- Write an Ansible playbook to automate the configuration of a web server.
- Install Nginx.
- customize the web page
- Verify the configuration on managed node.

---

## 🛠 Steps Performed

### 1️⃣ Create Inventory File named `inventory.ini` and add your managed node details:

```
[webservers]
<EC2_PUBLIC_IP> ansible_user=ec2-user ansible_ssh_private_key_file=path_to_ec2_private_key
```
### 2️⃣ Create Ansible Playbook
Create a file named `webserver.yaml` with the following content:
```
---
- name: Configure web server on Amazon Linux 2023
  hosts: webservers
  become: true
  tasks:
    - name: Install Nginx using dnf
      dnf:
        name: nginx
        state: present

    - name: Customize the index.html page
      copy:
        content: |
          <html>
          <head><title>Welcome</title></head>
          <body><h1>This page is deployed using Ansible 🚀</h1></body>
          </html>
        dest: /usr/share/nginx/html/index.html

    - name: Ensure Nginx is running and enabled
      service:
        name: nginx
        state: started
        enabled: yes
```
### 3️⃣ Run the Playbook
Execute the playbook:
```
ansible-playbook -i inventory.ini webserver.yaml
```
### 4️⃣ Verify the Configuration
Using Curl:
```
curl http://<EC2_PUBLIC_IP>
```
Expected Output:
```
<html>
<head><title>Welcome</title></head>
<body><h1>This page is deployed using Ansible 🚀</h1></body>
</html>
```
Or Open in Browser:
Visit http://<EC2_PUBLIC_IP> and check if the custom message appears.
