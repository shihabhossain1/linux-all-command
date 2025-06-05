Here's a complete README file documenting common Linux Ubuntu 24.04 commands including system monitoring, installation of services (Redis, Elasticsearch, PostgreSQL, pyenv), Python version management, and display scaling.

You can save this as a file called README.md:

📄 README.md

````markdown
# Ubuntu 24.04 - Command Reference Guide

This document includes step-by-step Linux commands for installing and managing common development tools and services on Ubuntu 24.04 LTS.

---

## 📦 System Update

```bash
sudo apt update
sudo apt upgrade -y
````

---

## 🧠 System Monitoring & CPU Information

### Check CPU Info

```bash
lscpu
cat /proc/cpuinfo
```

### Check CPU Usage (Live)

```bash
top
```

Alternative (better UI):

```bash
sudo apt install htop
htop
```

### Check CPU usage with mpstat

```bash
sudo apt install sysstat
mpstat 1
```

### Load average and uptime

```bash
uptime
```

---

## 🖥️ Set Custom Display Scale to 115%

```bash
gsettings set org.gnome.desktop.interface scaling-factor 1
gsettings set org.gnome.desktop.interface text-scaling-factor 1.15
```

To enable fractional scaling (optional):

```bash
gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"
```

---

## 🐍 Install pyenv & Python 3.11

### Install required packages

```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
libffi-dev liblzma-dev git
```

### Install pyenv

```bash
curl https://pyenv.run | bash
```

### Add to shell config (.bashrc or .zshrc)

```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

Then apply:

```bash
source ~/.bashrc  # or source ~/.zshrc
```

### Install Python 3.11

```bash
pyenv install 3.11.9
pyenv global 3.11.9
```

Verify:

```bash
python --version
```

---

## 💾 Install Redis Server

```bash
sudo apt update
sudo apt install redis-server -y
sudo systemctl enable redis-server
sudo systemctl start redis-server
```

### Test Redis

```bash
redis-cli
ping
# Output: PONG
```

---

## 🔎 Install Elasticsearch (latest 8.x)

### Add GPG key and repo

```bash
sudo apt install -y curl gnupg apt-transport-https
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/elastic-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

### Install Elasticsearch

```bash
sudo apt update
sudo apt install elasticsearch -y
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

### Check status

```bash
sudo systemctl status elasticsearch
```

### Stop Elasticsearch

```bash
sudo systemctl stop elasticsearch
```

---

## 🐘 Install PostgreSQL 17

### Add PostgreSQL repository

```bash
sudo apt install curl gnupg lsb-release -y
echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" | \
sudo tee /etc/apt/sources.list.d/pgdg.list
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/postgresql.gpg > /dev/null
```

### Install PostgreSQL 17

```bash
sudo apt update
sudo apt install postgresql-17 -y
sudo systemctl enable postgresql
sudo systemctl start postgresql
```

### Access PostgreSQL shell

```bash
sudo -i -u postgres
psql
# Type \q to quit
```

### Set postgres password

```bash
psql -c "ALTER USER postgres PASSWORD 'your_password';"
```

---

## ✅ Summary of Useful Service Commands

| Task            | Command                          |
| --------------- | -------------------------------- |
| Start Service   | sudo systemctl start <service>   |
| Stop Service    | sudo systemctl stop <service>    |
| Enable on Boot  | sudo systemctl enable <service>  |
| Disable on Boot | sudo systemctl disable <service> |
| Check Status    | sudo systemctl status <service>  |

Examples:

```bash
sudo systemctl start redis-server
sudo systemctl stop elasticsearch
sudo systemctl restart postgresql
```

---

Feel free to customize this file to match your specific environment or workflow.

```

Let me know if you'd like this saved as a downloadable file (e.g., zip or .md file), or if you'd like to include additional tools like Docker, Node.js, or Nginx.
```



Here is a categorized list of essential Linux commands, from basic to advanced, useful for Ubuntu 24.04 and other distributions.

---

# 🐧 Linux Command Cheat Sheet (Basic to Advanced)

---

## 📁 File and Directory Management (Basic)

| Task                       | Command                  |
| -------------------------- | ------------------------ |
| Show current directory     | pwd                      |
| List files                 | ls                       |
| List all (incl. hidden)    | ls -a                    |
| Long format list           | ls -l                    |
| Change directory           | cd foldername            |
| Go to parent directory     | cd ..                    |
| Make directory             | mkdir folder             |
| Remove empty directory     | rmdir folder             |
| Remove file                | rm file.txt              |
| Remove directory + content | rm -r folder/            |
| Copy file                  | cp file1.txt file2.txt   |
| Move/rename file           | mv file1.txt newname.txt |
| View file content          | cat file.txt             |
| View with paging           | less file.txt            |
| Edit file (CLI editor)     | nano file.txt            |

