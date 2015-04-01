title: Ansible Training
author:
  name: Rohit Gupta
  twitter: rohit01
  url: http://www.rohit.io
output: session-2.html
controls: false
<!-- style: style.css -->

---
# Ansible Training
## **Key Concepts**

---
### Topics -- Session 2

* **Playbooks**
* **Templates**
* **Roles**
* **Inventory**
* **Live Automation**
* **Best Practices**
* **Excercise**

---

## Sample Playbook - YAML File

```
- hosts: all
  vars:
    name: "knowlarity"
    department: "devops"
  gather_facts: no

  tasks:
    - debug: var="name"

    - name: "Value of variable - department"
      debug: var=department

    - shell: "date > /tmp/date_file"
      args:
        creates: "/tmp/date_file"
      notify: "show calendar"

  handlers:
    - name: "show calendar"
      shell: "cal"
```

---
# Questions?
