## ✅ **Exact Steps to Install ERPNext v15 on Ubuntu 24.04**

### ▶ Prerequisites

Make sure your system has:
- Updated Ubuntu 24.04  
- Python 3.12+  
- User with sudo access  
- pip 20+  
- MariaDB 10.3.x  
- Node.js 18  
- yarn 1.22+  
- 4 GB RAM and 40 GB Disk space

---

### 🔹 **Step 1 — Create Frappe User**

```bash
sudo apt-get update -y && sudo apt-get upgrade -y
sudo adduser frappe
sudo usermod -aG sudo frappe
su frappe
cd /home/frappe
```

---

### 🔹 **Step 2 — Install Git & Python**

```bash
sudo apt-get install git
sudo apt-get install python3-dev
sudo apt-get install python3-setuptools python3-pip
sudo apt install python3.12-venv
```

---

### 🔹 **Step 3 — Install MariaDB**

```bash
sudo apt-get install software-properties-common
sudo apt install mariadb-server
sudo systemctl status mariadb
```

Then secure MariaDB:

```bash
sudo mysql_secure_installation
```

**Enter Answers (recommended):**
- Switch to unix_socket authentication → `Y`  
- Change root password → `Y`  
- Remove anonymous users → `Y`  
- Disallow remote root login → `N`  
- Remove test database → `Y`  
- Reload privilege tables → `Y`

Now edit MariaDB config:

```bash
sudo nano /etc/mysql/my.cnf
```

Add at bottom:

```
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4
```

Restart service:

```bash
sudo service mysql restart
```

---

### 🔹 **Step 4 — Install Redis**

```bash
sudo apt-get install redis-server
```

---

### 🔹 **Step 5 — Install Node.js 18**

```bash
sudo apt install curl
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
source ~/.profile
nvm install 18
```

---

### 🔹 **Step 6 — Install Yarn**

```bash
sudo apt-get install npm
sudo npm install -g yarn
```

---

### 🔹 **Step 7 — Install wkhtmltopdf**

```bash
sudo apt-get install xvfb libfontconfig wkhtmltopdf
```

---

### 🔹 **Step 8 — Install Frappe Bench**

```bash
sudo -H pip3 install frappe-bench --break-system-packages
bench --version
```

---

### 🔹 **Step 9 — Initialize Bench & Install Frappe**

```bash
bench init frappe-bench --frappe-branch version-15
cd frappe-bench/
chmod -R o+rx /home/frappe
```
After you complete all the steps you want to create another setup then you can start from **Step - 9**

---

### 🔹 **Step 10 — Create a New Site**

```bash
bench new-site site1.local
```

---

### 🔹 **Step 11 — Download ERPNext & Additional Apps**

```bash
bench get-app erpnext --branch version-15
bench get-app payments
bench get-app hrms
```

---

### 🔹 **Step 12 — Install Apps on Site**

```bash
bench --site site1.local install-app erpnext
bench --site site1.local install-app payments
bench --site site1.local install-app hrms
```

---

### 🔹 **Step 13 — Start ERPNext**

```bash
bench use site1.local
bench start
```

---

### 🔹 **Optional: Post-Installation**

Turn off maintenance mode and enable scheduler:

```bash
bench --site site1.local set-maintenance-mode off
bench --site site1.local enable-scheduler
```

Enable developer mode:

```bash
bench set-config -g developer_mode 1
```

---

## 🔎 What Happens Next?

After `bench start`, you can access ERPNext in your browser at:

```
http://<your-server-IP>:8000
```

You’ll then complete first-time setup through the UI.

---
