title: Ansible Training
author:
  name: Rohit Gupta
  twitter: rohit01
  url: http://www.rohit.io
output: session-1.html
controls: false

---
# Ansible Training
## **Getting started**

---
### Topics -- Session 1

* **Quick Intro**: CM + Ansible
* **Installation**
* **Hello world**
* **Introduction to Modules**
* **Replacing shell**
* **Excercise**

---
### Quick Intro: CM + Ansible

* Configuration Management
* No special privileges required
* Runs tasks under ssh — no new daemon required
* Python — so runs on most standard linux installs
* Orchestration platform

---
### Installation

**Python Virtual Environment:**

```bash
$ sudo apt-get install python-pip
$ sudo pip install virtualenv
$ virtualenv venv
$ source venv/bin/activate
```

**Ansible:**

```bash
(venv) $ pip install ansible
```

---
### Hello world

Create inventory file: **ansiblehosts**

```bash
$ echo "ansible.rohit.io" > ansiblehosts
$ cat ansiblehosts
ansible.rohit.io
```

**Execute**

```bash
$ source venv/bin/activate
(venv) $ ansible all -v -i ansiblehosts -m ping
```

---
### Introduction to Modules

* **command**

```bash
(venv) $ ansible all -v -i ansiblehosts -m command -a 'echo "Hello Ansible!"'
(venv) $ ansible all -v -i ansiblehosts -m command -a 'date'
(venv) $ ansible all -v -i ansiblehosts -m command -a 'echo "HZllo" | tr Z e'
```

* **shell**

```bash
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'echo "Similar Module!"'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'cal'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'echo "HZllo" | tr Z e'
```

---

* **file**

```bash
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'ls -l'
(venv) $ ansible all -v -i ansiblehosts -m file -a 'path=devops state=touch'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'ls -l'
(venv) $ ansible all -v -i ansiblehosts -m file -a 'path=devops state=absent'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'ls -l'
(venv) $ ansible all -v -i ansiblehosts -m file -a 'path=.ssh/authorized_keys state=absent'
(venv) $ ansible all -v -i ansiblehosts -m ping
(venv) $ ssh ansible.rohit.io
(venv) $ ps aux | grep ansible
(venv) $ deactivate
$ source venv/bin/activate
(venv) $ ansible all -v -i ansiblehosts -m ping
```

---

* **copy**

```bash
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'ls -l'
(venv) $ ansible all -v -i ansiblehosts -m copy -a 'src=ansiblehosts dest=~'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'ls -l'
(venv) $ ansible all -v -i ansiblehosts -m copy -a 'src=ansiblehosts dest=~ mode=0600'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'ls -l'
```

---
* **cron**

```bash
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'crontab -l'
(venv) $ ansible all -v -i ansiblehosts -m cron -a 'name="devops" job="date > date_output"'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'crontab -l'
(venv) $ ansible all -v -i ansiblehosts -m cron -a 'name="devops" job="date > date_output" minute=53'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'crontab -l'
(venv) $ ansible all -v -i ansiblehosts -m cron -a 'name="newjob" job="cal > cal_output"'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'crontab -l'
(venv) $ ansible all -v -i ansiblehosts -m cron -a 'name="devops" state=absent'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'crontab -l'
(venv) $ ansible all -v -i ansiblehosts -m cron -a 'name="newjob" state=absent'
(venv) $ ansible all -v -i ansiblehosts -m shell -a 'crontab -l'
```

---
### Replacing shell: ansible_shell.sh

```bash
#!/usr/bin/env bash

inventory_file="$1"
prefix="ansible all -v -i $inventory_file -m shell -a "

echo "Prefix: $prefix"
echo

$prefix 'date'
$prefix 'ls -l'
$prefix 'cal'
$prefix 'echo "YipZZZZ" | tr Z e'
$prefix 'echo "Yipeee!!"'
```

```bash
**Execute**
$ chmod +x ansible_shell.sh
$ ./ansible_shell.sh ansiblehosts
```

---
### Exercise

* Convert one of your shell script into an ansible powered shell script.

---
# Questions?
