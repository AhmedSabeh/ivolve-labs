# Lab 8: Automated Host Discovery with Ansible Dynamic Inventory (AWS EC2)

-  Create AWS EC2 with tag name:ivolve
-  Set up Ansible dynamic inventories to automatically discover and manage running EC2s with tag name=ivolve.
- list the target hosts in Dynamic inventory using ansible inventory command.
-  Run any playbook or ad hoc command to verify.
---

## 📌 Prerequisites

- AWS account with EC2 access
- At least **one running EC2 instance** tagged `Name=ivolve`
- AWS CLI installed and configured:
  ```
  aws configure
  ```
- Ansible 2.12+ installed

- Python boto3 and botocore libraries:
```
  pip install boto3 botocore
```
- AWS EC2 Ansible collection:
```
  ansible-galaxy collection install amazon.aws
```
- SSH key pair for EC2 access (PEM file, chmod 400)
- project structure
```
ansible-labs/
└── lab8/
    ├── inventory_aws_ec2.yaml      # AWS EC2 dynamic inventory config
    ├── group_vars/
    │   └── tag_ivolve.yaml          # SSH connection variables for group
    └── README.md                   # Lab documentation
  ```
- Finally run your test
```
ansible-inventory -i inventory_aws_ec2.yaml --graph
ansible all -i inventory_aws_ec2.yaml -m ping
```
