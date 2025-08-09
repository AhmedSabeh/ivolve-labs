# Lab 6: Structured Configuration Management with Ansible Roles
-  Create an Ansible role for installing docker , Kubernetes CLI ‘kubectl ’, and Jenkins
-  Write Ansible playbook to run the created roles.
-  Verify the installation on managed node.
---

## Prerequisites
- **Ansible** installed on the control node  
  [Ansible Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html)
- SSH access to the managed node (key-based authentication)
- Managed node running **Amazon Linux 2023**

---
```
Lab6/
├── inventory.ini
├── install_tools.yaml
└── roles/
    ├── docker/
    │   └── tasks/
    │       └── main.yaml
    └── kubectl/
        └── tasks/
            └── main.yaml

```
---

## File Details

### **inventory.ini**
```
[all]
<public_ip> ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/private_key_file
```
-  Replace <public_ip> with the public IP address of your managed node.

-  Replace private_key_file with the actual name of your SSH private key.

### install_tools.yaml
```
---
- name: Install Docker and kubectl
  hosts: all
  become: true
  roles:
    - docker
    - kubectl
```
### roles/docker/tasks/main.yaml
```
---
- name: Install Docker on Amazon Linux 2023
  dnf:
    name: docker
    state: present
  become: true

- name: Enable and start Docker service
  systemd:
    name: docker
    enabled: yes
    state: started
  become: true
```
### roles/kubectl/tasks/main.yaml
```
- name: Download kubectl binary
  get_url:
    url: https://dl.k8s.io/release/v1.29.2/bin/linux/amd64/kubectl
    dest: /usr/local/bin/kubectl
    mode: '0755'
  become: true
```
### Steps to Run
1. Verify Inventory
      -  Edit inventory.ini to include your managed node's public IP and correct SSH key path.

2. Run the Playbook
```
ansible-playbook -i inventory.ini install_tools.yaml
```
3. Verify Installation
      -  SSH into the managed node and run, you should see the installed versions for both Docker and kubectl.
```
docker --version
kubectl version --client
```
