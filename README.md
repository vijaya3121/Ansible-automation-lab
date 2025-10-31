# 🚀 Ansible Automation Lab – CI/CD Deployment with GitHub Actions

This project demonstrates how to automate the provisioning and configuration of a web server using **Terraform**, **Ansible**, and **GitHub Actions**.

---

## 🧩 Project Overview

This lab automates:
- Creating an **Azure Linux VM** using **Terraform**
- Installing developer tools (**Git**, **Curl**, and **Nginx**) via **Ansible**
- Deploying a simple website automatically from **GitHub Actions (CI/CD)**

---

## 🏗️ Architecture

**GitHub Actions → SSH → Azure VM → Install + Deploy Website**

1. **Terraform**: Creates the Azure infrastructure  
2. **Ansible**: Installs Git, Curl, and Nginx on the Linux VM  
3. **GitHub Actions**: Triggers automatically on every code push to deploy updates  

---

## ⚙️ Steps Followed

### 🪴 Step 1: Provision VM with Terraform
Created a Linux VM on Azure and verified public IP connectivity.

### 🔧 Step 2: Install Ansible
Installed Ansible on the controller VM using:
```bash
sudo apt update && sudo apt install ansibl
 Step 3: Create Ansible Playbook

Created setup-dev-tools.yml to:

Install Git, Curl, and Nginx

Clone the sample website repository

Deploy files to /var/www/html

⚙️ Step 4: Configure GitHub Actions Workflow

Added a workflow file .github/workflows/deploy.yml to automatically:

SSH into the Azure VM

Execute the Ansible playbook

Redeploy the website when new commits are pushed

 Step 5: Verify Deployment

Opened the VM’s public IP in a browser and confirmed the sample website was deployed successfully

ye -y
