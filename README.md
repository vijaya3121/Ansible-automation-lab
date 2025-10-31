# 🧩 Ansible Automation Lab – GitHub Actions CI/CD Deployment

This project demonstrates an **automated deployment workflow** using **Ansible** and **GitHub Actions**.  
The setup installs essential tools on an Azure VM, deploys a sample website using Nginx, and verifies configuration — all triggered automatically on push to the `main` branch.

---

## 🚀 Project Overview

**Tools & Technologies Used**
- **Ansible** – Configuration management & automation
- **GitHub Actions** – CI/CD automation
- **Azure VM (Ubuntu)** – Deployment target
- **Nginx** – Web server for hosting
- **Git** & **Curl** – Supporting utilities

---

## ⚙️ Ansible Playbook

**File:** `setup-dev-tools.yml`  
This playbook installs Git, Curl, and Nginx, then clones a sample website from GitHub.

```yaml
- name: Install Git, Curl, and Nginx, then deploy website
  hosts: localhost
  become: yes

  tasks:
    - name: Install Git
      apt:
        name: git
        state: present
        update_cache: yes

    - name: Install Curl
      apt:
        name: curl
        state: present

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Clone sample website repository
      git:
        repo: "https://github.com/vijaya3121/sample-website.git"
        dest: /tmp/sample-website
        version: main
        force: yes

    - name: Copy website files to Nginx web root
      copy:
        src: /tmp/sample-website/
        dest: /var/www/html/
        owner: www-data
        group: www-data
        mode: '0644'
      notify: Restart Nginx

  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
