# 🚀 Ansible Automation Lab – CI/CD Deployment with GitHub Actions

This project demonstrates how to automate the provisioning and configuration of a web server using **Terraform**, **Ansible**, and **GitHub Actions**.

---

## 🧩 Project Overview

This lab automates:
- Creating an **Azure Linux VM** using **Terraform**
- Installing developer tools (**Git**, **Curl**, **Nginx**) via **Ansible**
- Deploying a simple website automatically using **GitHub Actions (CI/CD)**

---

## 🏗️ Architecture

**GitHub Actions → SSH → Azure VM → Install + Deploy Website**

1. **Terraform** – Creates the Azure infrastructure  
2. **Ansible** – Installs Git, Curl, and Nginx on the Linux VM  
3. **GitHub Actions** – Triggers automatically on every code push to deploy updates  

---

## ⚙️ Steps Followed

### 🪜 Step 1: Provision VM with Terraform
Created a Linux VM on Azure and verified public IP connectivity.

---

### 🧰 Step 2: Install Ansible
Installed Ansible on the controller VM using:
```bash
        sudo apt update && sudo apt install ansible -y
```

---


### 📑 Step3: Create Ansible playbook
Created a playbook named setup-dev-tools.yml

Install Git, Curl, and Nginx

Clone the sample website repository

Copy index.html to /var/www/html

Example snippet:

```
- name: Setup Developer Tools
  hosts: web
  become: yes
  tasks:
    - name: Install Git, Curl, and Nginx
      apt:
        name:
          - git
          - curl
          - nginx
        state: present
        update_cache: yes

    - name: Copy sample index.html to Nginx directory
     copy:
        src: /home/azureuser/sample-website/index.html
        dest: /var/www/html/index.html

```
---

### ⚙️ Step 4: Configure GitHub Actions Workflow

Added a workflow file .github/workflows/deploy.yml to trigger Ansible automatically on every push to the main branch.

Example workflow:

```
name: Deploy with Ansible

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Run Ansible Playbook on Azure VM
        uses: appleboy/ssh-action@v0.1.8
        with:
          host: ${{ secrets.AZURE_VM_IP }}
          username: azureuser
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          script: |
            cd ~/ansible-labs
            ansible-playbook setup-dev-tools.yml
```

---

### 🌐 Step 5: Verify Deployment

After GitHub Actions completed successfully:

Visited the VM’s public IP in a browser.

The sample website’s homepage appeared successfully

---

### Ansible Playbook Execution:
![Ansible run](https://github.com/vijaya3121/Ansible-automation-lab/blob/main/ansible-run.png.png)
### Github Action workflow:
![Github workflow](https://github.com/vijaya3121/Ansible-automation-lab/blob/main/github-action-workflow.png.png)
### Nginx homepage:
![Nginx output](https://github.com/vijaya3121/Ansible-automation-lab/blob/main/nginx-homepage.png.png)

---

### 🌱 Future Enhancements

Add automatic SSL configuration using Certbot

Deploy Docker containers through Ansible roles

Integrate Terraform and Ansible in a single CI/CD workflow

Add monitoring with Prometheus + Grafana

---

### 🧾 Results

✅ Successfully provisioned infrastructure with Terraform
✅ Configured and deployed Nginx using Ansible
✅ Automated deployment pipeline via GitHub Actions
✅ Website auto-updated on every commit to main branch

---

### 👩‍💻 Author

Vijaya Reddy
💼 DevOps & Cloud Engineer




