---

## 🔍 File & Text Search (Intermediate)

| Task                       | Command                           |
| -------------------------- | --------------------------------- |
| Find files by name         | find . -name "filename.txt"       |
| Find files by extension    | find /path -type f -name "\*.log" |
| Search inside files        | grep "text" file.txt              |
| Recursive search in folder | grep -r "text" /folder            |

---

## 🧠 System Information

| Task                       | Command             |
| -------------------------- | ------------------- |
| Check CPU info             | lscpu               |
| View memory usage          | free -h             |
| View disk usage            | df -h               |
| View disk usage per folder | du -sh \*           |
| Show system uptime         | uptime              |
| View system info           | uname -a            |
| Check running kernel       | uname -r            |
| Get Linux version          | cat /etc/os-release |

---

## ⚙️ Process & Resource Monitoring

| Task                  | Command                      |                  |
| --------------------- | ---------------------------- | ---------------- |
| Show live processes   | top                          |                  |
| Improved task manager | htop (sudo apt install htop) |                  |
| Search for process    | ps aux                       | grep processname |
| Kill process by PID   | kill 1234                    |                  |
| Kill by name          | pkill firefox                |                  |

---

## 🔐 User & Permission Management

| Task                   | Command                         |
| ---------------------- | ------------------------------- |
| Add new user           | sudo adduser username           |
| Switch user            | su - username                   |
| Show current user      | whoami                          |
| Show logged-in users   | w                               |
| Change file owner      | sudo chown user\:group file.txt |
| Change permissions     | chmod 755 script.sh             |
| Make script executable | chmod +x script.sh              |

---

## 📦 Package Management (APT - Ubuntu/Debian)

| Task                    | Command                      |
| ----------------------- | ---------------------------- |
| Update package list     | sudo apt update              |
| Upgrade packages        | sudo apt upgrade             |
| Install package         | sudo apt install packagename |
| Remove package          | sudo apt remove packagename  |
| Search package          | apt search keyword           |
| List installed packages | dpkg -l                      |

---

## 🌐 Network & Internet

| Task                | Command                                                           |
| ------------------- | ----------------------------------------------------------------- |
| Show IP address     | ip a                                                              |
| Show hostname       | hostname                                                          |
| Ping a host         | ping google.com                                                   |
| Download file (CLI) | wget [https://example.com/file.zip](https://example.com/file.zip) |
| Test open port      | telnet domain.com 80                                              |
| Check open ports    | ss -tuln                                                          |

---

## 🧩 Disk & Mounting (Advanced)

| Task                    | Command                   |
| ----------------------- | ------------------------- |
| List block devices      | lsblk                     |
| Mount disk              | sudo mount /dev/sdb1 /mnt |
| Unmount disk            | sudo umount /mnt          |
| Check disk usage        | df -h                     |
| Format disk (DANGEROUS) | sudo mkfs.ext4 /dev/sdb1  |

---

## 🧰 Systemd & Services

| Task                 | Command                        |
| -------------------- | ------------------------------ |
| Start service        | sudo systemctl start service   |
| Stop service         | sudo systemctl stop service    |
| Restart service      | sudo systemctl restart service |
| Enable on boot       | sudo systemctl enable service  |
| Check service status | sudo systemctl status service  |

---

## 📜 Archiving and Compression

| Task                   | Command                          |
| ---------------------- | -------------------------------- |
| Create tar.gz archive  | tar -czvf archive.tar.gz folder/ |
| Extract tar.gz archive | tar -xzvf archive.tar.gz         |
| Zip files              | zip file.zip file1 file2         |
| Unzip file             | unzip file.zip                   |

---

## 🧪 Scripting & Automation

| Task              | Command                       |
| ----------------- | ----------------------------- |
| Run shell script  | ./script.sh or bash script.sh |
| Schedule cron job | crontab -e                    |
| View cron jobs    | crontab -l                    |

Example cron entry:

```cron
0 2 * * * /home/user/backup.sh
```

(runs every day at 2 AM)

---

## 🐍 Python & Virtualenv

| Task                 | Command                       |
| -------------------- | ----------------------------- |
| Check Python version | python3 --version             |
| Install venv         | sudo apt install python3-venv |
| Create venv          | python3 -m venv venv          |
| Activate venv        | source venv/bin/activate      |
| Deactivate venv      | deactivate                    |

---

## 🚀 Git (Version Control)

| Task          | Command                              |
| ------------- | ------------------------------------ |
| Clone repo    | git clone [https://url](https://url) |
| Init new repo | git init                             |
| Check status  | git status                           |
| Add files     | git add .                            |
| Commit        | git commit -m "message"              |
| Push changes  | git push origin main                 |

---

Would you like this in a downloadable PDF or markdown file? I can generate it for you.
